# Post-Quantum Cryptography

also known as quantum-safe or quantum-resistant cryptography,
provides key exchange and signature algorithms that [resist both classic and quantum computers](https://www.etsi.org/technologies/quantum-safe-cryptography).

⚠️ **Construction Site** ⚠️

It is "post-quantum", because it extends cryptography into the future,
beyond the point in time where have effective and efficient quantum computing systems.

It is "quantum-safe", because it carries the practical safety of effective and efficient cryptography into the quantum era.

It is "quantum-resistant" in as much as classic cryptography is resistant to classic analysis.

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

## Cryptographic Hash Functions (CHFs)

enable data integrity checks and digital signatures.
These one-way functions make it hard to find the input from the output (pre-image attack).
The effort to find the input grows exponentially with the length of the hash value.
It is statistically much more probable to find an input that results in the same output (birthday attack), which halves the effective hash size.
Doubling the hash size restores the security level.

# Quantum Cryptanalysis

The classic cryptographic algorithms that we rely on today are affected by
quantum computers and algorithms to varying extents.

## Grover's Algorithm

finds solutions for cryptographic hashes and symmetric keys in the square root of the hash size or key size respectively.
This can be neutralized by simply doubling the key size.
Enforcing the collision resistance of cryptographic hash functions (CHFs) already requires doubling the hash size, so Grover is neutralized for CHFs by this.

## BHT Algorithm

combines aspects of the birthday attack with Grover's algorithm.
It theoretically splits the effective key length into 1/3,
but that would require quantum random access memory (QRAM),
which we do not have yet.
Without QRAM it still splits the effective key length to 2/5.

## Shor's Algorithm

finds solutions for asymmetric keys based on prime factoring and discrete logarithm in a polynomial of the key size instead of growing exponentially with the key size.

Classic: Real number `r` times basis `b` raised by exponent `n`

Shor: Real number `s` times basis `n` raised by exponent `e`

where `n` is the key size in bit.

# References

[Quantum-Safe Cryptography](https://learning.quantum.ibm.com/course/practical-introduction-to-quantum-safe-cryptography/quantum-safe-cryptography)
