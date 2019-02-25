# TLSSocket example for Mbed OS

This examples application demonstrates the usage of `TLSSocket` API. To understand how secure sockets work in Mbed OS, please refer to the [Documentation](#documentation) section below.

### Selecting the network interface

This application is able to use any network inteface it finds. Please see the Mbed OS documentationg for [selecting the default network interface](https://os.mbed.com/docs/latest/apis/network-interfaces.html).

For example, building on Ethernet enabled boards, you do not do any configuration.

Building for WiFi boards, you need to provide SSID, password and security settings in `mbed_app.json` as instructed in the documentation. For example, like this:

```
{
    "target_overrides": {
        "*": {
            "platform.stdio-convert-newlines": true,
            "target.network-default-interface-type": "WIFI",
            "nsapi.default-wifi-security": "WPA_WPA2",
            "nsapi.default-wifi-ssid": "\"ssid\"",
            "nsapi.default-wifi-password": "\"password\""
        }
    }
}
```

Building for boards that have more that one network interface, you might need to override `target.network-default-interface-type` variable.

### Building

```
mbed compile -t <toolchain> -m <target>
```

For example, building for K64F using GCC: `mbed compile -t GCC_ARM -m K64F`

### Expected output ###

**Note:** The default serial port baud rate is 9600 bit/s (8N1).

```
TLSSocket Example.
Mbed OS version: 5.11.4

Connecting to network
[DBG ][TLSW]: mbedtls_ssl_conf_ca_chain()
Connecting to api.ipify.org
[INFO][TLSW]: Starting TLS handshake with api.ipify.org
[DBG ][TLSW]: mbedtls_ssl_setup()
[INFO][TLSW]: TLS connection to api.ipify.org established
[DBG ][TLSW]: Server certificate:
    cert. version     : 3
    serial number     : 92:0F:D1:B7:FE:4B:88:AE:B6:ED:5A:B0:C3:6C:56:68
    issuer name       : C=GB, ST=Greater Manchester, L=Salford, O=COMODO CA Limited, CN=COMODO RSA Domain Validation Secure Server CA
    subject name      : OU=Domain Control Validated, OU=PositiveSSL Wildcard, CN=*.ipify.org
    issued  on        : 2018-01-24 00:00:00
    expires on        : 2021-01-23 23:59:59
    signed using      : RSA with SHA-256
    RSA key size      : 2048 bits
    basic constraints : CA=false
    subject alt name  : *.ipify.org, ipify.org
    key usage         : Digital Signature, Key Encipherment
    ext key usage     : TLS Web Server Authentication, TLS Web Client Authentication


[INFO][TLSW]: Certificate verification passed
[DBG ][TLSW]: send 58
HTTP/1.1 200 OK
Server: Cowboy
Connection: close
Content-Type: text/plain
Vary: Origin
Date: Mon, 25 Feb 2019 13:13:10 GMT
Content-Length: 11
Via: 1.1 vegur

85.76.45.48
[INFO][TLSW]: Closing TLS
[DBG ][TLSW]: mbedtls_ssl_conf_ca_chain()
Done
```

### Documentation ###

For more information refer to following sections on the Mbed OS documentation:

* [IP Networking in Mbed OS](https://os.mbed.com/docs/mbed-os/latest/reference/ip-networking.html)
* API Documentation: [Network Socket overview](https://os.mbed.com/docs/mbed-os/latest/apis/network-socket.html)
* [Secure Sockets](https://os.mbed.com/docs/mbed-os/latest/reference/secure-socket.html)
* API Documentation: [TLSSocket](https://os.mbed.com/docs/mbed-os/latest/apis/tlssocket.html)

