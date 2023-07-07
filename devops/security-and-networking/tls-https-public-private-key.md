## TLS, SSL, Public key, Private Key & SSH

### TLS, SSL, HTTPS
- TLS [ transport layer security ], SSL [ security sockets layer ] are security protocols to transfer data across network securly with encryption. 
- HTTPS is secured HTTP protocol. In HTTPS a TLS certificate or public key is provided to the browser client by the server. 

### Assymetric Encryption
- In Assymetric encryption, there are always key pairs. i.e public key and private key.
- Public key is generally widely distributed and public key is widely used for encrypting data.
- Private key is generally holded by the server or private entity [ i.e by a user in ssh context ].
- Private key is generally used to decrypt the data which is encrypted by public key. 
- In SSH[ secure shell ]context public key and private key are generated and public key is distributed or copied to the server the user need to login and holds the private key. 
- Using private key user will be able to SSH into the remote server.

### Symmetric Encryption
- Transferring huge amount of data through assymetric encryption is costly or inefficient. 
- So once a assymetric handshake is done data is trasfered using symmetric encryption. 
- In Symmetric encryption only one key is used for both encryption and decryption.
- In HTTPS using TLS/SSL a public key or TLS certificate is sent the the clent and it is used to establish assymetric handshake and then uses symmetric encryption once assymetric handshake is established.

### How do the TLS handshake happen.
- TLS handshake is transferring from assymetric to symmetric encryption. 
- i.e First client receieves the server's public key as TLS/HTTPS certificate. 
- Now client creates a `symmetric key`, encrypts it with the public key or SSL/TLS/HTTPS certificate and sends it to the server. 
- Server `decrypts` the `symmetric key with private key`
- Now both client and server has the symmetric key. 
- So client and server will start encrypting and decrypting messages using symmetric key which is more efficient. 