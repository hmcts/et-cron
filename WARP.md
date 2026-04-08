# ET Cron - Warp Instructions

## Overview
This repo contains the Helm chart for the ET Kubernetes cron job (`et-cron`). It schedules tasks by passing `run [taskname]` arguments to the [et-ccd-callbacks](https://github.com/hmcts/et-ccd-callbacks) jar image.

## Prerequisites
- `helm` CLI installed
- `kubectl` configured
- `az` (Azure CLI) installed and authenticated

## Makefile Targets

### `make setup`
Configures your local environment to connect to the HMCTS production ACR and AKS cluster.
- Sets the Azure subscription to `DCD-CFTAPPS-PROD`
- Configures the default ACR to `hmctsprod`
- Adds the ACR Helm repo
- Fetches AKS credentials for `cnp-aks-cluster` in `cnp-aks-rg`

> Run this once before any deploy/test steps if your credentials are not already set up.

### `make lint`
Lints the Helm chart against `ci-values.yaml`:
```
helm lint et-cron -f ci-values.yaml
```

### `make deploy`
Installs the Helm chart into the `chart-tests` namespace and waits up to 60 seconds for it to be ready.

### `make dry-run`
Performs a dry-run install with debug output — useful for previewing rendered templates without deploying.

### `make test`
Runs Helm tests against the deployed release (`chart-et-cron-release`).

### `make clean`
Removes the Helm release and deletes the test pod from the `chart-tests` namespace.

### `make all` (default)
Runs the full pipeline in order: `setup → clean → lint → deploy → test`

## Common Workflows

**Full local test run:**
```
make all
```

**Lint only (no cluster access needed):**
```
make lint
```

**Iterative development (skip setup if already configured):**
```
make clean && make deploy && make test
```

**Preview rendered Helm templates:**
```
make dry-run
```
