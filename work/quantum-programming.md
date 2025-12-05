# Quantum Programming

**under construction**

Quantum computers perform their calculations by executing quantum operations,
but these are encoded with classic bits and bytes.

So far the only quantum device in a quantum computer is the quantum processor.
The control system reads the classic bits and bytes of the quantum instructions.

## Toolchain

Running quantum algorithms on quantum computers needs a stack of software engineering tools.

Source code management and version control keep your foundation safe.

Compilers translate source code into executable code.

Simulators run executable code on classic computers.

## Software Development Kit (SDK)

There are several quantum SDKs and the [Unitary Foundation](https://unitary.foundation/) covered this in several [Quantum Open Source Surveys](https://unitaryfoundation.github.io/survey-2025/).
Among others the 2025 survey lists these [full-stack development platforms](https://unitaryfoundation.github.io/survey-2025/#full-stack-development-platforms-compilers-and-simulators-used-currently-or-in-the-future).
The description is cited verbatim from the homepage of the SDK and does not necessarily reflect the author's opinion.

| SDK | Provider | Open Source | Repository | License | Description |
| --- | -------- | ----------- | ---------- | ------- | ----------- |
| [Qiskit](https://www.ibm.com/quantum/qiskit) | [IBM](https://www.ibm.com/) | yes | [GitHub](https://github.com/Qiskit/qiskit) | [Apache 2.0](https://github.com/Qiskit/qiskit/blob/main/LICENSE.txt) | Qiskit is the world’s most popular and performant software stack for quantum computing and algorithms research. Build, optimize, and execute quantum workloads at scale. |
| [PennyLane](https://pennylane.ai/) | [Xanadu](https://xanadu.ai/) | yes | [GitHub](https://github.com/PennyLaneAI/pennylane) | [Apache 2.0](https://github.com/PennyLaneAI/pennylane/blob/master/LICENSE) | The definitive open-source Python framework for quantum programming. Built by researchers, for research.

## Runtime

are simulators on classic computers or they are physical quantum computers.

Simulators can calculate the quantum effects, but can do so practically for small numbers only.
At larger numbers the exponential effort dominates.

For a scheduler, the quantum computers are just nodes with specific resources.
