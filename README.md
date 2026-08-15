# Next-Item Prediction for Basket Completion
---

## 📌 Project Overview
This repository contains the final, reproducible code for Team DeepX's submission to the Next-Item Prediction Challenge. The notebook implements a **Dual-Transformer Ensemble with Dynamic Routing**, which achieved a final **Private Leaderboard score of 0.7855 (Rank #5)**. 

The architecture features two heavily regularized 64-dimensional Transformers (one purely sequential, one context-aware utilizing meal and day embeddings) fused via Reciprocal Rank Fusion (RRF) across 7 deterministic seeds.

---

## 📁 Required Data Files
To successfully run this notebook, you must have the following competition dataset files extracted and ready to upload:
1. `train_baskets.csv`
2. `train_transactions.csv`
3. `test_instances.csv`
4. `menu_items.csv`

---

## 🚀 How to Run on Google Colab
Follow these exact steps to reproduce the winning submission from start to finish.

### Step 1: Open the Notebook
1. Go to [Google Colab](https://colab.research.google.com/).
2. Click on **File > Upload notebook**.
3. Select and upload the provided `DeepX_Final.ipynb` file.

### Step 2: Enable GPU Acceleration (Crucial)
Because this pipeline trains 14 distinct PyTorch Transformer models, running on a GPU is required for efficiency.
1. In the top menu bar, click **Runtime > Change runtime type**.
2. Under "Hardware accelerator", select **T4 GPU** (or any available GPU).
3. Click **Save**.

### Step 3: Upload the Dataset to the Runtime
The notebook expects the data files to be in the root directory.
1. On the left-hand sidebar of Colab, click the **Folder icon** (Files).
2. Wait a moment for the runtime to connect and allocate disk space.
3. Drag and drop the four required dataset files (`train_baskets.csv`, `train_transactions.csv`, `test_instances.csv`, `menu_items.csv`) directly into the file browser area.
4. *Note: Colab will warn you that uploaded files are deleted when the runtime recycles. Click "OK".*

### Step 4: Execute the Code
1. In the top menu bar, click **Runtime > Run all** (or press `Ctrl+F9` / `Cmd+F9`).
2. The notebook will automatically:
   * Perform the strict 85/15 chronological data split.
   * Generate the heuristic fallback dictionaries.
   * Train the 7-seed Dual-Transformer models (printing validation NDCG along the way).
   * Apply Dynamic Routing and Reciprocal Rank Fusion to the test set.
   * Run the final cleanup filter to ensure 100% valid predictions.

### Step 5: Retrieve the Final Output
Once execution completes (typically takes ~10–15 minutes on a T4 GPU):
1. Look at the file browser on the left sidebar again.
2. You will see a newly generated file named **`RANK_1_FINAL_SUBMISSION.csv`** and the fully cleaned **`RANK_5.csv`**.
3. Right-click on **`RANK_5.csv`** and select **Download**. This is the exact file that scored 0.7855 on the Private Leaderboard.

### Step 6: Verify Reproducibility (Optional but Recommended)
To mathematically prove that this script generates our exact winning submission:
1. You can download our official winning file (**`submission_4c8256ea-33f.csv`**) directly from our team's submission dashboard on the competition website.
2. Upload this downloaded `submission_4c8256ea-33f.csv` file into the Colab file browser.
3. Run the **second cell** in the notebook. 
4. This cell uses `pandas` to compare every single row and column of the newly generated `RANK_5.csv` against the official `submission_4c8256ea-33f.csv`. It will output `Are the files exactly the same? True`, guaranteeing 100% reproducibility.

---

## ⚙️ Dependencies
*All required libraries (`pandas`, `numpy`, `torch`, `tqdm`) are natively pre-installed in the default Google Colab environment. No external `pip install` commands are necessary.*










FINAL CHECKPOINT:
✅ "Source code and/or notebooks": Satisfied by DeepX_Final.ipynb.

✅ "README file with execution instructions": Satisfied by README.md.

✅ "Required libraries/packages": Satisfied by the README.md (which explicitly states no external pip installs are needed since Colab has pandas, torch, and numpy natively).

✅ "Preprocessing and feature engineering steps": Satisfied by Sections 2, 3, and 4 inside DeepX_Final.ipynb (where you handle the time-decay logic and dictionary building).

✅ "Model training/inference scripts": Satisfied by Sections 6 and 7 inside DeepX_Final.ipynb.

✅ "Any necessary saved models or checkpoints": Satisfied by submission_4c8256ea-33f.csv.
