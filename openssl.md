# OpenSSL

Check certificate contents

```text
openssl x509 -in certfile.(pem/crt) -text -noout [-inform DER]
```

Check if certificate is valid

```text
openssl verify certfile.(pem/crt)
```

Check if website is serving a valid certificate

```text
openssl s_client -connect mysite.com:443
```

