# C2PA — Content Provenance for the AI Act

## What Is C2PA and Why Should You Care?

C2PA (Coalition for Content Provenance and Authenticity) is an open standard for embedding
tamper-evident provenance metadata into content files — images, video, audio, documents.
Think of it as a chain-of-custody record baked into the file itself.

For the AI Act, Article 50(2) specifically requires that AI-generated or manipulated content
(images, audio, video) be "marked in a machine-readable format" so downstream systems can
detect it. C2PA is the leading standard for doing exactly that. If your AI system generates
or substantially modifies media files, this is your compliance path.

## When to Use C2PA vs Simpler Metadata

Use C2PA when:
- You generate images, video, or audio with AI
- You substantially edit media with AI tools
- You need tamper-evident provenance (not just a header)
- Downstream consumers need machine-readable detection
- You want interoperability with Adobe, Google, Microsoft, BBC ecosystems

Use simpler metadata (HTTP headers, JSON fields, HTML attributes) when:
- You generate text only
- Your output is API responses consumed by your own frontend
- You don't need tamper-evidence (trust boundary is your own system)
- You need a quick compliance win while implementing C2PA properly

## Python: Creating C2PA Manifests

```python
# c2pa_sign.py
# pip install c2pa-python
import json
from c2pa import Builder, SigningAlg, create_signer

# 1. Define the manifest
manifest_json = json.dumps({
    "claim_generator": "YourApp/1.0",
    "title": "AI-Generated Image",
    "assertions": [
        {
            "label": "c2pa.actions",
            "data": {
                "actions": [
                    {
                        "action": "c2pa.created",
                        "digitalSourceType":
                            "http://cv.iptc.org/newscodes/digitalsourcetype/trainedAlgorithmicMedia",
                        "softwareAgent": "YourApp AI Image Generator/1.0"
                    }
                ]
            }
        },
        {
            "label": "c2pa.ai_generated",
            "data": {
                "ai_generated": True,
                "model": "stable-diffusion-xl",
                "provider": "YourCompany",
                "prompt_used": True
            }
        }
    ]
})

def sign_ai_content(input_path: str, output_path: str, cert_path: str, key_path: str) -> None:
    """Sign an AI-generated file with C2PA manifest."""
    with open(cert_path, "rb") as f:
        cert_bytes = f.read()
    with open(key_path, "rb") as f:
        key_bytes = f.read()

    signer = create_signer(cert_bytes, key_bytes, SigningAlg.PS256, "http://timestamp.digicert.com")

    builder = Builder(manifest_json)
    builder.sign_file(signer, input_path, output_path)
    print(f"Signed: {output_path}")


def verify_c2pa_manifest(file_path: str) -> dict | None:
    """Read and verify C2PA manifest from a file."""
    from c2pa import Reader

    try:
        reader = Reader.from_file(file_path)
        manifest_store = json.loads(reader.json())
        active = manifest_store.get("active_manifest")
        if active:
            manifest = manifest_store["manifests"].get(active)
            return manifest
        return None
    except Exception as e:
        print(f"No valid C2PA manifest found: {e}")
        return None


if __name__ == "__main__":
    sign_ai_content(
        input_path="input.jpg",
        output_path="output_signed.jpg",
        cert_path="certs/cert.pem",
        key_path="certs/key.pem",
    )

    manifest = verify_c2pa_manifest("output_signed.jpg")
    if manifest:
        print(json.dumps(manifest, indent=2))
```

## Node.js: Creating C2PA Manifests

```typescript
// c2pa-sign.ts
// npm install c2pa-node
import { createC2pa, SigningAlg } from "c2pa-node";
import { readFileSync } from "fs";

const manifest = {
  claim_generator: "YourApp/1.0",
  title: "AI-Generated Image",
  assertions: [
    {
      label: "c2pa.actions",
      data: {
        actions: [
          {
            action: "c2pa.created",
            digitalSourceType:
              "http://cv.iptc.org/newscodes/digitalsourcetype/trainedAlgorithmicMedia",
            softwareAgent: "YourApp AI Image Generator/1.0",
          },
        ],
      },
    },
    {
      label: "c2pa.ai_generated",
      data: {
        ai_generated: true,
        model: "dall-e-3",
        provider: "YourCompany",
        prompt_used: true,
      },
    },
  ],
};

async function signAIContent(
  inputPath: string,
  outputPath: string,
  certPath: string,
  keyPath: string
): Promise<void> {
  const c2pa = createC2pa();

  const cert = readFileSync(certPath);
  const key = readFileSync(keyPath);

  const signer = {
    type: "local" as const,
    certificate: cert,
    privateKey: key,
    algorithm: SigningAlg.PS256,
    tsaUrl: "http://timestamp.digicert.com",
  };

  const { signedAsset } = await c2pa.sign({
    asset: { path: inputPath },
    manifest,
    signer,
    outputPath,
  });

  console.log(`Signed: ${outputPath} (${signedAsset.mimeType})`);
}

async function verifyC2paManifest(
  filePath: string
): Promise<Record<string, unknown> | null> {
  const c2pa = createC2pa();

  try {
    const result = await c2pa.read({ path: filePath });
    if (!result) return null;

    const activeManifest = result.active_manifest;
    return activeManifest ? (result.manifests[activeManifest] ?? null) : null;
  } catch (err) {
    console.error(`No valid C2PA manifest found: ${err}`);
    return null;
  }
}

// Usage
signAIContent("input.png", "output_signed.png", "certs/cert.pem", "certs/key.pem");
```

