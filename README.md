# Authorizer Server on Railway

A deployment wrapper that runs the upstream Authorizer auth server as a Docker image on Railway, with PostgreSQL and Redis options.

**Status:** Starter. The repo holds a short Dockerfile and a README for a Railway deploy template. It contains no application code, so the substance lives in the upstream Authorizer image.

## The problem

Running an authentication server means provisioning a database, configuring the server and keeping it updated. This repo packages Authorizer for one-click deployment on Railway so a team can start with a working instance and a managed database.

## What it does

- Pins the upstream `lakhansamani/authorizer` image at version 1.1.0 in the `Dockerfile`.
- Starts the server with `--database_type=postgres`, so the instance uses PostgreSQL.
- Documents a Railway deploy button that provisions the server, with PostgreSQL or MySQL and Redis as options.
- Points to the upstream docs for the environment variables that configure each instance.
- Explains how to upgrade an existing Railway deployment by changing the image tag in the Dockerfile.

## How it's built

- The whole repo is a Dockerfile that extends the upstream Authorizer image. There is no source code, package manifest or build step in this repo.
- Configuration is supplied at runtime through environment variables set in Railway, and the database type is set in the start command.
- Upgrades are a version bump in the Dockerfile, with the image coming from Docker Hub.

## What's left

- The repo has no tests, CI or health checks.
- The PostgreSQL template is the only database wired into this Dockerfile. The MySQL and Redis variants are described in the README but live in other repos or branches.
- The image is pinned to 1.1.0, which is older than the 1.1.30 pinned in the sibling `authorizer` repo, and needs a manual bump to upgrade.
- The README is an adapted copy of the upstream Railway template README, and some of its links point to other repositories.
