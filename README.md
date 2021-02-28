# guacamole-test-server

A WebSocket broker server for testing RDP connections to [guacd](https://guacamole.apache.org/doc/gug/guacamole-architecture.html)

## Running

Package:

```
mvn package
```

Build:

```
java -jar target/gts.jar --guacd-host 1.2.3.4 --guacd-port 4822 --port 8080
```

## Connection parameters

| Parameter    | Description                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| hostname     | The hostname or IP address of the server Guacamole should connect to.                                                                                                                                                                                                                                                                                                                                    |
| protocol     | Protocol for guacamole server connection establishment to target PC client: VNC, SSH, RDP |
| port         | The port the RDP server is listening on, usually 3389. This parameter is optional. If this is not specified, the default of 3389 will be used.                                                                                                                                                                                                                                                               |
| username     | The username to use to authenticate, if any.                                                                                                                                                                                                                                                                                                                                                                 |
| password     | The password to use when attempting authentication, if any.                                                                                                                                                                                                                                                                                                                                                  |
| domain       | The domain to use when attempting authentication, if any.                                                                                                                                                                                                                                                                                                                                                    |
| security     | The security mode to use for the RDP connection. This mode dictates how data will be encrypted and what type of authentication will be performed, if any. By default, standard RDP encryption is requested, as it is the most widely supported. Possible values are: rdp, nla, tls, any                                                                                                                      |
| ignore-cert  | If set to "true", the certificate returned by the server will be ignored, even if that certificate cannot be validated. This is useful if you universally trust the server and your connection to the server, and you know that the server's certificate cannot be validated (for example, if it is self-signed).                                                                                            |
| disable-auth | If set to "true", authentication will be disabled. Note that this refers to authentication that takes place while connecting. Any authentication enforced by the server over the remote desktop session (such as a login dialog) will still take place. By default, authentication is enabled and only used when requested by the server.If you are using NLA, authentication must be enabled by definition. |
| width        | The name of the parameter containing the desired display width in pixels                                                                                                                                                                                                                                                                                                                                     |
| height       | The name of the parameter containing the desired display height in pixels                                                                                                                                                                                                                                                                                                                                    |
| dpi          | The desired effective resolution of the client display, in DPI                                                                                                                                                                                                                                                                                                                                               |
| audio        | The name of the parameter specifying one supported audio mimetype. This will normally appear multiple times within a single tunnel request once for each mimetype.                                                                                                                                                                                                                                           |
| video        | The name of the parameter specifying one supported video mimetype. This will normally appear multiple times within a single tunnel request once for each mimetype.                                                                                                                                                                                                                                           |
| image        | The name of the parameter specifying one supported image mimetype. This will normally appear multiple times within a single tunnel request once for each mimetype.                                                                                                                                                                                                                                           |
| enable-sftp  | Whether file transfer should be enabled. If set to "true", the user will be allowed to upload or download files from the specified server using SFTP. If omitted, SFTP will be disabled |
| enable-drive | File transfer is disabled by default, but with file transfer enabled, RDP users can transfer files to and from a virtual drive which persists on the Guacamole server. Enable file transfer support by setting this parameter to "true" |
| drive-path   | The directory on the Guacamole server in which transferred files should be stored. This directory must be accessible by guacd and both readable and writable by the user that runs guacd. This parameter does not refer to a directory on the RDP server |


Example connection string to an server:

```
RDP:
ws://192.168.88.129:8008/ws?hostname=192.168.88.131&port=3390&dpi=96&protocol=rdp&image=image%2Fpng&width=1920&height=1080&ignore-cert=true&enable-drive=true&drive-path=%2Fshared-folder&enable-sftp=undefined&clipboard-encoding=undefined

VNC:
ws://192.168.88.129:8008/ws?hostname=192.168.88.130&port=5900&dpi=96&protocol=vnc&image=image%2Fpng&width=1920&height=1080&ignore-cert=undefined&enable-drive=undefined&drive-path=undefined&enable-sftp=undefined&clipboard-encoding=undefined

```