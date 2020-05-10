# Self Signed Certificate

> Create a self-signed certificate in macos that will allow http2

Run the following in terminal. The settings are important, its the only way ive 
found that will enable chrome to truly trust the cert and allow the http2 
protocol to be used.

```bash
openssl req \
    -newkey rsa:2048 \
    -x509 \
    -nodes \
    -keyout server.local.key \
    -new \
    -out server.local.crt \
    -subj /CN=server.local \
    -reqexts SAN \
    -extensions SAN \
    -config <(cat /System/Library/OpenSSL/openssl.cnf \
        <(printf '[SAN]\nsubjectAltName=DNS:\server.local')) \
    -sha256 \
    -days 3650
```

Trust the cert in macos key chain

```bash
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain server.local.crt
```