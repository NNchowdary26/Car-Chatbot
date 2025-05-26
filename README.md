# Car-Chatbot
A chatbot that interacts based on the provided knowledge base
Below is a ready-to-drop-in **README.md** for your GitHub repository.
Copy it into the repo root (or into a new `README.md` file) and commit.

````markdown
# Car Chatbot Demo v2.2 🚗🤖  

A lightweight, pure-Python demo chatbot that answers common **car feature, troubleshooting, and owner-manual questions**.  
It uses local NLP (spaCy + NLTK + RapidFuzz) first, and gracefully falls back to the OpenAI API when the local knowledge base is unsure.

| Quick links |  |
|-------------|--|
| **Colab notebook** | [`Car_Chatbot.ipynb`](Car_Chatbot.ipynb) – one-click cloud demo |
| **Standalone script** | [`car_chatbot_colab_demo_v2.py`](car_chatbot_colab_demo_v2.py) |
| **License** | MIT |
| **Requirements** | Python ≥ 3.8 · spaCy · NLTK · RapidFuzz · NumPy · OpenAI Python SDK |

---

## ✨ Key Features

* **Natural-language Q&A** about adaptive headlights, infotainment, A/C, driver-assist packs, etc.  
* **Fuzzy matching** with RapidFuzz: “AC warm” → “Why is my A/C blowing warm air?”  
* **Local sentiment check** (VADER) to decide when to escalate to the OpenAI model.  
* **Plug-and-play knowledge base** – extend to 1 000 + FAQs with a single list or CSV (see below).  
* Runs **entirely offline** until it needs an answer beyond the local KB.  
* **Colab-ready**: one cell installs everything and starts chatting.

---

## 🚀 Quick Start (Colab)

```python
# In Colab:
!pip -q install spacy nltk rapidfuzz openai numpy
!python -m spacy download en_core_web_sm

# Add your key once per runtime
import os; os.environ["OPENAI_API_KEY"] = "sk-..."

%run car_chatbot_colab_demo_v2.py
bot = CarChatbot()
bot.chat()
````

Hit **Shift + Enter**, ask questions like:

```
You: How do I switch on the adaptive headlights?  
Bot : Headlights swivel with steering angle to illuminate curves.

You: Bluetooth keeps dropping.  
Bot : Try deleting the phone pairing on both devices, then re-pair…
```

---

## 🖥️ Local Setup

```bash
git clone https://github.com/your-handle/car-chatbot.git
cd car-chatbot
python -m venv .venv && source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python car_chatbot_colab_demo_v2.py
```

Set `OPENAI_API_KEY` in your shell **or** export it inside the script/notebook.

---

## 🧠 Growing the Knowledge Base

The demo ships with a concise FAQ list inside `car_chatbot_colab_demo_v2.py`:

```python
FAQS = [
    ("How do I switch on the adaptive headlights?",
     "Headlights swivel with steering angle to illuminate curves."),
    ...
]
```

To scale up to **1 000+ features**:

1. Collect your Q\&A pairs in a **CSV** or **JSON** (`question,answer`).
2. Replace the in-code list with:

```python
import csv, pathlib
KB_PATH = pathlib.Path("knowledge_base.csv")
with KB_PATH.open() as f:
    FAQS = [(row["question"], row["answer"]) for row in csv.DictReader(f)]
```

3. Re-run the script – no other changes required.

The fuzzy-matching and sentiment logic automatically adapts to the larger KB.

---

## 🗂️ Repository Structure

```
.
├─ Car_Chatbot.ipynb        ← One-click Colab demo
├─ car_chatbot_colab_demo_v2.py
├─ requirements.txt
└─ README.md                ← You are here
```

*(Optional files)*
`knowledge_base.csv`, `LICENSE`, GitHub Actions workflow, etc.

---

## 🤝 Contributing

Pull requests are welcome!
Please open an issue first for major changes so we can discuss scope and design.

1. Fork the repo & create your branch: `git checkout -b feature/foo`
2. Format with **Black** and **isort**.
3. Run `pytest` (if you add unit tests).
4. Submit a PR describing the motivation & changes.

---

> *Happy driving – and happy chatting!*

```
