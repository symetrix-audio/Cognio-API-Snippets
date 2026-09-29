# Symetrix Cognio Lua API Snippets

Snippets for writing Cognio 3rd-party Lua control drivers and Control Panel Group scripts in VS Code. They cover every Cognio Lua API extension: Controls, NamedControl, Device, System, HttpClient, TcpSocket, UdpSocket, SSH, JSON and Timer.

Type a snippet prefix in a `.lua` file and pick it from IntelliSense. Press `Tab` to move between placeholders. Placeholders with a list (for example `TcpSocket.EOL`) show the allowed values.

Snippets ending in **Framework** insert a complete working pattern. The others insert a single API call or property.

For the full API reference, see the Cognio documentation: *Control > 3rd Party Lua Control Drivers > Lua API Extensions*.

## Timer

| Prefix | Description |
| ------ | ----------- |
| `Timer`<br>`Timer Framework` | Timer framework: callback function, Timer.New, EventHandler and Start. Timers run at most 4 Hz (0.25 s minimum). |
| `Timer.New` | Timer.New() - creates a new Timer object. Up to 8 timers per script. |
| `Timer.ID` | TimerName.ID - 1-8 index of the timer, assigned in order of creation. |
| `Timer.Start` | TimerName:Start(period) - starts the timer with a period in seconds (minimum 0.25). |
| `Timer.Stop` | TimerName:Stop() - stops the timer. It can be restarted with Start. |
| `Timer.EventHandler` | TimerName.EventHandler(TimerName) - callback run each time the timer completes. The timer object (with .ID) is passed in. |
| `Timer One-Shot`<br>`Timer Delay` | One-shot timer: runs the callback once after a delay, then stops itself. |
| `Timer Multiplier Framework`<br>`Timer Fast/Slow Framework` | One fast timer with a counter for slower work - more efficient than creating several timers. |

## Controls

| Prefix | Description |
| ------ | ----------- |
| `Controls.Inputs.Value` | Controls.Inputs[input].Value - reads the value on a control input pin (1-based, usually 0-1). |
| `Controls.Inputs.EventHandler` | Controls.Inputs[input].EventHandler - called when the signal on a control input pin changes (max 4 Hz). |
| `Controls.Outputs.Value` | Controls.Outputs[output].Value - writes a value to a control output pin (usually 0-1). |
| `Controls Framework` | Controls framework: shared input pin EventHandler that drives an output pin. |

## NamedControl

| Prefix | Description |
| ------ | ----------- |
| `NamedControl.GetText` | NamedControl.GetText(name) - returns the text displayed on the control with this Script Name. |
| `NamedControl.SetText` | NamedControl.SetText(name, value) - sets the text displayed on the control (use for Labels). |
| `NamedControl.GetValue` | NamedControl.GetValue(name) - returns the control's value within its Minimum/Maximum range. |
| `NamedControl.SetValue` | NamedControl.SetValue(name, value) - sets the control's value within its Minimum/Maximum range. |
| `NamedControl.GetPosition` | NamedControl.GetPosition(name) - returns the control's 0-1 position (linear, ignores taper). |
| `NamedControl.SetPosition` | NamedControl.SetPosition(name, position) - sets the control's 0-1 position (linear, ignores taper). |
| `NamedControl.ModifyValue` | NamedControl.ModifyValue(name, offset) - adds an offset to the control's value. Useful for up/down buttons. |
| `NamedControl.GetChanged` | NamedControl.GetChanged(name) - returns 1 if the value or text changed since the last check, otherwise 0. Checking clears the flag. Don't also use SubscribeText on the same control. |
| `NamedControl.SubscribeText` | NamedControl.SubscribeText(name) - subscribes to a control so NamedControl.EventHandler is called when it changes. Don't also use GetChanged on the same control. |
| `NamedControl.EventHandler` | NamedControl.EventHandler(name, value) - called when a subscribed control changes. value is a string. |
| `NamedControl.GetProperty` | NamedControl.GetProperty(name, propertyName) - reads a control or Control Panel Group property: col, row, cols, rows, position, shape, panel, panels, visible, min, max. |
| `NamedControl.SetProperty` | NamedControl.SetProperty(name, propertyName, v1...vN) - sets a control or Control Panel Group property. Returns nil on success, otherwise an error string. 'position' takes col, row; 'shape' takes col, row, cols, rows. |
| `NamedControl Framework`<br>`NamedControl Subscribe Framework` | NamedControl framework: SubscribeText plus a single EventHandler for event-driven scripts. |
| `NamedControl Polling Framework` | Polling framework: a Timer that uses NamedControl.GetChanged to act only when a control changes. |
| `NamedControl Latching Button` | Self-clearing latching button - recommended over momentary buttons when polling. |

