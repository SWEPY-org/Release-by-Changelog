# Release By Changelog template

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://lab.frogg.it/swepy/cicd-templates/release-by-changelog/-/blob/main/LICENSE)

## Objective

Run release_by_changelog on your project.

## How to use it

1. Include the release_by_changelog template in your GitLab CI/CD configuration.
2. If you need to customize the job, refer to
   the [jobs customization](https://docs.r2devops.io/get-started/use-templates/#job-templates-customization)
   documentation.

## Variables

| Name                   | Description                              | Default                    |
|------------------------|------------------------------------------|----------------------------|
| `IMAGE_NAME`           | The default name for the docker image.   | `"python"`                 |
| `IMAGE_TAG`            | The default tag for the docker image.    | `"latest"`                 |
| `IMAGE`                | The default docker image name.           | `"$IMAGE_NAME:$IMAGE_TAG"` |
| `PROJECT_PATH`         | The path to the project root directory.  | `"."`                      |
| `RELEASE_BY_CHANGELOG` | The command to run release_by_changelog. | `"release_by_changelog"`   |
