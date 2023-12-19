# Integrating CycloneDX in a Gradle Project for SBOM Generation and Scanning

This repository demonstrates how to integrate the CycloneDX plugin into a Gradle project, generate a Software Bill of Materials (SBOM) using Syft, scan the SBOM, and import the SBOM file and scan results into a pipeline.

*For detailed insights on SBOM with maven projects and its importance, refer to our [SBOM 101 blog](https://kondukto.io/blog/sbom-software-bill-of-materials).*

*To view the related blog post for this repository, please visit [this link](https://kondukto.io/blog/how-to-generate-and-audit-sbom-in-a-ci-cd-pipeline).*

## Adding CycloneDX Plugin to Gradle

### For Groovy DSL (`build.gradle`):

Add the following to your `build.gradle`:

```groovy
plugins {
    id 'org.cyclonedx.bom' version 'x.y.z'
}
```

Replace `x.y.z` with the desired version of the CycloneDX plugin.

### For Kotlin DSL (`build.gradle.kts`):

Add the following to your `build.gradle.kts`:

```kotlin
plugins {
    id("org.cyclonedx.bom") version "x.y.z"
}
```
*To view the CycloneDX plugins gradle, please visit [this link]([https://kondukto.io/blog/how-to-generate-and-audit-sbom-in-a-ci-cd-pipeline](https://plugins.gradle.org/plugin/org.cyclonedx.bom)).*



## Generating SBOM with Syft

After integrating CycloneDX, generate the SBOM using Syft:

```bash
syft  sbom-gradle-cyclonedx-pipeline-scan -o cyclonedx-json --file kotlin-sbom.json
```

This command creates an SBOM in CycloneDX JSON format.

## Scanning SBOM with osv-scanner

To scan the generated SBOM with osv-scanner, execute:

```bash
osv-scanner -S gradle-sbom.json --json --output result.json
```


## Importing SBOM and Scan Results into a Pipeline

To automate the process of generating, scanning, and importing SBOM in a pipeline:

1. **Pipeline Configuration**: Set up your pipeline (e.g., GitHub Actions, Jenkins) to include steps for running CycloneDX, Syft, and osv-scanner.

2. **Pipeline Script**: Create a script or a set of commands in your pipeline configuration to execute the CycloneDX plugin, Syft, and osv-scanner sequentially.

3. **Execution**: Run your pipeline to automate the generation and scanning of the SBOM, and to import the results.

---
