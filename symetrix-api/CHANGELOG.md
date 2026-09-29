# Change Log

All notable changes to the "symetrix-api" extension will be documented in this file.

## [1.3.0]

- Updated snippets to cover the full Cognio Lua API (3rd Party Lua Control Drivers). All existing prefixes still work.
- Added System snippets: version properties, IsEmulating, IsDebugging, ClearDebugging, GetTime, GetExecutionTime.
- Added new Cognio NamedControl functions: ModifyValue, GetChanged, SubscribeText, EventHandler, GetProperty, SetProperty, plus subscription and polling frameworks.
- Added new Cognio Device functions: GetLastRecalledPreset, RecallPreset, and an IP-ready framework.
- Added UdpSocket multicast: MulticastTtl, MulticastLoop, JoinMulticast, and a multicast framework.
- Added missing TcpSocket, SSH and Timer members: ID, timeouts, BufferLength, per-event callbacks, Events and EOL enumerations, Start/Stop, and EventHandler/key-auth frameworks.
- Added `json.require` (`json = require("json")`) and a TCP Driver Framework template.
- Snippets now use tab-stop placeholders, and ReadLine/Events/property arguments offer a list of valid values.
- Fixed snippets that inserted invalid Lua (for example `[delimiter]` arguments and `Timeout = "number"`), and removed `ReadTimeout` from the SSH Framework because the SSH API doesn't have it.

## [1.2.0]

- Added SSH.

## [1.1.3]

- Added Tapstop.

## [1.0.7]

- Updated README.

## [1.0.0]

- Initial release of Symetrix API Snippets.
