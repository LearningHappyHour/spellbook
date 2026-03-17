# my-content

Cortex Platform content packs repository.

## Overview

This repository contains Cortex Platform content packs built using GoCortex Spellbook.

## Structure

```
my-content/
|-- Packs/                  # Content packs
|   +-- SamplePack/         # Starter pack with examples
|       |-- pack_metadata.json
|       |-- README.md
|       |-- CorrelationRules/
|       |-- ParsingRules/
|       |-- ModelingRules/
|       |-- XSIAMDashboards/
|       +-- ReleaseNotes/
|-- artifacts/              # Built pack zip files
+-- spellbook.yaml          # Build configuration
```

## Building Packs

Build packs locally using Docker. The built zip files appear in the `artifacts/` directory.

```bash
# Build all packs (run from this directory)
docker run --rm -v $(pwd):/content \
  ghcr.io/gocortexio/spellbook:latest build --all

# Build a specific pack
docker run --rm -v $(pwd):/content \
  ghcr.io/gocortexio/spellbook:latest build SamplePack

# The zip files are created in artifacts/
ls artifacts/
```

## Creating a New Pack

```bash
docker run --rm -v $(pwd):/content \
  ghcr.io/gocortexio/spellbook:latest create MyNewPack --description "My new pack"
```

## Validating Packs

```bash
# Validate all packs
docker run --rm -v $(pwd):/content \
  ghcr.io/gocortexio/spellbook:latest validate-all

# Validate a specific pack
docker run --rm -v $(pwd):/content \
  ghcr.io/gocortexio/spellbook:latest validate SamplePack
```

## Uploading to Cortex Platform

Upload packs directly to your Cortex Platform tenant. Set the environment variables first,
then pass them through to Docker:

```bash
export DEMISTO_BASE_URL="https://your-instance.xdr.paloaltonetworks.com"
export DEMISTO_API_KEY="your-api-key"
export XSIAM_AUTH_ID="your-auth-id"

docker run --rm -v $(pwd):/content \
  -v ~/.gitconfig:/home/spellbook/.gitconfig:ro \
  -e DEMISTO_BASE_URL \
  -e DEMISTO_API_KEY \
  -e XSIAM_AUTH_ID \
  ghcr.io/gocortexio/spellbook:latest upload Packs/SamplePack --xsiam
```

## References

- Cortex Platform Content Pack Format: https://xsoar.pan.dev/docs/packs/packs-format