## Device

| Prefix | Description |
| ------ | ----------- |
| `Device.Offline` | Device.Offline - true if the script is running offline in DesignOps, false when running on the device. |
| `Device.GetLastRecalledPreset` | Device.GetLastRecalledPreset() - returns the remote name and user name of the last recalled preset, or nil for each if none. |
| `Device.RecallPreset` | Device.RecallPreset(remoteName) - recalls a remote-enabled preset globally. Returns non-zero if the preset exists. |
| `Device.LocalUnit.ControlIP` | Device.LocalUnit.ControlIP - dotted IP address of the control network adapter. "0.0.0.0" until the IP has resolved. |
| `Device.LocalUnit.AudioIP` | Device.LocalUnit.AudioIP - dotted IP address of the network audio adapter. "0.0.0.0" until the IP has resolved. |
| `Device.LocalUnit.Name` | Device.LocalUnit.Name - unique network name of the device running the script. |
| `Device.LocalUnit.Type` | Device.LocalUnit.Type - hardware type enumeration of the device running the script. |
| `Device.LocalUnit.TypeName` | Device.LocalUnit.TypeName - hardware type name of the device running the script. |
| `Device.RemoteUnit.IP` | Device.RemoteUnit.IP - control IP of the associated Dante device, "0.0.0.0" if unknown. |
| `Device.RemoteUnit.Name` | Device.RemoteUnit.Name - network name of the associated Dante device. |
| `Device.RemoteUnit.Type` | Device.RemoteUnit.Type - hardware type enumeration of the associated Dante device (94 = Unspecified Dante). |
| `Device.RemoteUnit.TypeName` | Device.RemoteUnit.TypeName - hardware type name of the associated Dante device. |
| `Device.RemoteUnit.DanteIP` | Device.RemoteUnit.DanteIP - IP address of the associated device's Dante interface. |
| `Device.RemoteUnit.DanteMAC` | Device.RemoteUnit.DanteMAC - MAC address of the associated device's Dante interface. |
| `Device.RemoteUnit.DanteName` | Device.RemoteUnit.DanteName - Dante name of the associated device. |
| `Device.RemoteUnit.DanteModel` | Device.RemoteUnit.DanteModel - Dante model name of the associated device. |
| `Device.RemoteUnit.DanteMfg` | Device.RemoteUnit.DanteMfg - Dante manufacturer name of the associated device. |
| `Device IP Ready Framework` | Waits for Device.LocalUnit.ControlIP to become valid before starting communication. |

## System

