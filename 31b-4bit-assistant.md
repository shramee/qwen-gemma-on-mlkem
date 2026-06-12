mlx_vlm.generate --model "mlx-community/gemma-4-31B-it-4bit" \
--draft-model mlx-community/gemma-4-31B-it-qat-assistant-4bit \
--prompt "can you show me how ml-kem works with a little example?" \
--max-tokens 20480 --verbose

-------------

Files: [] 

Prompt: <bos><|turn>user
can you show me how ml-kem works with a little example?<turn|>
<|turn>model
<|channel>thought
<channel|>
ML-KEM (Module-Lattice-based Key Encapsulation Mechanism), formerly known as **Kyber**, is the new standard for post-quantum cryptography.

Unlike RSA or Elliptic Curve (ECC), which rely on the difficulty of factoring large numbers or calculating discrete logarithms, ML-KEM relies on the **Learning With Errors (LWE)** problem—specifically, the difficulty of finding a secret vector in a high-dimensional lattice when "noise" has been added.

Here is a simplified explanation and a conceptual example.

---

### 1. The Core Concept: "Noise"
Imagine I tell you:
$10 \times 5 = 50$
You can easily find the numbers. But what if I add a tiny bit of random "noise"?
$10 \times 5 \approx 51$

If I give you thousands of these "noisy" equations, it becomes mathematically impossible to figure out the original numbers unless you have a "secret key" that allows you to filter out the noise.

### 2. How ML-KEM Works (The Process)

ML-KEM is a **Key Encapsulation Mechanism**. This means it isn't used to encrypt a whole file; it is used to securely agree on a **Symmetric Key** (like an AES key) that both parties can then use to encrypt their actual data.

#### Step A: Key Generation (Alice)
Alice creates a public "lattice" (a matrix of numbers) and a secret "vector."
1. **Public Key:** A matrix $\mathbf{A}$ and a result $\mathbf{t}$ (where $\mathbf{t} = \mathbf{A}s + e$). 
   * *Note: $s$ is the secret, and $e$ is a small error/noise.*
2. **Private Key:** The secret vector $s$.

#### Step B: Encapsulation (Bob)
Bob wants to send a secret key to Alice. He uses Alice's public key.
1. Bob picks a random secret value (the "seed" for the key).
2. He performs a similar lattice multiplication using Alice's public key and adds his own noise.
3. He sends the result (the **Ciphertext**) to Alice.

#### Step C: Decapsulation (Alice)
Alice receives the ciphertext. Because she knows the secret vector $s$, she can "subtract" the lattice structure from the ciphertext.
1. The result is the original secret value, but it still has some noise attached.
2. Alice uses a **rounding function** (essentially "rounding to the nearest whole number") to strip away the noise.
3. Now Alice and Bob both have the exact same secret key.

---

### 3. A "Tiny" Numerical Example
*To keep this readable, we will use tiny numbers. In real ML-KEM, these are large polynomials.*

**Setup:** Let's work with numbers modulo 17 (all results are the remainder after dividing by 17).

**1. Alice's Key Gen:**
*   **Public Matrix $\mathbf{A}$:** $[4]$ (A simple $1 \times 1$ matrix)
*   **Secret $s$:** $[3]$
*   **Noise $e$:** $[1]$
*   **Public Key $\mathbf{t}$:** $(4 \times 3) + 1 = 13$.
*   *Alice publishes $\mathbf{A}=[4]$ and $\mathbf{t}=13$. She keeps $s=3$ secret.*

**2. Bob's Encapsulation:**
Bob wants to send a bit (0 or 1). Let's say he wants to send **1**.
*   Bob picks his own noise $e_{bob} = [1]$.
*   He calculates a value using Alice's public key: $(4 \times 1) + 1 = 5$.
*   He "masks" his bit (1) by adding it to a multiple of the modulus (roughly).
*   *Bob sends the ciphertext to Alice.*

**3. Alice's Decapsulation:**
Alice takes Bob's ciphertext and multiplies it by her secret $s=3$.
*   Because of the way the math is structured, the "lattice" parts cancel out, leaving:
    $\text{Result} = (\text{Bob's Bit}) + (\text{Small Noise})$
*   Alice sees the result is something like $1.2$.
*   She **rounds** $1.2$ to the nearest integer $\rightarrow \mathbf{1}$.
*   **Success!** Alice recovered Bob's bit.

---

### Summary Table

| Feature            | Traditional (RSA/ECC)      | ML-KEM (Kyber)                     |
| :----------------- | :------------------------- | :--------------------------------- |
| **Hard Problem**   | Factoring / Logarithms     | Learning With Errors (LWE)         |
| **Quantum Threat** | Broken by Shor's Algorithm | Resistant to known Quantum attacks |
| **Key Mechanism**  | Mathematical Exponents     | High-dimensional Lattice Vectors   |
| **Error Handling** | Exact math                 | Uses "Noise" and "Rounding"        |

-------------

Prompt: 27 tokens, 12.283 tokens-per-sec
Generation: 1121 tokens, 11.903 tokens-per-sec
Peak memory: 20.037 GB
Speculative decoding: 2.59 accepted tokens/round (1.59 accepted drafts/round, 52.9% of drafted, avg draft 3.00) over 433 rounds
