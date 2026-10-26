***I. Diseño y Requisitos***

- ***Los dos dominios ficticios elegidos (uno por marca) y por qué los habéis nombrado así.***
- Los dos dominios falsos se llamarán infoweb.local y infonet.local los llame asi por que es fácil de recordar y escribir ***El MPM de Apache elegido y la justificación técnica de esa elección (repasad UD2, bloque de MPM).***
- He elegido event 
  - Por que no elegí prefork = usa un proceso completo por usuario y gasta mucha ram solo se utiliza si no tenemos mas opciones por culpa de programas viejos
  - Por que no elegi worker = porque utiliza hilos no como prefork, pero aun asi los hilos de trabajo  bloqueados aunque ya no sean necesarios y por tanto llega un punto donde te quedas sin hilos y sin RAM

## V. Fase 3 — Diagnóstico provocado

## Verificación TLS con OpenSSL

Comando: `openssl s_client -connect 127.0.0.1:443 -servername infoweb.local`

```text
CONNECTED(00000003)
subject=CN=selena.iaw.net
issuer=CN=selena.iaw.net
Verification error: self-signed certificate
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Verify return code: 18 (self-signed certificate)
```
Selena@selena-G5-GD:~/IAW/Practica1$ openssl s_client -connect localhost:443 -servername infoweb.local
Connecting to 127.0.0.1
CONNECTED(00000003)
depth=0 CN=selena.iaw.net
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=selena.iaw.net
verify return:1
---
Certificate chain
 0 s:CN=selena.iaw.net
   i:CN=selena.iaw.net
   a:PKEY: EC, (prime256v1); sigalg: ecdsa-with-SHA256
   v:NotBefore: Oct 21 18:03:52 2026 GMT; NotAfter: Oct 21 18:03:52 2027 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIBiDCCAS2gAwIBAgIUGuCr2y6UB5Ye6tC06aD5vEk15/4wCgYIKoZIzj0EAwIw