| Prefix | Description |
| ------ | ----------- |
| `System.BuildVersion` | System.BuildVersion - software version string in X.X.X.X format. |
| `System.MajorVersion` | System.MajorVersion - major version number (X.x.x.x). |
| `System.MinorVersion` | System.MinorVersion - minor version number (x.X.x.x). |
| `System.PatchVersion` | System.PatchVersion - patch version number (x.x.X.x). |
| `System.Build` | System.Build - build number (x.x.x.X). |
| `System.IsEmulating` | System.IsEmulating - true if the script is running offline, false when running on hardware. |
| `System.IsDebugging` | System.IsDebugging - true if debug output is enabled (always true offline). |
| `System.ClearDebugging` | System.ClearDebugging() - clears the Lua Script Debug Output File. |
| `System.GetTime` | System.GetTime() - milliseconds since 1/1/1970. Compare two readings to measure elapsed time. |
| `System.GetExecutionTime` | System.GetExecutionTime() - ms used so far in the current 4 Hz pass. Keep each pass under 125 ms. |
| `System Elapsed Time`<br>`Elapsed Time Framework` | Measures elapsed milliseconds with System.GetTime inside a Timer. |
| `System Debug Print` | Only prints when debugging is enabled, avoiding debug work on the device. |

## HttpClient

| Prefix | Description |
| ------ | ----------- |
| `HttpClient.Download` | HttpClient.Download - GET text data from a URL. Returns true if accepted (max 8 open requests). User/Password/Headers/Timeout are optional. |
| `HttpClient.Upload` | HttpClient.Upload - send text data to a URL (POST by default). Returns true if accepted (max 8 open requests). |
| `HttpClient.CreateUrl` | HttpClient.CreateUrl - builds a URL from Host, and optional Port, Path, Query and Encode. |
| `HttpClient.EncodeParams` | HttpClient.EncodeParams - URL-encodes a table of parameters into key=value&key=value. |
| `HttpClient.EncodeString` | HttpClient.EncodeString(input, encodeSlash) - URL-encodes a string. encodeSlash defaults to true. |
| `HttpClient.DecodeString` | HttpClient.DecodeString(input) - decodes a URL-encoded string. |
| `HTTP Framework` | HTTP framework: shared response callback plus CreateUrl, Upload and Download. |

## TcpSocket

| Prefix | Description |
| ------ | ----------- |
| `TcpSocket.New()` | TcpSocket.New() - creates a TcpSocket object. Up to 8 per script. |
| `TcpSocket.ID` | TcpSocketName.ID - 1-8 number of the socket in the script. |
| `TcpSocket.EventHandler` | TcpSocketName.EventHandler(TcpSocket, event, error) - single callback for all socket events (compare with TcpSocket.Events). |
| `TcpSocket.ReadTimeout` | TcpSocketName.ReadTimeout - seconds to wait for a read before timing out. 0 (default) disables. |
| `TcpSocket.WriteTimeout` | TcpSocketName.WriteTimeout - seconds to wait for a write before timing out. 0 (default) disables. |
| `TcpSocket.ReconnectTimeout` | TcpSocketName.ReconnectTimeout - seconds to wait before reconnecting after an external disconnect (default 5). |
| `TcpSocket.IsConnected` | TcpSocketName.IsConnected - true if the socket is currently connected. |
| `TcpSocket.BufferLength` | TcpSocketName.BufferLength - count of received bytes waiting to be read. |
| `TcpSocket.Connect` | TcpSocketName:Connect(ip, port) - connects to an IP address (hostnames not supported). |
| `TcpSocket.Disconnect` | TcpSocketName:Disconnect() - disconnects a connected socket. |
| `TcpSocket.Write` | TcpSocketName:Write(data) - writes data to a connected socket. |
| `TcpSocket.Read` | TcpSocketName:Read(length) - reads and removes up to length bytes from the receive buffer. |
| `TcpSocket.ReadLine` | TcpSocketName:ReadLine(EOL, [delimiter]) - reads until the EOL is found. With TcpSocket.EOL.Custom, pass the delimiter string as the 2nd argument. |
| `TcpSocket.Search` | TcpSocketName:Search(pattern, [start]) - returns the 1-based index of an exact string in unread data, or nil. Does not consume data. |
| `TcpSocket.Connected` | TcpSocketName.Connected(sock) - called when the socket connects. |
| `TcpSocket.Reconnect` | TcpSocketName.Reconnect(sock) - called when the socket is attempting to reconnect. |
| `TcpSocket.Data` | TcpSocketName.Data(sock, data) - called when unread data is available. Read it with Read or ReadLine. |
| `TcpSocket.Closed` | TcpSocketName.Closed(sock) - called when the socket is closed. |
| `TcpSocket.Error` | TcpSocketName.Error(sock, err) - called when there is an error, with the error string. |
| `TcpSocket.Timeout` | TcpSocketName.Timeout(sock, err) - called on a read or write timeout, with the error string. |
| `TcpSocket.Events` | TcpSocket.Events - event enumeration for EventHandler: Connected=1, Reconnect=2, Data=3, Closed=4, Error=5, Timeout=6. |
| `TcpSocket.EOL` | TcpSocket.EOL - ReadLine enumeration: Any=1, CrLf=2, CrLfStrict=3, Lf=4, Null=5, Custom=6. |
| `TCP Framework` | TCP framework with a discrete handler for each socket event. |
| `TCP EventHandler Framework` | TCP framework with a single EventHandler handling all six TcpSocket.Events and line-based reads. |

