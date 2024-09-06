# minimal reproduction for my issue with github-release-attachments

I run locally in the directory of this cloned repository the following command

    podman run -it --rm --env-file=.env -v $(pwd):/usr/src/app docker.io/renovate/renovate:latest --dry-run --platform=local

Local `.env` file only contains

    LOG_LEVEL=debug
    GITHUB_COM_TOKEN=lalala

## Current behavior

Renovate seems to detect everything correctly but it does not look up the new version of adoptium/temurin8-binary 8u422b05.

Log output

    DEBUG: Checking packageFiles for deprecated packages (repository=local)
       "packageFiles": {
         "regex": [
           {
             "deps": [
               {
                 "depName": "adoptium/temurin8-binaries",
                 "currentValue": "8u412b08",
                 "datasource": "github-release-attachments",
                 "replaceString": "OpenJDK8U-jdk_x64_linux_hotspot_8u412b08.tar.gz",
                 "updates": [],
                 "packageName": "adoptium/temurin8-binaries",
                 "versioning": "semver-coerced",
                 "warnings": [],
                 "sourceUrl": "https://github.com/adoptium/temurin8-binaries",
                 "registryUrl": "https://github.com",
                 "currentVersion": "8u412b08",
                 "currentVersionTimestamp": "2024-09-02T20:03:27.000Z",
                 "fixedVersion": "8u412b08"
               },
               {
                 "depName": "adoptium/temurin11-binaries",
                 "currentValue": "11.0.24_8",
                 "datasource": "github-release-attachments",
                 "replaceString": "OpenJDK11U-jdk_x64_linux_hotspot_11.0.24_8.tar.gz",
                 "updates": [],
                 "packageName": "adoptium/temurin11-binaries",
                 "versioning": "semver-coerced",
                 "warnings": [],
                 "sourceUrl": "https://github.com/adoptium/temurin11-binaries",
                 "registryUrl": "https://github.com",
                 "currentVersion": "11.0.24_8",
                 "currentVersionTimestamp": "2024-07-17T21:00:29.000Z",
                 "fixedVersion": "11.0.24_8"
               }
             ],
             "matchStrings": [
               "OpenJDK(?<major>[0-9]+)U-jdk_x64_linux_hotspot_(?<currentValue>[0-9a-z\\._]*)\\.tar\\.gz"
             ],
             "depNameTemplate": "adoptium/temurin{{{major}}}-binaries",
             "datasourceTemplate": "github-release-attachments",
             "packageFile": "Temurin.kt"
           }
         ]
       }

Everything like depName, currentValue, datasource, sourceUrl is detected correctly but no new versions are looked up.

## Expected behavior

Renovate notifies me about new adoptium/temurin8-binaries version 8u422b05.

## Link to the Renovate issue or Discussion

[Link to discussion](https://github.com/renovatebot/renovate/discussions/31249)
