# Product requirements

Status: Draft for the first public prerelease

## Purpose

Libre LUCI enables Home Assistant users to monitor and control compatible Libre
Wireless streamers over the local network without a cloud dependency.

## Goals

- Provide a safe, UI-configurable Home Assistant integration.
- Represent each configured endpoint as a media-player device.
- Recover predictably from network and device interruptions.
- Keep protocol support testable without requiring Home Assistant or physical
  hardware for every test.
- Package releases for straightforward installation through HACS.

## Functional requirements

- **REQ-CONF-001:** A user can configure a hostname or IP address and TCP port through
  Home Assistant's integration UI.
- **REQ-CONF-002:** Duplicate endpoints are rejected.
- **REQ-CONN-001:** The integration communicates over the framed LUCI TCP protocol.
- **REQ-CONN-002:** Connection attempts and writes are bounded by timeouts.
- **REQ-CONN-003:** A dropped connection makes the entity unavailable and is retried
  without requiring a Home Assistant restart.
- **REQ-STATE-001:** Valid playback status, volume, source, device name, and elapsed
  position updates are reflected in Home Assistant.
- **REQ-STATE-002:** Malformed, unsupported, or out-of-range device values are ignored
  safely.
- **REQ-CTRL-001:** The media player supports play, pause/resume, stop, next, previous,
  seek, and volume changes when connected.
- **REQ-SAFE-001:** Only explicitly supported commands are sent. Arbitrary raw LUCI
  commands are outside the public interface.
- **REQ-LIFE-001:** Unloading or reloading the config entry closes tasks and sockets.

## Non-functional requirements

- **REQ-NFR-001:** Network operations must not block Home Assistant's event loop.
- **REQ-NFR-002:** Protocol behavior must have deterministic tests for fragmented and
  concatenated frames, invalid frames, and boundary values.
- **REQ-NFR-003:** CI must run linting, formatting checks, tests, HACS validation, and
  Home Assistant manifest validation.
- **REQ-NFR-004:** Logs must not expose secrets or unnecessary device-identifying
  information.
- **REQ-NFR-005:** User-facing strings must be translatable.

## Explicit non-goals for the first stable release

- Cloud control or telemetry.
- TLS added on top of device protocols that do not natively support it.
- Arbitrary raw-command execution.
- Multiroom grouping or topology management.
- Automatic model heuristics without validated protocol evidence.
- Network discovery until a reliable, device-supported mechanism is documented.

## Release acceptance criteria

The first stable release requires all requirements above to be implemented and
tested, protocol behavior to be validated on at least one representative device,
installation documentation to be verified from a clean Home Assistant environment,
and no unresolved release-blocking issues.

