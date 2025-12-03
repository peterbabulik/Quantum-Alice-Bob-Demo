# ⚛️ Quantum Alice & Bob Demo (BB84 Protocol)

**A high-capacity simulation of Quantum Key Distribution (QKD) using Python and PennyLane.**

This project demonstrates how two parties (Alice and Bob) can generate a shared secret key using quantum mechanics to securely encrypt and decrypt a message. It simulates the **BB84 protocol**, allowing Alice to transmit quantum states to Bob via a simulated channel.

## 📂 Repository Structure

*   **`Alice_Encrypt.ipynb`**: The Sender. Alice generates random bits, encodes them into qubits using random bases, and transmits them.
*   **`Bob_Decrypt.ipynb`**: The Receiver. Bob measures the incoming qubits, compares bases with Alice (Sifting), and decrypts the message.

## 🚀 Key Features

*   **High-Capacity Simulation**: Generates **500 qubits** to ensure the final sifted key is long enough to encrypt the full message `"HELLO_QUANTUM_WORLD"`.
*   **Simulated Quantum Channel**: Uses Python `pickle` serialization to mimic the physical transmission of photons. The file `quantum_channel.pkl` acts as the fiber optic cable.
*   **Real Encryption**: Implements the **One-Time Pad** (XOR) algorithm using the generated quantum key—the only mathematically unbreakable encryption method (provided the key is secure).
*   **PennyLane Integration**: Uses `pennylane.default.qubit` to accurately model quantum state preparation and measurement.

## 🛠️ Prerequisites

You can run these notebooks locally or in Google Colab. You will need the following Python libraries:

```bash
pip install pennylane numpy
```

## 📖 How to Run the Demo

Since this simulates a physical transfer of information, the order of operations matters:

### Step 1: Alice (Sender)
1.  Open **`Alice_Encrypt.ipynb`**.
2.  Run all cells.
3.  **Result**: Alice generates 500 qubits and saves two files:
    *   `quantum_channel.pkl` (The qubits sent to Bob)
    *   `alice_private_key.pkl` (Alice's private record for verification)
4.  *Note: If running locally, these files appear in your folder. If on Colab, download them.*

### Step 2: Bob (Receiver)
1.  Open **`Bob_Decrypt.ipynb`**.
2.  Ensure `quantum_channel.pkl` and `alice_private_key.pkl` are in the same directory (or uploaded to the Colab environment).
3.  Run all cells.
4.  **Result**: 
    *   Bob measures the qubits.
    *   He communicates with Alice to discard bits where their measurement bases didn't match ("Sifting").
    *   He successfully decrypts the message: **`HELLO_QUANTUM_WORLD`**.

## 🧠 How it Works (Under the Hood)

1.  **Preparation**: Alice creates a string of random bits ($0$ or $1$) and random bases ($+$ or $\times$).
2.  **Encoding**:
    *   If Basis is $+$ (Rectilinear): $0 \to |0\rangle$, $1 \to |1\rangle$
    *   If Basis is $\times$ (Diagonal): $0 \to |+\rangle$, $1 \to |-\rangle$
3.  **Transmission**: The state vectors are saved to the "channel" file.
4.  **Measurement**: Bob chooses his own random bases to measure the incoming qubits.
5.  **Sifting**: Alice and Bob publicly share *which* bases they used (but not the results). They keep only the bits where their bases matched.
6.  **Key Generation**: This resulting matching string becomes the **Shared Secret Key**.

## ⚠️ Note on Security
This is a **simulation**. In a real-world scenario, `alice_private_key.pkl` would never be shared. The security of BB84 comes from the fact that an eavesdropper (Eve) trying to measure the qubits in transit would disturb the quantum states, introducing errors that Alice and Bob would detect.

---
*Created by [Peter Babulik](https://github.com/peterbabulik)*
```
