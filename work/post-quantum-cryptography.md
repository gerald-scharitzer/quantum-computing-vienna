# Post-Quantum Cryptography

also known as quantum-safe or quantum-resistant cryptography,
provides key exchange and signature algorithms that [resist both classic and quantum computers](https://www.etsi.org/technologies/quantum-safe-cryptography).

⚠️ **Construction Site** ⚠️

It is "post-quantum", because it extends cryptography into the future, beyond the point in time from where have effective and efficient quantum computing systems.

It is "quantum-safe", because it carries the practical safety of effective and efficient cryptography into the quantum era.

It is "quantum-resistant" in as much as classic cryptography is resistant to classic cryptanalysis.

# Disclaimer

This my private rationale on post-quantum cryptography.

I do not recommend anything to anyone in this matter.

# Objective

Large parts of our information society rely on the following capabilities of cryptography.

- Authenticity: We verify that we communicate with the right entity, before we send or receive content.
- Integrity: We verify that the message we received is the one that was sent.
- Privacy: We communicate with each other and the content is known to us only.

Cryptography comes with other capabilities as well, but this context focuses on these three capabilities.

# Classic Method

Transport Layer Security (TLS) establishes secure communication sessions
with its [handshake algorithm](https://datatracker.ietf.org/doc/html/rfc8446#section-2).

1. The client requests a TLS connection and sends a list of supported cipher suites (TLS Handshake `ClientHello` message). These are combinations of symmetric key encryption algorithms, message authentication codes, key exchange algorithms, and parameters.
2. The server sends which cipher suite it picked (`ServerHello` message).
3. As of here the server communicates encrypted and sends its extension list (`EncryptedExtensions` message).
4. The server authenticates with its digital certificate (`Certificate` message) and the proof that it posesses the matching private key (`CertificateVerify` message).
5. The server concludes its part of the handshake (`Finished` message).
6. The client verifies the server certificate.
7. If the server requests a client certificate,
then the client authenticates with its digital certificate.

Each certificate contains its public key, a reference to its issuer,
and the digital signature of the issuer.

Communicating entities verify the identity of the other one by verifying the signature of the certificate against their set of trusted certificates.

8. The client establishes an encrypted communication channel with the server, based on the public key of this server, by
    - encrypting a cryptographically secure random number with the public key or
    - securely generating a cryptographically random session key
9. In both cases the client and server generate the session key from the exchanged random numbers.
10. The remaining communication is private, because it is encrypted with a random symmetric key, which is known to the two communicating entities only.

You can see this with the command
`echo Q | openssl s_client -msg openssl.org:443 | grep TLS`.

That looks similar to this.
```
>>> TLS 1.3, Handshake, ClientHello
<<< TLS 1.3, Handshake, ServerHello
<<< TLS 1.3, Handshake, EncryptedExtensions
<<< TLS 1.3, Handshake, Certificate
<<< TLS 1.3, Handshake, CertificateVerify
<<< TLS 1.3, Handshake, Finished
>>> TLS 1.3, ChangeCipherSpec
>>> TLS 1.3, Handshake, Finished
New, TLSv1.3, Cipher is ****************
>>> TLS 1.3, Alert, warning close_notify
```

## Cryptographic Hash Functions (CHFs)

enable data integrity checks by identifying with high probability,
whether a data set was changed or not,
based on the single input of the data set itself only.
They are one-way functions and make it theoretically possible, but practically infeasible to compute the input from the output.
Together with asymmetric key cryptography they enable digital signatures
by verifying with high probability,
whether the data was processed by something with access to a specific private key.

CHFs rely on efficiently mapping long input values to short output values
and varying greatly with small changes to the input.
These one-way functions, based on the amount of computation per input length, make it hard to find the input from the output (pre-image attack).
The effort to find the input grows exponentially with the length of the hash value.
It is statistically much more probable to find an input that results in the same output (birthday attack), which halves the effective hash size.
Doubling the hash size restores the security level.

## Symmetric Key Cryptography

provides privacy by encrypting the messages with a relatively short key lengths.

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

1976: The first asymmetric (public key) cryptosystem [Diffie-Hellman (DH) key exchange](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange) authenticates communicating partners and generates secret keys, that are known by these authenticated communicating partners only.
It can do so over an insecure channel, because reading all key exchange messages does not reveal all required information.

1977: The asymmetric [cryptosystem Rivest–Shamir–Adleman (RSA)](https://en.wikipedia.org/wiki/RSA_cryptosystem) encrypts and decrypts, and thus enables digital signatures, such that the private key is needed to create the signature and one can verify with the public key, whether the private key was used.

1994: Peter Shor invents [Shor's algorithm](https://en.wikipedia.org/wiki/Shor%27s_algorithm), which breaks both DH and RSA in polynomial time on a quantum computer with sufficient capacity.

1998: The first quantum computer is created and its size is 2 qubits.

2016: NIST starts the project [Post-Quantum Cryptography Standardization](https://csrc.nist.gov/projects/post-quantum-cryptography/post-quantum-cryptography-standardization) to develop quantum-safe asymmetric encryption and key exchange algorithms.

2020: Quantum computers reach a quantum volume of 2 to the 4th power.

2023: There are quantum computers with 1180 qubits now.

2024: NIST releases the first [post-quantum cryptography standards](https://csrc.nist.gov/Projects/post-quantum-cryptography/selected-algorithms) for key exchange and digital signatures.

2024: Quantum computers reach a quantum volume of 2 to the 20th power. That is an increment of computing capacity by a factor of approximately 65000 in four years, or a factor of 16 per year.

2025: The [International Year of Quantum Science and Technology 2025](https://quantum2025.org/)

# Implementations

[Open Quantum Safe (OQS)](https://openquantumsafe.org/) maintains [liboqs](https://openquantumsafe.org/liboqs/) and integrations into major [applications and protocols](https://openquantumsafe.org/applications/).

[PQ Code Package (PQCP)](https://github.com/pq-code-package) implements the [NIST FIPS 203 and 204](https://csrc.nist.gov/publications/fips).

Both OQS and PQCP are projects of the [Post-Quantum Cryptography Alliance (PQCA)](https://pqca.org/).

# Initiatives

There is a workgroup on [Quantum-safe Security](https://cloudsecurityalliance.org/research/working-groups/quantum-safe-security) at the Cloud Security Alliance.

The Cybersecurity & Infrastructure Security Agency (CISA) of the United States Government runs a [Post-Quantum Cryptography Initiative](https://www.cisa.gov/quantum).

The [Quantum Europe Strategy](https://digital-strategy.ec.europa.eu/en/library/quantum-europe-strategy) reads:

> "the EU and its Member States are now implementing the post-quantum cryptography [Recommendation](https://digital-strategy.ec.europa.eu/en/library/recommendation-coordinated-implementation-roadmap-transition-post-quantum-cryptography) and have just published a [Roadmap](https://digital-strategy.ec.europa.eu/en/news/eu-reinforces-its-cybersecurity-post-quantum-cryptography) for the transition to post-quantum cryptography."

# Conclusion

Even without the post-quantum cryptographic algorithms, there is value in knowing where you are using which cryptographic algorithms, such that you can change them effectively.
This leads to crypto-agility.

# Fun Facts

April 14 is Quantum Day, because 4.14 is the [Planck Constant](https://en.wikipedia.org/wiki/Planck_constant) in electronvolt seconds, rounded to two fractional digits.

The Crystals algorithms are named Dilithium and Kyber. Both are fictional crystals from science fiction.

Dilithium is used to control the matter anti-matter annihilation in space ship's warp cores.

Kyber

# References

[Quantum-Safe Cryptography](https://learning.quantum.ibm.com/course/practical-introduction-to-quantum-safe-cryptography/quantum-safe-cryptography)
