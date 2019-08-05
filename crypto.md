### Cryptography

## Encryption
# Asymmetric
* Asymmetric encryption uses different keys for encryption and decryption (2 keys  = 1 public & 1 private)
* Is more secure but slow
* examples:
  * AES
  * mm

# Symmetric
* Symmetric encryption uses the same key for both encryption and decryption (1 public key)
* usually much faster but the key needs to be transferred over an encrypted channel
* examples:
 * Diffie-Hellman
 * RSA
 * SSH uses it
 * TLS ( technically both symmetric & asymmetric)

# Summary
* a hybrid approach should be preferred
* Setting up a channel using asymmetric encryption and then sending the data using symmetric process.
