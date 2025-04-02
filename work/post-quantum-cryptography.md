# Post-Quantum Cryptography

also known as quantum-safe or quantum-resistant cryptography,
provides key exchange and signature algorithms that [resist both classic and quantum computers](https://www.etsi.org/technologies/quantum-safe-cryptography).

⚠️ **Construction Site** ⚠️

# Objective

Large parts of our information society rely on the following capabilities of cryptography.

Authenticity: We verify that we communicate with the right entity, before we send content.

Integrity: We verify that the message we received is the one sent.

Privacy: We communicate with each other and the content is known to us only.

This context focuses on these three capabilities,
but cryptography comes with others as well.

# Classic Method

Transport Layer Security (TLS) establishes secure communication sessions.

1. Its handshake algorithm authenticates with certificates containing their public key.
2. Communicating entities verify the identity of the other one by verifying the signature of the certificate against their set of trusted certificates.
3. The receiver of the public key establishes an encrypted communication channel with the sender of the key by
    - encrypting a cryptographically secure random number with the public key or
    - securely generating a cryptographically secure random number
4. The sender decrypts the encrypted challenge and generates the correct answer.

You can see this with the command
`echo Q | openssl s_client -msg openssl.org:443 | grep TLS`.

# Quantum Cryptanalysis

The Grover algorithm finds solutions for cryptographic hashes and symmetric keys in the square root of the hash size or key size respectively. This can be neutralized by simply doubling the key size.

## Shor's Algorithm

finds solutions for asymmetric keys based on prime factoring and discrete logarithm in a polynomial of the key size instead of growing exponentially with the key size.

Classic: Real number `r` times basis `b` raised by exponent `n`

Shor: Real number `s` times basis `n` raised by exponent `e`

where `n` is the key size in bit.

# References

[Quantum-Safe Cryptography](https://learning.quantum.ibm.com/course/practical-introduction-to-quantum-safe-cryptography/quantum-safe-cryptography)
