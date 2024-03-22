# Self-signed Certificate

## Generate Private CA (private key)

`$ openssl genrsa -aes256 -out ca-key.pem 4096`

## Generate CA Certificate

`$ openssl req -new -x509 -sha256 -days 365 -key ca-key.pem -out ca.pem`

## View

`$ openssl x509 -in ca.pem -text`

## Create self signed certificate using CA(private key)

`$ openssl genrsa -out cert-key.pem 4096`

## Create Certificate sign request

`$ openssl req -new -sha256 -subj "/CN=yourcn" -key cert-key.pem -out cert.csr`

## Create conf file

`$ echo "subjectAltName=DNS:your-dns.record,IP:0.0.0.0" >> extfile.cnf`

## Generate Certificate

`$ openssl x509 -req -sha256 -days 365 -in cert.csr -CA ca.pem -CAkey ca-key.pem -out cert.pem -extfile extfile.cnf -CAcreateserial`

## Create full-chain certificate file

`$ cat cert.pem > fullchain.pem`
`$ cat ca.pem >> fullchain.pem`

"cert-key.pem" private key<br>
"cert.pem" certificate 
