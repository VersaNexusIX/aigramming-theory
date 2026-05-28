# 02 - Core Concepts of Aigramming

## 2.1 Definition

**Aigramming** is a programming paradigm in which the fundamental unit of program instruction is a natural language prompt, interpreted by an artificial intelligence model running locally on the device. This paradigm positions the AI model as the runtime layer, supplanting the role previously occupied by an interpreter or virtual machine.

---

## 2.2 File Structure

### 2.2.1 File Extensions

File extensions within the Aigramming ecosystem reflect the AI model serving as the interpreter. The projected conventions are as follows:

| Extension | Runtime Model | Description |
|---|---|---|
| `.gpt` | GPT-family runtime | Interpreted by a GPT-based model |
| `.gemini` | Gemini runtime | Interpreted by a local Gemini model |
| `.llama` | LLaMA runtime | Interpreted by a LLaMA model |
| `.claude` | Claude runtime | Interpreted by a Claude model |

This extension convention is analogous to the `.py` extension indicating that a file is to be interpreted by the Python runtime, or `.js` indicating a JavaScript engine.

### 2.2.2 File Content Format

The contents of an Aigramming file consist of plain natural language text. The file can be read using standard utilities such as `cat`, `less`, or any plain text editor.

A hypothetical example of the contents of a file named `hello.gpt`:

```
Display a welcome message to the user.
Ask for their name.
Store the name and use it in every subsequent interaction throughout the session.
```

By way of conceptual comparison: executing `cat` on a compiled object file `.o` in the context of C produces a binary representation that is not readily human-readable. In Aigramming, the result is a fully readable prompt; however, the underlying "execution logic" remains concealed within the weights of the AI model.

---

## 2.3 Ecosystem Components

### 2.3.1 AI Runtime

The AI Runtime is the core component, functioning in a capacity equivalent to an interpreter or virtual machine. It is a locally running AI model that accepts prompts as input and executes the corresponding instructions within an actual computational context.

Principal requirements of an AI Runtime:
- Operates entirely offline without network dependency for execution.
- Possesses the capability to access the operating system, file system, and required hardware interfaces.
- Exhibits deterministic or semi-deterministic behavior to support testing and reproducibility requirements.

### 2.3.2 Aigram Package Manager

Analogous to `pip`, `npm`, or `cargo`, the Aigramming ecosystem requires dependency management for:
- AI runtime models of varying versions.
- Reusable prompt libraries that can be imported across projects.
- Context configurations and runtime-specific constraints.

### 2.3.3 Aigram Debugger

Debugging within Aigramming presents unique challenges. Because execution logic is not deterministic in the traditional sense, a debugger must be capable of:
- Recording an execution trace of the runtime's interpretive process.
- Providing inspection of the contextual state the model used when executing instructions.
- Enabling execution replay under identical contextual parameters.

---

## 2.4 Development Paradigm

### 2.4.1 Prompt Engineering as Programming

In Aigramming, the primary competency of a developer shifts from mastery of formal language syntax toward the ability to craft prompts that are precise, consistent, and free of unintended ambiguity.

This does not imply that programming becomes fundamentally simpler. Complexity shifts rather than disappears. Designing prompts that produce deterministic, predictable behavior across diverse input conditions represents a significant technical challenge.

### 2.4.2 Versioning and Reproducibility

Among the most substantial challenges in Aigramming is reproducibility. An identical program may produce different outputs across different model versions, even when the prompt itself is unchanged. Consequently, runtime model versioning assumes an importance equivalent to that of source code versioning.

An `aigram.lock` file, analogous to `package-lock.json` or `Cargo.lock`, would store:
- The precise version of the runtime model in use.
- A hash of the model weights for integrity verification.
- The inference parameters applied during execution.

### 2.4.3 Testing

Unit testing in Aigramming cannot rely exclusively on simple deterministic assertions. Projected testing approaches include:
- **Behavioral testing**: Verifying whether output satisfies defined behavioral criteria rather than character-for-character equivalence.
- **Semantic assertion**: Verifying whether the meaning of the output conforms to expectations rather than its exact format.
- **Boundary testing**: Examining behavior at edge inputs that may induce ambiguous interpretation by the runtime.

---

## 2.5 Paradigm Comparison Example

Task: Read a text file and display only the lines containing a specific word.

**Python (Interpreted):**
```python
with open("data.txt") as f:
    for line in f:
        if "word" in line:
            print(line)
```

**Aigramming (Hypothetical, `search.gpt`):**
```
Open the file data.txt.
Read each line.
Display only the lines containing the word "word".
```

The two approaches are functionally equivalent. However, in the Aigramming version, there is no formal syntax, no explicit error handling within the code, and the behavior under edge conditions, such as a missing file or an invalid encoding, depends entirely on how the AI runtime interprets the instructions given the available context.