GTEXMBUGA1UEAwwOc2VsZW5hLmlhdy5uZXQwHhcNMjYxMDIxMTgwMzUyWhcNMjcx
MDIxMTgwMzUyWjAZMRcwFQYDVQQDDA5zZWxlbmEuaWF3Lm5ldDBZMBMGByqGSM49
AgEGCCqGSM49AwEHA0IABETovljaJ4b3ErJx3yK6y89r8zLmGgjAJ3jhmFMxvwiF
6r1U6sLxZzV5FOVl19mes/LDs+x+vurzpIbXvDniWfmjUzBRMB0GA1UdDgQWBBQf
X3jmptXd4/qMVBLbOIQtZmWqXjAfBgNVHSMEGDAWgBQfX3jmptXd4/qMVBLbOIQt
ZmWqXjAPBgNVHRMBAf8EBTADAQH/MAoGCCqGSM49BAMCA0kAMEYCIQCXt3/o2wlM
L1AUaOdrRqXv5LyPxjYcvyicOWJfGVlR+wIhAOwjHd6mzSf8eNHXXdamaAV6x6Nq
vPWvfAxVtF+Q7g9s
-----END CERTIFICATE-----
subject=CN=selena.iaw.net
issuer=CN=selena.iaw.net
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: ecdsa_secp256r1_sha256
Negotiated TLS1.3 group: X25519MLKEM768
---
SSL handshake has read 1858 bytes and written 1635 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Protocol: TLSv1.3
Server public key is 256 bit
This TLS version forbids renegotiation.
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 9A8C5E343B790D16B2BF9728D27C223F4954D1CB4BD723BB92964A2AEED40501
    Session-ID-ctx: 
    Resumption PSK: C6146943E31D9075A622CF580D91E2D2FE5DBD7AB89332D898D57436BF06A8001E50B468257A3BAA9D31E5A42E80E6DB
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - a0 8b cb 0f c7 f2 6f b6-61 cb 6b 04 84 4b 40 f3   ......o.a.k..K@.
    0010 - 8e f6 cc 2a 9f e4 95 db-31 e9 f1 84 6a 51 05 5a   ...*....1...jQ.Z
    0020 - e4 a6 16 ec 29 5d 8c 70-41 0a 6d 29 f4 9d 12 7a   ....)].pA.m)...z
    0030 - 15 56 00 8f 19 37 b9 1d-ab de 13 55 f1 3e 0d 70   .V...7.....U.>.p
    0040 - 21 02 b7 d1 07 c1 d4 01-09 04 41 e6 7b 09 88 ee   !.........A.{...
    0050 - d5 b3 c6 eb 1e 82 c7 5f-f2 c5 a8 7e 38 fa 64 e5   ......._...~8.d.
    0060 - d2 12 66 e3 4d 0d 53 e2-ef fb 7a e9 d4 04 48 2d   ..f.M.S...z...H-
    0070 - 72 1c 37 6f 8d 70 47 1a-23 d7 73 01 fb ab 72 f7   r.7o.pG.#.s...r.
    0080 - 7d 25 50 4d f9 76 a7 73-de 02 d1 10 92 07 33 09   }%PM.v.s......3.
    0090 - a3 c1 55 d2 cc 84 5c 8f-b4 95 88 de 03 66 42 07   ..U...\......fB.
    00a0 - 49 a4 8e b3 7d 5e 93 c5-95 c5 02 a4 eb f8 6d f0   I...}^........m.
    00b0 - a1 34 c7 79 28 6e 60 f9-13 55 e0 b9 06 7a 56 f7   .4.y(n`..U...zV.
    00c0 - eb 2c cb 47 48 e5 e0 33-3d d4 42 82 51 3c bf 10   .,.GH..3=.B.Q<..
    00d0 - bb 65 97 31 5c 04 ef 5b-70 1b fe d5 ab ed 83 f8   .e.1\..[p.......
    00e0 - d4 dc af de 36 99 7b 79-88 0c 09 47 13 9d bb 0e   ....6.{y...G....

    Start Time: 1793008525
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 519112DA873896C979EF16A0A19F86C72161ED031495435A68DC188583B87C9D
    Session-ID-ctx: 
    Resumption PSK: FF575DFC9B0EBCF29FBE214DBAF33266867B365B2283C3F047EB4A47F031E34EB141B0B0829003B9DEC1453A0920E5D9
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - a0 8b cb 0f c7 f2 6f b6-61 cb 6b 04 84 4b 40 f3   ......o.a.k..K@.
    0010 - 8e 23 e3 43 a8 b2 1e a7-37 69 46 82 d5 25 76 a7   .#.C....7iF..%v.
    0020 - 75 7b 89 ca 17 08 73 bc-77 29 b9 33 80 36 c6 dc   u{....s.w).3.6..
    0030 - 2f 24 26 a3 03 d5 02 e0-87 75 b0 6a 5a 85 cf 0f   /$&......u.jZ...
    0040 - 95 68 a9 1b 0e ec 52 63-e0 10 c5 83 7f a9 4c 17   .h....Rc......L.
    0050 - 83 c2 34 d7 2c ed c5 05-80 0b c6 4b 97 06 be 21   ..4.,......K...!
    0060 - d7 ed 60 c7 2f 82 84 0f-0e bc 89 b8 cd 00 54 c3   ..`./.........T.
    0070 - 90 f8 08 ed cc 6e 59 26-8c 4e 2a 8c 70 54 b1 70   .....nY&.N*.pT.p
    0080 - bf be 47 56 2c 2a 4b 2c-b6 72 fe 93 76 dc 6d d4   ..GV,*K,.r..v.m.
    0090 - ad 30 2b 69 66 82 ac 7d-92 b3 26 b8 d5 03 57 63   .0+if..}..&...Wc
    00a0 - 3f 02 bc 01 37 7b b2 a1-44 e6 33 e5 ca 2f b7 8d   ?...7{..D.3../..
    00b0 - c4 49 43 00 e2 40 82 55-7d f0 22 5c f4 e3 91 74   .IC..@.U}."\...t
    00c0 - b3 94 34 17 89 a8 c4 cf-1e 6c 82 57 0c 8a e8 6f   ..4......l.W...o
    00d0 - e0 ef 4e af 74 2d 56 64-12 e3 26 ed 2e 39 16 10   ..N.t-Vd..&..9..
    00e0 - 9f 1b 71 39 19 f9 31 e7-44 25 34 f8 83 5f a8 14   ..q9..1.D%4.._..

    Start Time: 1793008525
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
