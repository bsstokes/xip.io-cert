# Self-Signed SSL Certificate for xip.io

If you use [xip.io](http://xip.io/) with your development environment, here's an SSL certificate that might come in handy.

**This certificate is for development only.** You're browser will probably complain that it's self-signed and hasn't been verified.

- `xip.io.key` -- *Private* key
- `xip.io.csr` -- Certificate signing request
- `xip.io.crt` -- Self-signed certificate

## Here's How I Created the Files

### Private Key

    openssl genrsa -out xip.io.key 1024

### Certificate Signing Request (CSR)

    openssl req -new -key xip.io.key -out xip.io.csr

*Common Name* is `*.xip.io`, and the rest of the fields are blank.
    
### Self-Signed Certificate

    openssl x509 -req -days 365 -in xip.io.csr -signkey xip.io.key -out xip.io.crt

## Example nginx.conf Snippet

    server {
      listen       443;
      server_name  *.xip.io;

      ssl on;
      ssl_certificate     /path/to/certs/xip.io-cert/xip.io.crt;
      ssl_certificate_key /path/to/certs/xip.io-cert/xip.io.key;

      # The rest of the config...
    }