## UdpSocket

| Prefix | Description |
| ------ | ----------- |
| `UdpSocket.New` | UdpSocket.New() - creates a UdpSocket object. Up to 8 per script. |
| `UdpSocket.ID` | UdpSocketName.ID - 1-8 number of the socket in the script. |
| `UdpSocket.Open` | UdpSocketName:Open(ip, port) - binds to the control or audio IP ("0.0.0.0" = control network) and port (0 = automatic). Returns true on success. |
| `UdpSocket.Close` | UdpSocketName:Close() - closes the socket. Don't reuse the object afterwards. |
| `UdpSocket.Send` | UdpSocketName:Send(ip, port, data) - sends data (must fit in one packet) to an IP and port. |
| `UdpSocket.GetSockName` | UdpSocketName:GetSockName() - returns the bound IP address and port. |
| `UdpSocket.Data` | UdpSocketName.Data(socket, packet) - called when a packet arrives. packet has .Address, .Port and .Data. |
| `UdpSocket.MulticastTtl` | UdpSocketName.MulticastTtl - hops allowed for sent multicast (default 1). Set before Open(). |
| `UdpSocket.MulticastLoop` | UdpSocketName.MulticastLoop - loop sent multicast back to this device (default true). Set before Open(). |
| `UdpSocket.JoinMulticast` | UdpSocketName:JoinMulticast(multicastIp, [interfaceIp]) - joins a 224.0.0.0-239.255.255.255 group. Call after Open(). Returns true on success. |
| `UDP Framework` | UDP framework: open a socket, handle received packets and send data. |
| `UDP Multicast Framework` | UDP multicast framework: set TTL/loopback, Open, JoinMulticast, receive and send. |

## SSH

