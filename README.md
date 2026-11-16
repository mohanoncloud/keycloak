# Keycloak

[![Maven Package upon a push](https://github.com/mosip/keycloak/actions/workflows/push-trigger.yml/badge.svg?branch=release-1.3.x)](https://github.com/mosip/keycloak/actions/workflows/push-trigger.yml)

## Overview
Contains MOSIP customised keycloak image for IAM.  

## Documentation
To know more about Keycloack, refer [here](https://docs.mosip.io/1.2.0/modules/keycloak).

## Contribution & Community
- To learn how you can contribute code to this application, [click here](https://docs.mosip.io/1.2.0/community/code-contributions).
- If you have questions or encounter issues, visit the [MOSIP Community](https://community.mosip.io/) for support.
- For any GitHub issues: [Report here](https://github.com/mosip/keycloak/issues)

## Helm chart
The chart under `helm/` (keycloak-init) is published to GHCR as OCI chart by `.github/workflows/chart-lint-publish.yml`, which calls the shared `BHS-BS/shared-workflow` `helm-lint-publish.yml` workflow:
* A pull request that changes `helm/` lints the chart.
* When the pull request is merged into `develop` or a `release*` branch, the chart is published to `oci://ghcr.io/bhs-bs/charts/keycloak-init`. The `charts/` path keeps the charts apart from the images (`ghcr.io/bhs-bs/<image>`).
* A release version that is already published (e.g. `1.3.0`) is never overwritten: bump `version` in `Chart.yaml`. Pre-release versions (e.g. `0.0.1-develop`) are overwritten.
* The chart uses the `develop` image from GHCR (`ghcr.io/bhs-bs/keycloak-init`). The images are private: the cluster needs a `ghcr.io` pull secret.

Install a chart (needs a GitHub token with `read:packages`):
```
helm registry login ghcr.io -u <github-user>
helm install keycloak-init oci://ghcr.io/bhs-bs/charts/keycloak-init --version <version>
```

## License
This project is licensed under the terms of [Mozilla Public License 2.0](LICENSE).