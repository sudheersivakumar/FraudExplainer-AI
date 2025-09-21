# FraudExplainer-AI

## 📄 Phase 1: Environment Setup & Synthetic Data Creation
### Goal: Prepare the development environment and generate a synthetic dataset of fraudulent transactions with human-readable explanations.

### ✅ Step 1: Google Colab Setup
#### Created a new notebook
#### Changed runtime to use TPU (v5e-1)

### ✅ Step 2: Install Dependencies
#### Installed all required Python libraries using pip
``` bash
!pip install -q transformers accelerate peft bitsandbytes datasets pandas matplotlib huggingface_hub
```
#### Libraries installed
#### `transformers` — Hugging Face’s core library for models
#### `accelerate` — For multi-device training support
#### `peft` — Parameter-Efficient Fine-Tuning (LoRA)
#### `bitsandbytes`  — For 4-bit quantization (memory efficiency)
#### `datasets`  — For loading and formatting training data
#### `pandas` — For dataset creation and manipulation
#### `matplotlib` — For plotting loss curves later
#### `huggingface_hub` — To log in and access LLaMA 3
> _✅ All installations completed without errors._

### ✅ Step 3: Hugging Face Login
#### Authenticated with Hugging Face Hub to access the LLaMA 3 8B model:
``` bash
from huggingface_hub import login
login(token="hf_xxx...", write_permission=True)
```
> _✅ Authentication successful. Ready to download LLaMA 3 in Phase 2._

### ✅ Step 4: Synthetic Dataset Creation
#### Generated a synthetic dataset of 300 transactions, including:
- 30% flagged as fraudulent (90 rows)
- Each fraudulent transaction includes a human-like, context-rich explanation
- Saved as `fraud_explainer_dataset.csv`
#### 📊 Dataset Schema

| Column             | Description                                      |
|------------------  |--------------------------------------------------|
| `transaction_id`   | Unique ID (1 to 300)                             |
| `amount`           | Transaction amount (random: $5.00 – $5,000.00)   |
| `location`         | One of 10 global cities                          |
| `transaction_type` | Online, ATM, In-Store, or International Transfer |
| `time_of_day`      | Morning, Afternoon, Evening, Night               |
| `is_fraud`         | Binary flag: 1 = Fraud, 0 = Not Fraud            |
| `explanation`      | Human-written reason for fraud (if applicable)   |

#### 📝 Sample Rows
``` bash
transaction_id,amount,location,transaction_type,time_of_day,is_fraud,explanation
1,2134.57,"Mumbai, India","International Transfer","Night",1,"Transaction occurred at an odd hour (Night) in a foreign location (Mumbai, India)."
2,45.30,"Chicago, IL","In-Store","Afternoon",0,
3,3890.22,"Tokyo, Japan","Online Purchase","Morning",1,"Unusually high amount ($3890.22) for this user's profile."
```
> _✅ Dataset successfully generated and validated. Explanations are diverse, realistic, and suitable for instruction fine-tuning._

## 🎯 Phase 1 Deliverables
- ✅ Google Colab notebook configured with TPU
- ✅ All dependencies installed
- ✅ Hugging Face authentication complete
- ✅ `fraud_explainer_dataset.csv` created and saved
- ✅ Dataset previewed and verified for quality
