# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.1] - 2019-10-24

### Changed

- Fixed resource saving

## [1.1.0] - 2019-10-24

### Changed

- Display the Notes field on update view
- Only allow the note creator to delete the note

## [1.0.2] - 2019-10-23

### Added

- Show only up to 5 notes initially with "show more" button to display all others

### Changed

- Improved sorting by adding note ID as tie-breaker in case multiple notes were created on the same second

## [1.0.1] - 2019-10-22

### Removed

- Removed `addActivity` method from `HasNotes` trait

## [1.0.0] - 2019-10-22

### Added

- Notes field on Detail view
- Differentiation between user-added and system-added notes
- Ability to add notes through the UI or programmatically
- Ability to delete user-made notes (w/ confirmation modal)
- Customizable placeholder support

[1.1.1]: https://github.com/optimistdigital/nova-notes-field/compare/1.1.0...1.1.1
[1.1.0]: https://github.com/optimistdigital/nova-notes-field/compare/1.0.2...1.1.0
[1.0.2]: https://github.com/optimistdigital/nova-notes-field/compare/1.0.1...1.0.2
[1.0.1]: https://github.com/optimistdigital/nova-notes-field/compare/1.0.0...1.0.1
[1.0.0]: https://github.com/optimistdigital/nova-notes-field/releases/tag/1.0.0
