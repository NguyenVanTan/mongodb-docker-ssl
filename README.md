
#### Gen root key 
    openssl genrsa -out rootCA.key 2048
#### self-sign this certificate. You can also create a key that is password protected by adding `-des3`
    openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem

>You are about to be asked to enter information that will be incorporated
into your certificate request. What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
> - Country Name (2 letter code) []:**VN**

> - State or Province Name (full name) []:**DaNang**

> - Locality Name (eg, city) []:**DaNang**

> - Organization Name (eg, company) []:**Sun**

> - Organizational Unit Name (eg, section) []:**Div2**

> - Common Name (eg, fully qualified host name) []:**localhost**

> - Email Address []:**tannv85@gmail.com**

***Done, this will create an SSL certificate called rootCA.pem, signed by itself, valid for 1024 days, and it will act as our root certificate.***
 
---
#### Create key for Mongodb
    openssl genrsa -out mongodb.key 2048
#### generate the certificate signing request
    openssl req -new -key mongodb.key -out mongodb.csr

>You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
- Country Name (2 letter code) []:**VN**

- State or Province Name (full name) []:**DaNang**

- Locality Name (eg, city) []:**DaNang**

- Organization Name (eg, company) []:**Sun**

- Organizational Unit Name (eg, section) []:**Div2**

-  Common Name (eg, fully qualified host name) []:**localhost**

-  Email Address []:**tannv85@gmail.com**

- Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:**tannv**

> **Refer to changlenge password**: 
     https://serverfault.com/questions/266232/what-is-a-challenge-password/266258

#### creates a signed certificate called mongodb.crt which is valid for 500 days 
    openssl x509 -req -in mongodb.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out mongodb.crt -days 500 -sha256


#### convert  to pem file 
    cat mongodb.key mongodb.crt > mongodb.pem






