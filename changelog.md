# Changelog

All notable changes to this project will be documented in this file.

<!--
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).
-->

## [Release 3]

### Added

- Simulation of an original PET2001

- Diagnostic dongles for the user port and keyboard to be used with the Diagnostic ROM/Clip.

- Simulation of the Commodore Diagnostic Clip (6502-DIAG-Clip.dig)

- User port connector

### Changed

- There are now two mainboard files:
  - Mainboard-CBM3032.dig
  - Mainboard-PET2001-4.dig

  for the two simulated systems.

- Monitor.dig changed to
  - CRT-green.dig and
  - CRT-white.dig

- `PETComponentsDigitalPlugin.jar` upgraded to 1.0.1 (fixed errors in 6520 and 6522 simulations)

- README.md updated

### Fixed

- 74LS165 circuit [issue](https://github.com/hneemann/Digital/issues/1434).

- Mainboard-CBM3032.dig: "Write Protect" ROM to prevent simulation crash when writing to ROM (e.g by CBM Diagnostic ROM)

## [Release 2] - 2025-05-27

### Changed

- CRT Simulation now is green-on-black instead of white-on-black.

### Fixed

- Fixed the issue of randomly booting into TIM or BASIC. This can now be selected as required (default boot to BASIC)

- A new PETComponentsDigitalPlugin.jar is included, which fixes errors in the 6522 Timer to make the cassette tape write work.

## [Release 1] - 2025-05-23

First release.

Simulation is working with some known minor bugs.

<!--
Replace [1.0.0] and YYYY-MM-DD with your version and release date.
Add new versions above this line.
-->