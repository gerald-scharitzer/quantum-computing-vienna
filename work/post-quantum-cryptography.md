# Post-Quantum Cryptography

provides key exchange and signature algorithms that [resist quantum computers](https://www.etsi.org/technologies/quantum-safe-cryptography).

⚠️ **Construction Site** ⚠️

# Objective

Large parts of our information society rely on the following capabilities of cryptography.

Identity: We verify that we communicate with the right entity, before we send content.

Integrity: We verify that the message we received is the one sent.

Privacy: We communicate with each other and the content is known to us only.

This context focuses on these three capabilities,
but cryptography comes with others as well.

# Classic Method

With TLS we authenticate with certificates containing their public key.
The receiver of the public key can establish an encrypted communication channel with the sender of the key.
Communicating entities verify the identity of the other one by encoding a challenge, encrypting it, and then sending it to the other entity.
The receiver decrypts the encrypted challenge and generates the correct answer.
