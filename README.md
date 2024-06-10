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

As a remote Template (recommended):

```yaml
include:
    -   remote: 'https://gitlab.com/swepy/cicd-templates/release-by-changelog/-/raw/0.4.2/templates/release-by-changelog.yml'
```

As a local Template (if the template is local to the instance):

```yaml
include:
    -   project: 'swepy/cicd-templates/release-by-changelog'
        ref: '0.4.2'
        file: 'templates/release-by-changelog.yml'
```

As a Component ([beta](https://gitlab.com/gitlab-org/gitlab/-/issues/407556) and if the
component is local to the instance):

```yaml
include:
    -   component: $CI_SERVER_FQDN/swepy/cicd-templates/release-by-changelog/release-by-changelog@0.4.2
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

| Name                 | Description                                   | Default          |
|----------------------|-----------------------------------------------|------------------|
| `CHANGELOG_FILEPATH` | The path to the CHANGELOG.md file.            | `"CHANGELOG.md"` |
| `PREFIX`             | Value to prepend to the tag and release name. |                  |
| `SUFFIX`             | Value to append to the tag and release name.  |                  |
| `TAG_PREFIX`         | Value to prepend to the tag.                  | `$PREFIX`        |
| `TAG_SUFFIX`         | Value to append to the tag.                   | `$SUFFIX`        |
| `NAME_PREFIX`        | Value to prepend to the release name.         | `$PREFIX`        |
| `NAME_SUFFIX`        | Value to append to the release name.          | `$SUFFIX`        |

## About `CHANGELOG.md`

### Unreleased changes

The `CHANGELOG.md` file may have an `Unreleased` section at the top of the file.
This section is used to keep track of changes that are not yet released.

Example:

```markdown
# Changelog

## [Unreleased]

* Add new feature

## [1.0.0] - 2020-01-01

* First release
```

#### Bump the version

When the release is ready, the `Unreleased` section must be moved to a new version
section and the version number must be bumped.

If you are using [bump_my_version](https://pypi.org/project/bump-my-version/), you can
automate the update of the `Unreleased` section.

To do so, you need this configuration in your `pyproject.toml` file:

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
bump_my_version bump <MAJOR|MINOR|PATCH>
```

You'll find a full example of the `bump_my_version`
configuration [here](pyproject.toml).

### Upcoming and Historical releases

For each release, the version release date MUST be included
(see [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)). This date is used
to define the release date in the GitLab release. If the date is the same as the
current date when the job runs, the release exact time is defined by gitlab. Otherwise,
the release time is set to 00:00:00 UTC and the release will carry a badge as historical
or upcoming.

* For upcoming releases, the badge will be removed when the release is published.
* For historical releases, the badge will remain, and release evidences won't be
  available.

See:

* [Upcoming releases](https://docs.gitlab.com/ee/user/project/releases/#upcoming-releases)
* [Historical releases](https://docs.gitlab.com/ee/user/project/releases/#historical-releases)
