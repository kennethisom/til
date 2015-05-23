Creating a CSR
--------------

Use the following settings (tweaked as needed) to generate your CSR configuration for OpenSSL (saved as req.cfg below):

```
[ req ]
default_bits            = 4096
default_keyfile         = privkey.pem
distinguished_name      = req_distinguished_name
prompt                  = no

[ req_distinguished_name ]
countryName                     = US
stateOrProvinceName             = .
localityName                    = .
organizationName                = .
organizationalUnitName          = .
commonName                      = example.com
emailAddress                    = someone@example.com
```

To generate the CSR do:

```bash
# Generate Private Key and CSR
openssl req -config req.cfg -newkey rsa:4096 -nodes -keyout subdomain.example.com.pem -sha256 -out subdomain.example.com.csr

# Protect Private Key
chmod 600 subdomain.example.com.pem
```
