# NGINX Sample Config

## Allgemein

Konfigurationsdateien für den sicheren Betrieb eines frisch installierten Nginx Webservers.

Soweit möglich sind die Dateien modular aufgebaut.
Enthalten sind:

- `security.conf` -> Security Header
- `php_fastcgi.conf` -> Zusätzliche PHP Anweisungen
- `allow-cloudflare-only.conf` -> IP Addressbereiche von Cloudflare mit Anweisung alle anderen IPs zu sperren
- `general.conf` -> Allgemeingültige Konfigurationen
- `proxy.conf` -> Anweisungen für Reverse Proxy

## ACME SSL Zertifikate beantragen und installieren

### Verzeichnis anlegen

`mkdir -p /etc/letsencrypt/domain.tld/ecc`

### ECC Zertifikat beantragen

`acme.sh --issue --dns dns_cf --ecc --accountemail "admin@domain.tld" -d domain.tld -d *.domain.tld --keylength ec-384 --key-file /etc/letsencrypt/domain.tld/ecc/key.pem --ca-file /etc/letsencrypt/domain.tld/ecc/ca.pem --cert-file /etc/letsencrypt/domain.tld/ecc/cert.pem --fullchain-file /etc/letsencrypt/domain.tld/ecc/fullchain.pem --reloadcmd "systemctl restart nginx.service"`

### Zertifikat installieren

`acme.sh --install-cert -d domain.tld --key-file /etc/letsencrypt/domain.tld/ecc/key.pem --fullchain-file /etc/letsencrypt/domain.tld/ecc/fullchain.pem --reloadcmd "systemctl restart nginx force-reload"`
