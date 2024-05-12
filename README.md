# Release By Changelog template

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://lab.frogg.it/swepy/cicd-templates/release-by-changelog/-/blob/main/LICENSE)

## Objective

Publish a new release based on the content of the `CHANGELOG.md` file.
The file must follow the [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)
format and each release must adhere
to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## How to use it

### Include the component/template

Add the following to your `.gitlab-ci.yml` file.

As a Template:

```yaml
include:
    -   project: 'swepy/cicd-templates/release-by-changelog'
        ref: '0.3.4'
        file: 'templates/release-by-changelog.yml'
```

As a Component:

```yaml
# As a Component
include:
    -   component: $CI_SERVER_FQDN/swepy/cicd-templates/release-by-changelog/release-by-changelog@0.3.4
```

### Customize job

You can customize the job by overriding specific keys. For example:

```yaml
release-by-changelog:
    stage: release
    variables:
        CHANGELOG_FILEPATH: "docs/CHANGELOG.md"
```

## Variables

You can customize the job by overriding the following variables:

| Name                 | Description                        | Default          |
|----------------------|------------------------------------|------------------|
| `CHANGELOG_FILEPATH` | The path to the CHANGELOG.md file. | `"CHANGELOG.md"` |
