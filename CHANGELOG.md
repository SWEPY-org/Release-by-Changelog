# Changelog

All notable changes to this job will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.4.4] - 2024-07-16

* Doc about supported domains (gitlab.com and froggit.fr)
* Version of gitlab release-cli now fixed

## [0.4.3] - 2024-06-26

### Fixed

* Default stage now set to `deploy`

## [0.4.2] - 2024-06-10

### Fixed

* Include remote template example 

## [0.4.1] - 2024-05-12

* More documentation

## [0.4.0] - 2024-05-12

* More documentation

### Added

* Prefix and suffix to tag and release name

## [0.3.4] - 2024-05-12

* Better documentation

## [0.3.3] - 2024-05-12

### Fixed

* Present day release are not considered as "historical" anymore

## [0.3.2] - 2024-05-12

### Fixed

* R2 template path now pointing to the correct folder
* When no text is found in the version description, the description is not the following
  header anymore

## [0.3.1] - 2024-05-12

### Fixed

* Template path now pointing to the correct folder

## [0.3.0] - 2024-05-12

### Changed

* Do not require Python, use release-cli

### Removed

* venv job

## [0.2.4] - 2024-05-08

### Fixed

* release-by-changelog-venv job now only runs on tags

## [0.2.3] - 2024-05-06

### Fixed

* Job name is now set to `release_by_changelog`

## [0.2.2] - 2024-05-06

### Changed

* `release-by-changelog` venv will now run only on default branch except if configured
  otherwise

## [0.2.1] - 2024-05-06

### Fixed

* venv job name is fixed

## [0.2.0] - 2024-05-06

### Changed

* Pipeline will now run only on default branch except if configured otherwise

## [0.1.1] - 2024-05-06

### Changed

* Fix documentation links

## [0.1.0] - 2024-05-05

* Initial version