| Prefix | Description |
| ------ | ----------- |
| `Ssh.New()` | Ssh.New() - creates an Ssh object. Up to 8 per script. |
| `SshName.ID` | SshName.ID - 1-8 number of the socket in the script. |
| `SshName.EventHandler(Ssh, event, error)` | SshName.EventHandler(Ssh, event, error) - single callback for all SSH events (compare with Ssh.Events). |
| `SshName.WriteTimeout` | SshName.WriteTimeout - seconds to wait for a write before timing out and disconnecting. 0 (default) disables. |
| `SshName.ReconnectTimeout` | SshName.ReconnectTimeout - seconds before reconnecting after an external disconnect (default 5). 0 disables reconnect. |
| `SshName.IsConnected` | SshName.IsConnected - true if the socket is currently connected. |
| `SshName.IsInteractive` | SshName.IsInteractive - set true if the server requires a pseudoterminal (PTY). Default false. |
| `SshName.BufferLength` | SshName.BufferLength - count of received bytes waiting to be read. |
| `SshName.PublicKey` | SshName.PublicKey - public key in SSH format for PKI authentication (max 4095 chars). |
| `SshName.PrivateKey` | SshName.PrivateKey - private key in PEM format for PKI authentication (max 4095 chars). |
| `SshName.PrivateKeyPassword` | SshName.PrivateKeyPassword - password for the private key, if needed (max 255 chars). |
| `SshName:Connect(ip, port, username, password)` | SshName:Connect(ip, port, username, password) - connects to an IP or hostname. Use "" as the password with key authentication. |
| `SshName:Disconnect()` | SshName:Disconnect() - disconnects a connected socket. |
| `SshName:Write(data)` | SshName:Write(data) - writes data (max 64K) to a connected socket. |
| `SshName:Read(length)` | SshName:Read(length) - reads and removes up to length bytes from the receive buffer. |
| `SshName:ReadLine(EOL, [delimiter])` | SshName:ReadLine(EOL, [delimiter]) - reads until the EOL is found. With Ssh.EOL.Custom, pass the delimiter string as the 2nd argument. |
| `SshName:Search(pattern, [start])` | SshName:Search(pattern, [start]) - returns the 1-based index of an exact string in unread data, or nil. |
| `SshName.LoginFailed(Ssh, error)` | SshName.LoginFailed(Ssh, error) - called when login fails, with the error string. |
| `SshName.Connected(Ssh)` | SshName.Connected(Ssh) - called when the socket connects and login succeeds. |
| `SshName.Reconnect(Ssh)` | SshName.Reconnect(Ssh) - called when the socket is attempting to reconnect. |
| `SshName.Data(Ssh, data)` | SshName.Data(Ssh, data) - called when unread data is available. Read it with Read or ReadLine. |
| `SshName.Closed(Ssh)` | SshName.Closed(Ssh) - called when the socket closes for any reason other than Disconnect(). |
| `SshName.Error(Ssh, error)` | SshName.Error(Ssh, error) - called when there is an error, with the error string. |
| `SshName.Timeout(Ssh, error)` | SshName.Timeout(Ssh, error) - called on a write timeout, with the error string. |
| `Ssh.Events` | Ssh.Events - event enumeration for EventHandler: Connected=1, Reconnect=2, Data=3, Closed=4, Error=5, Timeout=6, LoginFailed=7. |
| `Ssh.EOL` | Ssh.EOL - ReadLine enumeration: Any=1, CrLf=2, CrLfStrict=3, Lf=4, Null=5, Custom=6. |
| `SSH Framework` | SSH framework with password login and a discrete handler for each event. |
| `SSH EventHandler Framework` | SSH framework with a single EventHandler handling all seven Ssh.Events and line-based reads. |
| `SSH Key Auth Framework`<br>`SSH PKI Framework` | SSH framework using public/private key (PKI) authentication. |

## JSON

| Prefix | Description |
| ------ | ----------- |
| `json.require`<br>`require json` | Loads the JSON library. Required before using json.encode / json.decode. |
| `json.encode` | json.encode(object) - encodes a table, string, boolean, number, nil or json.null as a JSON string. |
| `json.decode` | json.decode(jsonString, [startPos]) - decodes JSON into a Lua value. Also returns the position after the decoded object. |
| `json.null` | json.null() - a JSON null that keeps its key in encoded tables (nil keys are dropped). |

## Driver Templates

| Prefix | Description |
| ------ | ----------- |
| `TCP Driver Framework`<br>`Driver Framework` | Starting point for a 3rd-party TCP control driver: IP from a Control Panel control, connection status LED, subscribed controls and line-based feedback parsing. |

Born out of a recording studio in 1976, Symetrix was created to make tools that deliver brilliant audio quality. As the AV industry has grown and changed, so have we. Longtime fans of Symetrix, Mark and Rachelle Graham joined the Symetrix team in 2019 as owners, kicking off the next chapter in Symetrix’s 40+ year history. Their dream of working in an audio/video tech business with their family has become a delightful reality. Symetrix continues to enable inspirational AV experiences while serving our unique mission to be a force for good in the world.
