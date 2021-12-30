# Cryptography

### introduction
cryptography is needed to provide better security.

data -> encrypted data

7 crypto concepts:

#### Hash
- input -> hashing function(md4, sha, argon2) -> fixed output
- same input will produce the same output
- infeasable to reverse it
- useful for storing passwords
- md5 has become deprecated
- hashing a password to store in a database is not good enough

#### Salt
- a salt is a random value that is added to the input before it is hashed

#### HMAC

- HMAC stands for hash-based message authentication code
- is a hash that also requires a password. the only person that can create the same hash signature also needs the key/password.
- an example is a JSON webtoken

#### Symmetric Encryption

- take the input and make a cipher text. then a key or password is provided to the receiver to decrypt the cipher text.

#### Keypairs

- there is a private key which is a secret and there is a public key that is shared between the sender and the receiver

#### Assymetric Encryption

- HTTPS uses asymmetric encryption to establish the identity of the parties and to exchange a symmetric key. 
Then symmetric encryption is used since it's faster

#### signing

- a digital signature. the sender will use their private key to sign a hash of the original message. the receiver can use a public key
to verify the authenticity of the payload.