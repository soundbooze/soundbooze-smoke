<b>Absolutely awesome for paranoid pair!</b>

OpenBSD 6.0
x86_64 i386
sndio
<pre>                     _        
 ___ _ __ ___   ___ | | _____ 
/ __| '_ ` _ \ / _ \| |/ / _ \
\__ \ | | | | | (_) |   <  __/
|___/_| |_| |_|\___/|_|\_\___|
</pre>

 - Ultra lightweight, tiny, robust and extremely secure Voice Over TLS sitting on top of libtls with added Blowfish encryption for OpenBSD and sndio only.

> rcctl sndiod start (please refer to OpenBSD FAQ: Multimedia for configuring audio devices).

```
usage: smoke [-p playback device] [-c capture device] [-x key.pem] [-y cert.pem] [-S server] [-P port]
```

<pre>
-----------------------------------------------------

Device format (playback / capture):

snd/0       First playback device exposed by sndiod(8).
rsnd/0      First capture device.

-----------------------------------------------------

key.pem     PEM file containing a private key.
cert.pem    PEM file containing a certificate.

server      Server IP Address (IPv4 only)
port        Port number

-----------------------------------------------------
</pre>

<pre>
Generate PEM files (key and cert) with generatePEM.sh (optional)
You will be asked for a password each time you are trying to communicate, both users require the same password.

smoke> ./smoke 
Blowfish Password: 
Enter PEM pass phrase:
[+] Waiting for valid connection
[+] Authentication (x.x.x.x)
[+] Starting conversation

# Single Interface (both playback and capture frames will be transported over the same interface)

# (1) smoke -P 5150
# (4) smoke -S 10.0.0.2 -P 5151

# (2) smoke -S 10.0.0.1 -P 5150
# (3) smoke -P 5151

# Multiple Interface (playback and capture frames will be transported over different interfaces)

Both interfaces can accept different PEM files and a different password making it extremely secure.

## Server (111.5.5.5 & 222.5.5.5)

$ (1) smoke -P 5150
$ (4) smoke -S 222.6.6.6 -P 5151

## Client (111.6.6.6 & 222.6.6.6)

$ (2) smoke -S 111.5.5.5 -P 5150
$ (3) smoke -P 5151

Extremely more robust, guarding the port with pf(4).

NOTE:

** (1) Alice capture - bind(2), tls_write(3)
** (2) Bob playback - tls_read(3)
** (3) Bob capture - bind(2), tls_write(3)
** (4) Alice playback - tls_read(3)

SHARED LIBRARY DEPENDENCIES:

  /usr/lib/libsndio.so.6.1
  /usr/lib/libpthread.so.22.0
  /usr/lib/libtls.so.11.0
  /usr/lib/libc.so.88.0
  /usr/lib/libcrypto.so.38.0
  /usr/lib/libssl.so.39.0
  /usr/libexec/ld.so

</pre>

___

![alt text](https://licensebuttons.net/l/by-nc/3.0/88x31.png "Creative Commons")
###Attribution-NonCommercial 
###CC BY-NC

This license lets others remix, tweak, and build upon your work non-commercially, and although their new works must also acknowledge you and be non-commercial, they don’t have to license their derivative works on the same terms.

