# tcp-port-scanner
# Sandshark TCP Port Scanner (v1.0.0.00)

Sandshark is a lightweight, cross-platform network socket auditing tool written natively in Python 3. Developed as a practical implementation of Layer 4 networking concepts studied for the CompTIA Network+ curriculum, this utility provides system administrators with a fast, dependency-free method to discover open network pathways and audit endpoint security controls.

## Key Engineering Features

- **Robust Input Validation:** Parses input strings dynamically to convert port ranges (example: `20-80`) into usable integer streams, enforcing hard boundaries on valid network ports ($1$ to $65535$).
- **Dual Operational Modes:** Supports both interactive console runtimes and automated script executions via native command-line flags (`argparse`).
- **Resilient Exception Scoping:** Unlike basic scanning scripts that crash entirely upon encountering a dropped packet, Sandshark isolates `socket.timeout` and `socket.error` exceptions *inside* the execution loop. If a port is filtered or dead, the active socket closes cleanly, and the loop seamlessly continues to the next target.
- **Cross-Platform Environment Awareness:** Sniffs the host operating system dynamically to issue correct console-clearing commands seamlessly across Windows (`cls`), macOS, and Linux distributions (`clear`).
- **Zero External Dependencies:** Built entirely with native Python modules to guarantee zero friction and instant deployment on secure systems.

---

## Core Network Handshake Mechanics

Sandshark uses a **TCP Connect Scan** architecture via Python's native `socket.connect_ex()` method. This method hooks into the operating system's network stack to attempt a complete Layer 4 three-way handshake:
