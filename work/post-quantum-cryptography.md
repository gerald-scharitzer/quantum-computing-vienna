# Post-Quantum Cryptography

provides key exchange and signature algorithms that [resist quantum computers](https://www.etsi.org/technologies/quantum-safe-cryptography).

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
2. The receiver of the public key establishes an encrypted communication channel with the sender of the key.
3. Communicating entities verify the identity of the other one by encoding a challenge, encrypting it, and then sending it to the other entity.
4. The receiver decrypts the encrypted challenge and generates the correct answer.
