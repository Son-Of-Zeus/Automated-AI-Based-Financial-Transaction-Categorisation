# Autonomous Neuro-Symbolic System for Financial Transaction Categorisation

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Son-Of-Zeus/Automated-AI-Based-Financial-Transaction-Categorisation/blob/main/AI_Based_Transaction_Categorisation_System.ipynb)

A robust, offline-capable AI pipeline designed for high-accuracy categorization of raw financial transaction strings. This solution directly addresses the GHCI Hackathon requirement for a **standalone, high-performance system** by eliminating dependency on external, expensive, and latency-prone third-party APIs. It provides a secure, on-premise alternative for Personal Financial Management (PFM) and Fintech applications.

---

## Key Features and Architecture

The core of the system is a novel **Neuro-Symbolic Architecture** that fuses three distinct layers of intelligence to achieve optimal balance between speed, precision, and generalization.

### 1. Symbolic Engine (Precision Layer)
* **Mechanism:** A deterministic, YAML-configurable rule set **`config.yaml`** that performs exact keyword matching.
* **Role:** Provides **zero-latency, 100\% confident** classification for known, high-volume merchants (e.g., any string containing "SWIGGY" is instantly categorized as "Food & Dining").

### 2. Graph Context (Memory Layer)
* **Mechanism:** A persistent NetworkX graph (`graph.pkl`) that stores learned associations between merchant tokens (extracted via Regex) and their historical category.
* **Role:** Enables the system to instantly recognize recurrent transactions and learn customer-specific habits, improving performance on local or unbranded vendors.

### 3. Neural Engine (Generalization Layer)
* **Mechanism:** A local Sentence Transformer model (`all-mpnet-base-v2`) integrated with a **FAISS Vector Index** for rapid semantic similarity search.
* **Role:** Handles the "Cold Start" problem. It categorizes completely new or obfuscated merchant names (e.g., "The Gourmet Shop") by mapping their meaning to the closest category description ("Groceries").

---

## Innovation Highlights

### Active Learning: Human-in-the-Loop
The system incorporates an essential **Active Learning** feedback loop using interactive widgets.
1.  When the model’s prediction confidence falls below a threshold, the user is prompted for a correction.
2.  The system instantly updates its **Symbolic Rule Set** (`config.yaml`) and **Graph Context** (`graph.pkl`) on the disk.
3.  This means the system permanently "learns" from every human correction, dramatically improving accuracy for all future transactions without ever requiring a full model retraining.

### Ethical AI Audit
A proactive `check_bias_coverage` function is included to assess the diversity of the trained model's knowledge base. This ensures the taxonomy and data are not skewed towards only urban/premium brands (like Starbucks), and has adequate coverage for the unorganized retail sector (e.g., "Kirana", "General Store"), addressing inclusivity requirements.

---

## Getting Started

The fastest way to test the solution is to click the **"Open in Colab"** badge at the top of this README.

### Repository Structure
| File | Description |
| :--- | :--- |
| `AI_Based_Transaction_Categorisation_System.ipynb` | The main executable notebook containing all code, interactive widgets, and evaluation steps. |
| `config.yaml` | The core category taxonomy and initial keyword mapping (user-editable). |
| `graph.pkl` | The serialized, persistent state of the Graph Context model (auto-generated). |
| `requirements.txt` | List of Python dependencies for a local setup. |

### Local Setup
For a local development environment:
```bash
# Clone the repository
git clone [https://github.com/Son-Of-Zeus/Automated-AI-Based-Financial-Transaction-Categorisation.git](https://github.com/Son-Of-Zeus/Automated-AI-Based-Financial-Transaction-Categorisation.git)
cd Automated-AI-Based-Financial-Transaction-Categorisation

# Install dependencies 
# Note: Ensure you use the right FAISS version (faiss-cpu or faiss-gpu)
pip install -r requirements.txt

# Run the notebook environment 
jupyter lab AI_Based_Transaction_Categorisation_System.ipynb
