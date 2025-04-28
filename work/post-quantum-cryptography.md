# Post-Quantum Cryptography

also known as quantum-safe or quantum-resistant cryptography,
provides key exchange and signature algorithms that [resist both classic and quantum computers](https://www.etsi.org/technologies/quantum-safe-cryptography).

⚠️ **Construction Site** ⚠️

It is "post-quantum", because it extends cryptography into the future,
beyond the point in time where have effective and efficient quantum computing systems.

It is "quantum-safe", because it carries the practical safety of effective and efficient cryptography into the quantum era.

It is "quantum-resistant" in as much as classic cryptography is resistant to classic cryptanalysis, where one-way functions make it theoretically possible, but practically infeasible to compute the input from the output.

# Objective

Large parts of our information society rely on the following capabilities of cryptography.

- Authenticity: We verify that we communicate with the right entity, before we send content.
- Integrity: We verify that the message we received is the one sent.
- Privacy: We communicate with each other and the content is known to us only.

This context focuses on these three capabilities,
but cryptography comes with others as well.

# Classic Method

Transport Layer Security (TLS) establishes secure communication sessions
with its handshake algorithm.

1. The client requests a TLS connection and sends a list of supported cipher suites. These are combinations of symmetric key encryption algorithms, message authentication codes, key exchange algorithms, and parameters.
2. The server sends which cipher suite it picked and
authenticates with its digital certificate.
3. The client verifies the server certificate.
4. If the server requests a client certificate,
then the client authenticates with its digital certificate.

Each certificate contains its public key, a reference to its issuer,
and the digital signature of the issuer.

Communicating entities verify the identity of the other one by verifying the signature of the certificate against their set of trusted certificates.

5. The client establishes an encrypted communication channel with the server, based on the public key of the server, by
    - encrypting a cryptographically secure random number with the public key or
    - securely generating a cryptographically secure random number
3. The sender decrypts the encrypted challenge and generates the correct answer.

You can see this with the command
`echo Q | openssl s_client -msg openssl.org:443 | grep TLS`.

## Cryptographic Hash Functions (CHFs)

enable data integrity checks by identifying with high probability,
whether a data set was changed or not,
based on the single input of the data set itself only.
Together with asymmetric key cryptography they enable digital signatures
by verifying with high probability,
whether the data was processed by something with access to a specific private key.

CHFs rely on efficiently mapping long input values to short output values
and varying greatly with small changes to the input.
These one-way functions, based on the amount of computation per input length, make it hard to find the input from the output (pre-image attack).
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

# Timeline

1925: The [methods of quantum mechanics are developed](https://documents.un.org/doc/undoc/ltd/n24/131/80/pdf/n2413180.pdf).

...

2025: The [International Year of Quantum Science and Technology 2025](https://quantum2025.org/)

# References

[Quantum-Safe Cryptography](https://learning.quantum.ibm.com/course/practical-introduction-to-quantum-safe-cryptography/quantum-safe-cryptography)
