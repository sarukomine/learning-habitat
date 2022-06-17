
### Contents

- [Create a Root CA](#create-a-root-ca)
- [Generate Self Signed Certificate](#generate-self-signed-certificate)
- [Extensions File](#extensions-file)

---

### Create a Root CA

openssl genrsa -des3 -out root.key 2048

openssl req -x509 -new -nodes -key root.key -sha256 -days 825 -out root.pem

---

### Generate Self Signed Certificate

openssl genrsa -out coca-cola-digital.test.key 2048

openssl req -new -key coca-cola-digital.test.key -out coca-cola-digital.test.csr

openssl x509 -req -in coca-cola-digital.test.csr -CA ../root.pem -CAkey ../root.key -CAcreateserial -out coca-cola-digital.test.crt -days 825 -sha256 -extfile coca-cola-digital.test.extensions -extensions coca_cola_digital

openssl x509 -noout -fingerprint -text < sample.test.pem > sample.test.info

---

### Extensions File

[ sample_test ]
nsCertType              = server
keyUsage                = digitalSignature,nonRepudiation,keyEncipherment
extendedKeyUsage        = serverAuth
subjectKeyIdentifier    = hash
authorityKeyIdentifier  = keyid,issuer
subjectAltName          = @sample_test_subject
[ sample_test_subject ]
DNS.1 = sample.test
DNS.2 = www.sample.test
