
# Integrating CycloneDX in a Gradle Project for SBOM Generation and Scanning


The Software Bill of Materials (SBOM) is essential in cybersecurity, offering detailed insights into all components of a software build. This includes not only the primary software but also third-party and transitive dependencies. SBOMs play a crucial role in identifying hidden risks and addressing potential security threats.

*For insights on SBOM with maven projects and its importance, refer to our [SBOM 101 blog](https://kondukto.io/blog/sbom-software-bill-of-materials).*

CycloneDX is an open-source initiative that focuses on creating a standardized format for SBOMs, enhancing the security of software supply chains. It simplifies the process of generating SBOMs, allowing for a more thorough assessment of vulnerabilities in dependencies. This project demonstrates the use of CycloneDX with Gradle plugins to create SBOMs for a build.gradle.kts file.

*To view the related blog post for this repository, please visit [this link](https://kondukto.io/blog/how-to-generate-and-audit-sbom-in-a-ci-cd-pipeline).*

## Adding CycloneDX Plugin to Gradle

### For Groovy (`build.gradle`):

Add the following to your `build.gradle`:

```groovy
plugins {
    id 'org.cyclonedx.bom' version 'x.y.z'
}
```

Replace `x.y.z` with the desired version of the CycloneDX plugin.

### For Kotlin (`build.gradle.kts`):

Add the following to your `build.gradle.kts`:

```kotlin
plugins {
    id("org.cyclonedx.bom") version "x.y.z"
}
```
*To check CycloneDX plugin on gradle, you can have a look at [this link](https://plugins.gradle.org/plugin/org.cyclonedx.bom).*

![CycloneDX Integration Example](/assets/cycloneDXplugin.png)


## Generating SBOM on build process

After integrating CycloneDX, we use 'gradle cyclonedxBom' command to generate the SBOM:

```bash
gradle cyclonedxBom
```

This command creates an SBOM in CycloneDX JSON format on the directory mentioned in the tasks of the plugin inside build.gradle.kts.

## Scanning SBOM with osv-scanner

OSV-scanner, a CLI tool, checks for open-source vulnerabilities in SBOM files. To scan your SBOM and find vulnerabilities, use:

```bash
osv-scanner -S gradle-sbom.json --json --output result.json
```



## Importing SBOM and Scan Results into a Pipeline

Kondukto, an application security coordination and orchestration tool, streamlines vulnerability management. Utilize Kondukto's kdt CLI tool to import vulnerabilities and scan results into your pipeline, thereby enhancing cybersecurity management efficiency.

![Pipeline Example](/assets/pipeline.png)

---
