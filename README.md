# NovaEco Releases

This repository is the central, authoritative source for all stable, ecosystem-wide releases.

This is a **"tag-only"** repository. It contains no source code. Its sole purpose is to host Git tags that correspond to a specific "Ecosystem Release."

## Release Strategy: CalVer + SemVer

Our ecosystem uses a hybrid versioning strategy:

1.  **Semantic Versioning (SemVer) (e.g., `novahub-v1.5.0`)**
      * **Where:** Used for individual artifacts (e.g., `novahub-api.tar.gz`) in each `novaeco-tech` enabler/sector/worker/product repository.
      * **Purpose:** Tracks the independent development and features of each microservice.

2.  **Calendar Versioning (CalVer) (e.g., `v2025.11.14`)**
      * **Where:** Used *only* in this `ecosystem-releases` repository.
      * **Purpose:** Represents a "snapshot" of the entire ecosystem, composed of a list of SemVer artifacts that have been tested and are confirmed to work together.

## Release Workflow: The "Bill of Materials"

A "Release" in this repository is a **CalVer Git tag** (e.g., `v2025.11.14`) that contains a `release-manifest.json` file in its body.

This manifest is the "bill of materials" that tells the downstream deployment system *exactly* which artifact versions to assemble and deploy.

### **Manual Release Process (For Release Managers)**

Publishing a new release is a **manual, human-gated** action that triggers the production deployment.

1.  **Verify Stable Artifacts:** Go to the `novaeco-tech/ecosystem-qa` repository and identify the set of "Stable" (promoted from pre-release) artifact tags you want to include in this new ecosystem release.

2.  **Create the Manifest:** Create a `release-manifest.json` file on your local machine. This file lists the *exact* Git tag for each artifact to be deployed.

3.  **Draft a New Release:**
      * Go to the "Releases" page of *this* (`ecosystem-releases`) repository.
      * Click "Draft a new release."
      * In the "Choose a tag" box, type a **new CalVer tag** (e.g., `v2025.11.14`). Click "Create new tag on publish."
      * Set the "Release title" to the same tag (e.g., `v2025.11.14`).
      * In the release body, paste the entire contents of your `release-manifest.json` file, wrapped in a JSON code block.

4.  **Publish the Release:**
      * Review the manifest one last time.
      * Click **"Publish release"**.

### Automation (What happens next?)

Clicking "Publish" triggers two parallel workflows:
1.  **Validation (`validate-release.yml`):** Ensures your JSON syntax is correct and required fields are present.
2.  **Signaling (`signal-operations.yml`):** Sends a secure, blind dispatch event to the commercial operator (`circular-engineering`) to begin the production deployment.

### Example: `release-manifest.json`

This is the content you would paste into the body of the GitHub Release.

```json
{
  "version": "v2025.11.14",
  "description": "November stable release. Includes new NovaHub search and NovaFin staking features.",
  "artifacts": {
    "ecosystem-core-api": "ecosystem-core-api-v1.2.1",
    "ecosystem-core-app": "ecosystem-core-app-v1.2.5",
    "ecosystem-core-auth": "ecosystem-core-auth-v1.2.1",
    "ecosystem-core-website": "ecosystem-core-website-v1.2.4",
    
    "novahub-api": "novahub-api-v1.5.1",
    "novahub-app": "novahub-app-v1.5.5",
    "novahub-website": "novahub-website-v1.5.2",
    
    "novafin-api": "novafin-api-v1.4.2",
    "novafin-app": "novafin-app-v1.4.5",
    "novafin-website": "novafin-website-v1.4.2",
    
    "novabalance-worker-air": "novabalance-worker-air-v1.0.1",
    
    "product-duras-agv-api": "product-duras-agv-api-v1.1.1",
    "product-duras-agv-app": "product-duras-agv-app-v1.1.5",
    "product-duras-agv-website": "product-duras-agv-website-v1.1.7"
  }
}