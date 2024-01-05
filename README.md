# create-csr-ssl

Generate private key

```
openssl genrsa -out stg-ssl-private.key 2048
```

Create the `ssl.cnf` file and add the required domain names and information

```
[ req ]
default_bits            = 2048
encrypt_key             = no
default_md              = sha256
utf8                    = yes
string_mask             = utf8only
prompt                  = no
distinguished_name = req_distinguished_name
req_extensions     = req_ext

[ req_distinguished_name ]
countryName         = IN
stateOrProvinceName = KA
localityName        = Bangalore
organizationName    = Myorganisation
organizationalUnitName = Myorganisation
commonName          = example.mydomain.com

[ req_ext ]
subjectAltName = @alt_names

[alt_names]
DNS.1 = example.mydomain.com
DNS.2 = example2.mydomain.com
DNS.3 = example3.mydomain.com
```

Create CSR

```
openssl req -new -sha256 -out my.csr -key private.key -config ssl.cnf
```

Verify the csr

```
openssl req -in my.csr -noout -text
```
