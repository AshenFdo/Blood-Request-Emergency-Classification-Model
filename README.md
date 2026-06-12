# 🩸 Blood Request Emergency Classification Model

## 🎯 My Goal

I am building a **blood donation mobile application for Sri Lanka**.

Inside the app, people can post blood requests. Some of those requests are **life-threatening emergencies** — a patient is in critical condition and needs blood right now. Others are **routine or planned** needs.

The problem is: **not all requests are equal**, but the app treats them the same way.

So I want to build an **AI model** that reads a blood request description and automatically decides:

> *"Is this an emergency or not?"*

This lets the app **prioritize urgent requests**, alert nearby donors faster, and potentially save lives.

---

## 🗺️ The Big Picture

The app will use **2 AI models**, both built using **transfer learning (fine-tuning)** on top of pre-trained HuggingFace models:

```
Blood Donation App (Sri Lanka)
        │
        ▼
  User posts a blood request
  (description, blood type, location, patient info...)
        │
        ├─────────────────────────────────────────────────────┐
        ▼                                                     ▼
  🤖 Model 1 (This Repo)                          🤖 Model 2 (Planned)
  Emergency Classifier                            Donor Recommender
  ─────────────────────                           ──────────────────
  Reads the description                           Reads the full request
        │                                         (description + blood type
        ├──▶ emergency                             + location + etc.)
        │    → 🚨 Alert nearby donors                      │
        │       immediately                                 ▼
        │                                         Top 10–20 most suitable
        └──▶ not_emergency                        donors recommended
             → 📋 Listed normally
                in the feed
```

> Both models are built using **transfer learning** — taking a pre-trained model from HuggingFace and fine-tuning it on Sri Lanka-specific blood donation data. Model 2 is planned for a future phase.

---

## 🚧 Current Stage

I am currently in the **data & model building phase** — before the app is built.

Here is where I am in the journey:

| Step | Status | What |
|------|--------|------|
| 1. Create dataset | ✅ Done | Built a synthetic dataset of 2,500 Sri Lankan blood request descriptions |
| 2. Upload to HuggingFace | ✅ Done | Publishing dataset to HF Hub for open access |
| 3. Train classifier model | ✅ Done | Fine-tuning a text classification model on the dataset |
| 4. Publish model + demo | 🔜 Next | Push trained model to HF Hub with a simple demo Space |
| 5. Integrate into app | 🔜 Future | Plug the model API into the blood donation mobile app |

---

## 📁 This Repository

This repo contains the work for **steps 2 and 3** — preparing the dataset and training the model.

```
Blood-Request-Emergency-Classification-Model/
│
├── 📓 notebooks/                                                    # All notebooks are created in Google colab
│   ├── Huggingface_blood_request_emegency_datasate_creation.ipynb   # Data set Creation
│   └── 02_model_training.ipynb        # Fine-tuning the classifier
│
├── 📁 data/
│   └── data.csv                       # Synthetic dataset (2,500 samples)
├── 📁 src/                            # APIs
|
|
├── 📄 README.md
└── 📄 requirements.txt
```
## Notebook links
* Huggingface_blood_request_emegency_datasate_creation: [`google-colab`](https://colab.research.google.com/drive/1uiqyCGHtfWJzFPcuxpIib2Mfk8sj1DFC?usp=sharing)
---

## 📊 The Dataset

- **2,500** blood request descriptions
- **Balanced** — 1,250 emergency, 1,250 not emergency
- **Sri Lanka only** — references real Sri Lankan hospitals and cities
- **Synthetic** — AI-generated to bootstrap the model before real data is available
- **Published on HuggingFace →** [`AshenFdo/synthetic_blood_request_urgency_dataset`](https://huggingface.co/datasets/AshenFdo/synthetic_blood_request_urgency_dataset)

---

## 🤖 The Model

This is **not built from scratch**. Instead, I take a pre-trained transformer model from HuggingFace and **fine-tune it** on my dataset using transfer learning. This approach is faster, requires less data, and produces better results than training from zero.

- **Technique:** Transfer learning (fine-tuning a HuggingFace pre-trained model)
- **Task:** Binary text classification
- **Input:** A blood request description (plain text)
- **Output:** `emergency` or `not_emergency`
- **Training environment:** Google Colab (GPU)

---

## 🔮 What's Next

**Model 1 (This repo):**
- [ ] Complete fine-tuning and evaluation
- [ ] Push trained model to HuggingFace Hub
- [ ] Build a simple HuggingFace Space for live demo

**Model 2 (Planned — separate repo):**
- [ ] Create dataset for donor recommendation
- [ ] Fine-tune a pre-trained model to recommend top 10–20 donors based on full request details
- [ ] Publish to HuggingFace Hub

**App:**
- [ ] Integrate both models into the Sri Lanka blood donation mobile app

---

*This is a personal project with a real-world purpose — helping connect blood donors with patients faster, especially in emergencies. 🩸*
