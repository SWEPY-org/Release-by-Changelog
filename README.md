# Release By Changelog

![10 seconds](https://img.shields.io/badge/10_seconds-green) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://lab.frogg.it/swepy/cicd-templates/release-by-changelog/-/blob/main/LICENSE) [![Supported by GitLab.com](https://img.shields.io/badge/Supported_by-GitLab.com-orange)](https://gitlab.com) [![Supported by Frogg.it](https://img.shields.io/badge/Supported_by-Frogg.it-green)](https://froggit.fr/)


## Goal

Publish a new release based on the content of the `CHANGELOG.md` file in less than 10 seconds. The file must follow the [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format and each release must adhere to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## How to use it

Add the following to your `.gitlab-ci.yml` file:

### For gitlab.com and mirrored instance

```yaml
include:
  - component: $CI_SERVER_FQDN/swepy/cicd-templates/release-by-changelog/release-by-changelog@1.0.0
```

> ⚠️ On gitlab <16.10, use `$CI_SERVER_FQDN:$CI_SERVER_PORT` instead of `$CI_SERVER_FQDN`.

When referencing a CI/CD catalog component, you can use a special format to specify the latest semantic version in a range. [Read more about Semantic version ranges](https://docs.gitlab.com/ee/ci/components/#semantic-version-ranges).


[![Supported by GitLab.com](https://img.shields.io/badge/Supported_by-GitLab.com-orange)](https://gitlab.com) [![Supported by Frogg.it](https://img.shields.io/badge/Supported_by-Frogg.it-green)](https://froggit.fr/)

### Self-hosted instance

For self-hosted instances, you need to import the component as a remote template.

```yaml
include:
  - remote: 'https://gitlab.com/swepy/cicd-templates/release-by-changelog/-/raw/1.0.0/templates/release-by-changelog.yml'
```

If you want to use semantic version ranges, you need to do a [mirror](https://docs.gitlab.com/ee/user/project/repository/mirror/pull.html) of the repository and rely on the component include.

### Customize

You can configure the component/template using [inputs](https://docs.gitlab.com/ee/ci/yaml/inputs.html). 

Available inputs:

| Name                  | Description                                   | Default        |
|-----------------------|-----------------------------------------------|----------------|
| `stage`               | The stage of the job.                         | `deploy`       |
| `changelog file path` | The path to the `CHANGELOG.md` file.          | `CHANGELOG.md` |
| `suffig`              | Value to prepend to the tag and release name. | `""`           |
| `prefix`              | Value to append to the tag and release name.  | `""`           |

Example of configuration with local component:

```yaml
include:
  - component: $CI_SERVER_HOST/swepy/cicd-templates/release-by-changelog/release-by-changelog@1.0.0
    inputs:
      stage: release
      prefix: version-
```

Example of configuration with remote template:

```yaml
include:
  - remote: 'https://gitlab.com/swepy/cicd-templates/release-by-changelog/-/raw/1.0.0/templates/release-by-changelog.yml'
    inputs:
      stage: release
      prefix: version-
```

#### Further configuration

Using variables, you have access to more granular configuration. Example:

```yaml
include:
  - component: $CI_SERVER_FQDN/swepy/cicd-templates/release-by-changelog/release-by-changelog@1.0.0

release-by-changelog:
  variables:
    TAG_PREFIX: "v"
    NAME_PREFIX: "Version: "
```

Available variables:

| Name                 | Description                                   | Default     |
| -------------------- | --------------------------------------------- | ----------- |
| `CHANGELOG_FILEPATH` | The path to the `CHANGELOG.md` file.          | from inputs |
| `PREFIX`             | Value to prepend to the tag and release name. | from inputs |
| `SUFFIX`             | Value to append to the tag and release name.  | from inputs |
| `TAG_PREFIX`         | Value to prepend to the tag.                  | `$PREFIX`   |
| `TAG_SUFFIX`         | Value to append to the tag.                   | `$SUFFIX`   |
| `NAME_PREFIX`        | Value to prepend to the release name.         | `$PREFIX`   |
| `NAME_SUFFIX`        | Value to append to the release name.          | `$SUFFIX`   |

## About `CHANGELOG.md`

### Unreleased changes

The `CHANGELOG.md` file may have an `Unreleased` section at the top of the file. This section is used to keep track of changes that are not yet released and will be ignored by `release-by-changelog`.

Example:

```markdown
# Changelog

## [Unreleased]

* Add new feature

## [1.0.0] - 2020-01-01

* First release
```

#### Bump the version

When the release is ready, the `Unreleased` title must be updated to the new version and date, following the following format: `## [{new_version}] - {now:%Y-%m-%d}`

##### Automation

If you are using [bump_my_version](https://pypi.org/project/bump-my-version/), you can automate the update of the `Unreleased` section. To do so, you need this configuration in your `.bumpversion.toml` or `pyproject.toml` file:

```toml
[[tool.bumpversion.files]]
filename = "CHANGELOG.md"
replace = """## [Unreleased]

## [{new_version}] - {now:%Y-%m-%d}
"""
search = """## [Unreleased]
"""
```

Then you can bump the version by running the following command:

```shell
bump-my-version bump <MAJOR|MINOR|PATCH>
```

You'll find a full example of the `bump_my_version` configuration [here](.bumpversion.toml).

### Upcoming and Historical releases

For each release, the version release date MUST be included (see [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)). This date is used to define the release date in the GitLab release. If the date is the same as the current date when the job runs, the release exact time is defined by gitlab. Otherwise, the release time is set to 00:00:00 UTC and the release will carry a badge as historical or upcoming.

* For upcoming releases, the badge will be removed when the release is published.
* For historical releases, the badge will remain, and release evidences won't be available.

See:

* [Upcoming releases](https://docs.gitlab.com/ee/user/project/releases/#upcoming-releases)
* [Historical releases](https://docs.gitlab.com/ee/user/project/releases/#historical-releases)

## Notes

Release by Changelog uses itself for its releases. This project is not related to the [CNRV](https://cnrv.info/) (yet).
