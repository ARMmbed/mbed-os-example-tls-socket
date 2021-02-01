![](./resources/warning.png)
## This example has been deprecated

Please use [sockets example](https://github.com/ARMmbed/mbed-os-example-sockets) instead.

---


# TLSSocket example for Mbed OS

This examples application demonstrates the usage of `TLSSocket` API. To understand how secure sockets work in Mbed OS, please refer to the [Documentation](#documentation) section below.
**NOTE**: This example works only on devices having TRNG supported!

### Selecting the network interface

This application is able to use any network inteface it finds. Please see the Mbed OS documentation for [selecting the default network interface](https://os.mbed.com/docs/latest/apis/network-interfaces.html).

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

### Configuring mbedtls

It might be necessary to configure the mbedtls library with appropriate macros in mbed_app.json file. Some boards (like UBLOX_EVK_ODIN_W2) will work fine without any additional configuration and some of them might require some minimal adjustment. For example K64F will require at least the following macro added:

```
{
    "macros": ["MBEDTLS_SHA1_C"],
    "target_overrides": {
        ...
    }
}
```

See [mbedtls configuration guidelines](https://github.com/ARMmbed/mbed-os/tree/master/features/mbedtls#configuring-mbed-tls-features) for more details.

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
Connecting to ifconfig.io
[DBG ][TLSW]: mbedtls_ssl_conf_ca_chain()
[INFO][TLSW]: Starting TLS handshake with ifconfig.io
[DBG ][TLSW]: mbedtls_ssl_setup()
[INFO][TLSW]: TLS connection to ifconfig.io established
[DBG ][TLSW]: Server certificate:
    cert. version     : 3
    serial number     : 0C:41:8C:DF:D9:3E:0D:A0:FC:7F:46:90:C1:64:A0:F2
    issuer name       : C=US, ST=CA, L=San Francisco, O=CloudFlare, Inc., CN=CloudFlare Inc ECC CA-2
    subject name      : C=US, ST=CA, L=San Francisco, O=Cloudflare, Inc., CN=sni.cloudflaressl.com
    issued  on        : 2020-01-30 00:00:00
    expires on        : 2020-10-09 12:00:00
    signed using      : ECDSA with SHA256
    EC key size       : 256 bits
    basic constraints : CA=false
    subject alt name  :
        dNSName : sni.cloudflaressl.com
        dNSName : *.ifconfig.io
        dNSName : ifconfig.io
    key usage         : Digital Signature
    ext key usage     : TLS Web Server Authentication, TLS Web Client Authentication
    certificate policies : ???, ???


[INFO][TLSW]: Certificate verification passed
[DBG ][TLSW]: send 56
HTTP/1.1 200 OK
Date: Wed, 19 Feb 2020 11:06:02 GMT
Content-Type: text/html; charset=utf-8
Transfer-Encoding: chunked
Connection: close
Set-Cookie: __cfduid=da3c9233e724ec7c8b091ceac83d117c91582110361; expires=Fri, 20-Mar-20 11:06:01 GMT; path=/; domain=.ifconfig.io; HttpOnly; SameSite=Lax
CF-Cache-Status: DYNAMIC
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Alt-Svc: h3-25=":443"; ma=86400, h3-24=":443"; ma=86400, h3-23=":443"; ma=86400
Server: cloudflare
CF-RAY: 5677c4e25b74fe34-HEL

<html>
...
ifconfig.io's HTML code
...
</html>

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

### License and contributions

The software is provided under Apache-2.0 license. Contributions to this project are accepted under the same license. Please see [contributing.md](CONTRIBUTING.md) for more info.

This project contains code from other projects. The original license text is included in those source files. They must comply with our license guide.
