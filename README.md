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
[DBG ][TLSW]: mbedtls_ssl_conf_ca_chain()
Connecting to ifconfig.io
[INFO][TLSW]: Starting TLS handshake with ifconfig.io
[DBG ][TLSW]: mbedtls_ssl_setup()
[INFO][TLSW]: TLS connection to ifconfig.io established
[DBG ][TLSW]: Server certificate:
    cert. version     : 3
    serial number     : 3F:28:36:EC:98:F3:1D:A8:10:6F:96:47:3E:9C:8B:B2
    issuer name       : C=GB, ST=Greater Manchester, L=Salford, O=COMODO CA Limited, CN=COMODO ECC Domain Validation Secure Server CA 2
    subject name      : OU=Domain Control Validated, OU=PositiveSSL Multi-Domain, CN=sni44589.cloudflaressl.com
    issued  on        : 2018-10-03 00:00:00
    expires on        : 2019-04-11 23:59:59
    signed using      : ECDSA with SHA256
    EC key size       : 256 bits
    basic constraints : CA=false
    subject alt name  : sni44589.cloudflaressl.com, *.8bit.tv, *.allseniorlivingrun.live, *.allseniorlivingsyes.live, *.andautoinsurancebuy.live, *.andglobaldentalimplantpurchesok.live, *.andseniorlivingkey.live, *.anokbestattungsversicherungok.live, *.anokunsoldsuvok.live, *.aptuklifeinsuranceok.live, *.authentic8.blog, *.beseniorparttimeshype.live, *.bewomencancertreatmentsok.live, *.bloodpressurehome.com, *.cancertreatm
[INFO][TLSW]: Certificate verification passed
[DBG ][TLSW]: send 56
HTTP/1.1 200 OK
Date: Tue, 12 Mar 2019 14:50:04 GMT
Content-Type: text/html; charset=utf-8
Transfer-Encoding: chunked
Connection: close
Set-Cookie: __cfduid=d7c5c5e5d175b7367e562180bdca57c2d1552402204; expires=Wed, 11-Mar-20 14:50:04 GMT; path=/; domain=.ifconfig.io; HttpOnly
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Server: cloudflare
CF-RAY: 4b66940f3911cc9d-WAW

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
