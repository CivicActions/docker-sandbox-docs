# Docker Sandbox Documentation
Documenting docker based developer sandboxes

## Table of Contents

## Managing Ports

Sometimes containers don't start on a `docker-compose up -d` and it wasn't clear why. Check that the ports the project is requesting (likely in docker-compose.yml and likely port 80) are not already in use by something else such as apache.

## Contributing

We value concise documentation over completeness.
Please feel free to submit pull requests.
