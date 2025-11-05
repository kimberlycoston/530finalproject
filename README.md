CRRT Filter Clotting Prediction

A machine learning project exploring whether CRRT (Continuous Renal Replacement Therapy) circuit clotting can be predicted before it happens — not just detected when the machine is already failing.

This project uses logistic regression and random forest models with physiologic labs and CRRT machine parameters to classify clotting risk and surface the features contributing to that risk.

🔍 Project Goal

Develop an early-warning model to predict CRRT filter clotting in advance, allowing providers to intervene before the circuit occludes, therapy stops, and the patient experiences delays in life-sustaining treatment.

📂 Dataset

Dataset derived from MIMIC-IV and preprocessed into CSVs:

File	Purpose
crrt.csv	Circuit parameters + clotting outcome label
coagulation.csv	Coag labs (INR, PTT, fibrinogen, d-dimer)
complete_blood_count.csv	Platelets, hematocrit
chemistry.csv	Electrolytes (Calcium)
first_day_sofa.csv	stay_id ↔ subject_id/hadm_id mapping

The notebook performs time-alignment to match labs to CRRT events.

🧠 Methods

Models implemented in Python + scikit-learn:

Logistic Regression (primary interpretable baseline)

Random Forest (non-linear model for comparison)

Evaluation metrics:

ROC-AUC

Precision-Recall

Feature importance visualization

✅ Key Findings

Both models performed well; Random Forest achieved strong metrics.

Machine-level CRRT signals (UF rate, filter pressure, system active status, return pressure) dominated feature importance.

Lab values contributed minimally in this pass because the model is currently learning moment-of-failure patterns, not early physiologic changes.

This means the model is accurate — but it's detecting what nurses and machines already see just before clotting, not predicting ahead of time yet.

💡 Interpretation

This behavior is expected in early iterations: the model latched onto highly correlated “end-stage” features (e.g., rising filter pressure).
To move toward true early prediction, we need to:

Remove or time-shift contemporaneous machine variables

Train only on pre-clot window (e.g., 2–6 hours before clot)

Focus on labs, flow rates, anticoagulation parameters

This matches the clinical goal: prevent, not just detect.

🚀 Next Steps

Time-shift features to earlier intervals before clotting events

Re-train with focus on physiologic and flow variables

Consider SHAP for interpretability

Build a simple early-warning interface (Low / Medium / High risk)

Validate with additional real-world CRRT data if available

📁 Repository Structure
.
├── chemistry.csv
├── coagulation.csv
├── complete_blood_count.csv
├── crrt.csv
├── first_day_sofa.csv
├── script.ipynb        
├── Project proposal.docx
├── screenshot1.png
├── screenshot2.png
└── README.md  

🏥 Why It Matters

CRRT interruptions delay therapy, harm critically ill patients, and burden ICU nurses. A predictive model that flags clotting risk before the machine alarms could:

Reduce downtime and filter waste

Prevent avoidable therapy interruptions

Improve nursing workflow and patient safety

Build evidence for explainable AI at the bedside