## C2PA Manifest Structure Explained

```json
{
  "claim_generator": "YourApp/1.0",
  "title": "AI-Generated Image",

  "assertions": [
    {
      "label": "c2pa.actions",
      "data": {
        "actions": [
          {
            "action": "c2pa.created",
            "digitalSourceType": "http://cv.iptc.org/newscodes/digitalsourcetype/trainedAlgorithmicMedia",
            "softwareAgent": "YourApp AI Generator/1.0"
          }
        ]
      }
    }
  ]
}
```

Key fields for AI Act compliance:
- **claim_generator**: identifies your application (the deployer/provider)
- **action**: `c2pa.created` for new AI content, `c2pa.edited` for AI-modified content
- **digitalSourceType**: the IPTC code `trainedAlgorithmicMedia` means "AI generated"
- **softwareAgent**: the specific tool/model that generated the content

## Cloud Storage Integration: S3 Upload Hook

```python
# s2pa_s3_hook.py
# Sign AI-generated content with C2PA before uploading to S3.
import json
import tempfile
from pathlib import Path
import boto3
from c2pa import Builder, SigningAlg, create_signer


def upload_ai_content_with_c2pa(
    local_path: str,
    bucket: str,
    s3_key: str,
    cert_path: str,
    key_path: str,
    ai_model: str,
    ai_provider: str,
) -> str:
    """Sign file with C2PA manifest, then upload to S3."""
    manifest_json = json.dumps({
        "claim_generator": f"{ai_provider}/1.0",
        "title": Path(local_path).name,
        "assertions": [
            {
                "label": "c2pa.actions",
                "data": {
                    "actions": [
                        {
                            "action": "c2pa.created",
                            "digitalSourceType":
                                "http://cv.iptc.org/newscodes/digitalsourcetype/trainedAlgorithmicMedia",
                            "softwareAgent": f"{ai_provider} {ai_model}",
                        }
                    ]
                }
            }
        ]
    })

    with open(cert_path, "rb") as f:
        cert_bytes = f.read()
    with open(key_path, "rb") as f:
        key_bytes = f.read()

    signer = create_signer(cert_bytes, key_bytes, SigningAlg.PS256, "http://timestamp.digicert.com")

    with tempfile.NamedTemporaryFile(suffix=Path(local_path).suffix, delete=False) as tmp:
        signed_path = tmp.name

    builder = Builder(manifest_json)
    builder.sign_file(signer, local_path, signed_path)

    s3 = boto3.client("s3")
    s3.upload_file(signed_path, bucket, s3_key, ExtraArgs={
        "Metadata": {
            "ai-generated": "true",
            "ai-model": ai_model,
            "c2pa-signed": "true",
        }
    })

    Path(signed_path).unlink()
    return f"s3://{bucket}/{s3_key}"
```

## Limitations and Current State

Things to know before you commit to C2PA:

1. **Format support**: Works well with JPEG, PNG, TIFF, MP4, WAV. PDF and WebP support is
   improving. SVG and plain text are not supported — use metadata approaches for those.

2. **Stripping risk**: Social media platforms and CDNs may strip C2PA metadata during
   transcoding. The C2PA spec includes "soft binding" (perceptual hashes) to help, but
   this is not foolproof.

3. **Certificate management**: You need a real code-signing certificate from a CA in the
   C2PA trust list. Self-signed certs work for development but won't validate in
   production verifiers.

4. **Performance**: Signing adds latency (100-500ms per file depending on size). For
   real-time applications, consider signing asynchronously after generation.

5. **Verification ecosystem**: Adobe Photoshop, Lightroom, and Content Authenticity
   verify.contentauthenticity.org can read C2PA manifests. Browser-native support is
   still in development.

6. **Not a DRM system**: C2PA proves provenance, it doesn't prevent copying or misuse.
   It's a transparency tool, not an access control mechanism.
