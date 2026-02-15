# DEMO SCENARIOS & SYNTHETIC PATIENT DATA

This document contains 5 realistic patient scenarios for demonstrating the Clinical Copilot MVP.

---

## SCENARIO 1: ACUTE CORONARY SYNDROME (Primary Demo)

### Patient Profile
```json
{
  "patient_id": "DEMO-001",
  "demographics": {
    "age": 45,
    "gender": "Male",
    "race": "Caucasian",
    "ethnicity": "Non-Hispanic"
  },
  "chief_complaint": "Chest pain, shortness of breath, sweating",
  "symptoms": [
    {
      "name": "Chest pain",
      "onset": "30 minutes ago",
      "characteristics": "Substernal, pressure-like, radiating to left arm",
      "severity": 8,
      "duration": "Ongoing"
    },
    {
      "name": "Dyspnea",
      "onset": "30 minutes ago",
      "severity": 7
    },
    {
      "name": "Diaphoresis",
      "onset": "30 minutes ago",
      "severity": 6
    }
  ],
  "medical_history": {
    "conditions": [
      {"name": "Hypertension", "icd10": "I10", "status": "active"},
      {"name": "Hyperlipidemia", "icd10": "E78.5", "status": "active"}
    ],
    "family_history": ["Father had MI at age 52"]
  },
  "current_medications": [
    {"name": "Lisinopril", "dosage": "10mg", "frequency": "daily"},
    {"name": "Atorvastatin", "dosage": "40mg", "frequency": "daily"}
  ],
  "vital_signs": {
    "blood_pressure": "150/95",
    "heart_rate": 105,
    "respiratory_rate": 22,
    "oxygen_saturation": 94,
    "temperature": 98.6
  },
  "allergies": ["None known"]
}
```


### Expected AI Response

**Differential Diagnosis**:
1. Acute Coronary Syndrome (78% confidence)
   - Supporting: chest pain, dyspnea, diaphoresis, age, male, HTN, hyperlipidemia
   - Risk factors: Family history, cardiovascular risk factors
   
2. Pulmonary Embolism (12% confidence)
   - Supporting: dyspnea, chest pain
   - Against: No leg swelling, no recent immobilization, no travel
   
3. GERD (7% confidence)
   - Supporting: chest pain
   - Against: Acute onset, exertional, with diaphoresis and dyspnea
   
4. Panic Attack (3% confidence)
   - Against: No psychiatric history, physical exertion trigger, cardiovascular risk factors

**Recommended Actions**:
- 🔴 URGENT: Immediate ECG, troponin I/T, aspirin 325mg
- 📋 Order: CBC, BMP, chest X-ray, lipid panel
- ⚠️ Monitor: Continuous cardiac monitoring, oxygen therapy
- 🚑 Prepare: Cardiac catheterization lab on standby

**Evidence Sources**:
- AHA/ACC Chest Pain Guidelines (2021)
- JAMA: Acute Coronary Syndrome Diagnosis (2023)
- UpToDate: Evaluation of Chest Pain in Adults
- Framingham Risk Score Calculator

**Demo Notes**:
- This is the PRIMARY demo scenario
- Shows high confidence (78%) with clear reasoning
- Demonstrates drug interaction checking (safe with current meds)
- Highlights explainability with evidence citations

---

## SCENARIO 2: COMMUNITY-ACQUIRED PNEUMONIA


### Patient Profile
```json
{
  "patient_id": "DEMO-002",
  "demographics": {
    "age": 68,
    "gender": "Female",
    "race": "African American",
    "ethnicity": "Non-Hispanic"
  },
  "chief_complaint": "Cough, fever, difficulty breathing for 3 days",
  "symptoms": [
    {
      "name": "Productive cough",
      "onset": "3 days ago",
      "characteristics": "Yellow-green sputum",
      "severity": 7
    },
    {
      "name": "Fever",
      "onset": "3 days ago",
      "severity": 8,
      "max_temp": 102.5
    },
    {
      "name": "Dyspnea",
      "onset": "2 days ago",
      "severity": 6,
      "characteristics": "Worse with exertion"
    },
    {
      "name": "Pleuritic chest pain",
      "onset": "1 day ago",
      "severity": 5
    }
  ],
  "medical_history": {
    "conditions": [
      {"name": "Type 2 Diabetes", "icd10": "E11.9", "status": "active"},
      {"name": "COPD", "icd10": "J44.9", "status": "active"}
    ]
  },
  "current_medications": [
    {"name": "Metformin", "dosage": "1000mg", "frequency": "twice daily"},
    {"name": "Albuterol inhaler", "dosage": "2 puffs", "frequency": "as needed"}
  ],
  "vital_signs": {
    "blood_pressure": "135/82",
    "heart_rate": 98,
    "respiratory_rate": 24,
    "oxygen_saturation": 89,
    "temperature": 101.8
  },
  "social_history": {
    "smoking": "Former smoker, quit 5 years ago, 30 pack-year history"
  }
}
```

### Expected AI Response

**Differential Diagnosis**:
1. Community-Acquired Pneumonia (85% confidence)
2. COPD Exacerbation (10% confidence)
3. Influenza (3% confidence)
4. Lung Cancer (2% confidence - low probability but consider given smoking history)

**Recommended Actions**:
- Chest X-ray (PA and lateral)
- Sputum culture and Gram stain
- Blood cultures x2
- CBC with differential, BMP
- Antibiotics: Ceftriaxone + Azithromycin (per IDSA guidelines)
- Oxygen therapy to maintain SpO2 >90%

**Demo Notes**:
- Shows handling of comorbidities (diabetes, COPD)
- Demonstrates consideration of social history (smoking)
- Lower oxygen saturation triggers appropriate urgency

---

## SCENARIO 3: DIABETIC KETOACIDOSIS

### Patient Profile
```json
{
  "patient_id": "DEMO-003",
  "demographics": {
    "age": 22,
    "gender": "Female",
    "race": "Hispanic",
    "ethnicity": "Hispanic"
  },
  "chief_complaint": "Nausea, vomiting, abdominal pain, confusion",
  "symptoms": [
    {
      "name": "Nausea and vomiting",
      "onset": "24 hours ago",
      "severity": 8,
      "frequency": "Multiple episodes"
    },
    {
      "name": "Abdominal pain",
      "onset": "24 hours ago",
      "severity": 7,
      "characteristics": "Diffuse, cramping"
    },
    {
      "name": "Polyuria",
      "onset": "3 days ago",
      "severity": 6
    },
    {
      "name": "Polydipsia",
      "onset": "3 days ago",
      "severity": 6
    },
    {
      "name": "Altered mental status",
      "onset": "6 hours ago",
      "severity": 7,
      "characteristics": "Lethargic, confused"
    }
  ],
  "medical_history": {
    "conditions": [
      {"name": "Type 1 Diabetes", "icd10": "E10.9", "status": "active", "onset": "Age 12"}
    ]
  },
  "current_medications": [
    {"name": "Insulin glargine", "dosage": "20 units", "frequency": "bedtime"},
    {"name": "Insulin lispro", "dosage": "Variable", "frequency": "with meals"}
  ],
  "vital_signs": {
    "blood_pressure": "95/60",
    "heart_rate": 120,
    "respiratory_rate": 28,
    "oxygen_saturation": 98,
    "temperature": 98.2
  },
  "recent_history": "Patient reports missing insulin doses for 2 days due to illness"
}
```

### Expected AI Response

**Differential Diagnosis**:
1. Diabetic Ketoacidosis (92% confidence)
2. Gastroenteritis (5% confidence)
3. Sepsis (2% confidence)
4. Acute Pancreatitis (1% confidence)

**Recommended Actions**:
- 🔴 CRITICAL: Immediate BMP, glucose, venous blood gas, beta-hydroxybutyrate, urinalysis
- IV fluid resuscitation (0.9% NaCl)
- Insulin infusion protocol
- Potassium monitoring and replacement
- ICU admission
- Search for precipitating cause (infection, MI, medication non-compliance)

**Evidence Sources**:
- ADA Guidelines for DKA Management
- Endocrine Society Clinical Practice Guidelines

**Demo Notes**:
- Shows recognition of life-threatening condition (92% confidence)
- Demonstrates understanding of medication non-compliance as trigger
- Highlights need for ICU-level care

---

## SCENARIO 4: MIGRAINE HEADACHE

### Patient Profile
```json
{
  "patient_id": "DEMO-004",
  "demographics": {
    "age": 32,
    "gender": "Female",
    "race": "Asian",
    "ethnicity": "Non-Hispanic"
  },
  "chief_complaint": "Severe headache with visual changes",
  "symptoms": [
    {
      "name": "Headache",
      "onset": "2 hours ago",
      "severity": 9,
      "characteristics": "Unilateral, throbbing, left temporal",
      "duration": "Ongoing"
    },
    {
      "name": "Visual aura",
      "onset": "30 minutes before headache",
      "characteristics": "Zigzag lines, flashing lights",
      "duration": "20 minutes"
    },
    {
      "name": "Photophobia",
      "severity": 8
    },
    {
      "name": "Phonophobia",
      "severity": 7
    },
    {
      "name": "Nausea",
      "severity": 6
    }
  ],
  "medical_history": {
    "conditions": [
      {"name": "Migraine with aura", "icd10": "G43.1", "status": "active", "onset": "Age 18"}
    ],
    "family_history": ["Mother has migraines"]
  },
  "current_medications": [
    {"name": "Sumatriptan", "dosage": "50mg", "frequency": "as needed for migraine"}
  ],
  "vital_signs": {
    "blood_pressure": "118/75",
    "heart_rate": 78,
    "respiratory_rate": 16,
    "oxygen_saturation": 99,
    "temperature": 98.4
  },
  "recent_history": "Patient reports increased stress at work, missed meals today"
}
```

### Expected AI Response

**Differential Diagnosis**:
1. Migraine with Aura (88% confidence)
2. Tension Headache (7% confidence)
3. Cluster Headache (3% confidence)
4. Intracranial Hemorrhage (2% confidence - low but rule out given severity)

**Recommended Actions**:
- Sumatriptan 50mg PO (patient's usual medication)
- Antiemetic: Metoclopramide 10mg IV
- IV fluids for hydration
- Dark, quiet room
- Neurological exam to rule out red flags
- Consider CT head if atypical features or first severe headache

**Red Flags to Monitor**:
- Sudden onset ("thunderclap")
- Fever or neck stiffness
- Focal neurological deficits
- Change in mental status

**Demo Notes**:
- Shows recognition of classic migraine pattern
- Demonstrates appropriate use of patient's existing medication
- Highlights red flag monitoring (safety-focused)
- Lower confidence triggers consideration of serious alternatives

---

## SCENARIO 5: URINARY TRACT INFECTION

### Patient Profile
```json
{
  "patient_id": "DEMO-005",
  "demographics": {
    "age": 58,
    "gender": "Female",
    "race": "Caucasian",
    "ethnicity": "Non-Hispanic"
  },
  "chief_complaint": "Burning with urination, frequent urination, lower abdominal pain",
  "symptoms": [
    {
      "name": "Dysuria",
      "onset": "2 days ago",
      "severity": 7,
      "characteristics": "Burning sensation"
    },
    {
      "name": "Urinary frequency",
      "onset": "2 days ago",
      "severity": 6,
      "characteristics": "Every 30-60 minutes"
    },
    {
      "name": "Urinary urgency",
      "onset": "2 days ago",
      "severity": 7
    },
    {
      "name": "Suprapubic pain",
      "onset": "1 day ago",
      "severity": 5
    },
    {
      "name": "Hematuria",
      "onset": "1 day ago",
      "characteristics": "Pink-tinged urine"
    }
  ],
  "medical_history": {
    "conditions": [
      {"name": "Recurrent UTIs", "status": "active", "note": "3 episodes in past year"},
      {"name": "Postmenopausal", "status": "active"}
    ]
  },
  "current_medications": [
    {"name": "Multivitamin", "frequency": "daily"}
  ],
  "vital_signs": {
    "blood_pressure": "128/78",
    "heart_rate": 82,
    "respiratory_rate": 16,
    "oxygen_saturation": 99,
    "temperature": 99.2
  },
  "allergies": ["Sulfa drugs (rash)"]
}
```

### Expected AI Response

**Differential Diagnosis**:
1. Acute Cystitis (UTI) (90% confidence)
2. Pyelonephritis (6% confidence - monitor for fever, flank pain)
3. Interstitial Cystitis (3% confidence)
4. Bladder Cancer (1% confidence - consider given recurrent UTIs and hematuria)

**Recommended Actions**:
- Urinalysis with microscopy
- Urine culture and sensitivity
- Antibiotics: Nitrofurantoin 100mg BID x 5 days (avoid sulfa due to allergy)
- Alternative: Ciprofloxacin 250mg BID x 3 days
- Increase fluid intake
- Consider post-menopausal vaginal estrogen for prevention

**Drug Interaction Check**:
- ⚠️ ALLERGY ALERT: Patient allergic to sulfa drugs
- ✓ Nitrofurantoin is safe alternative
- ✓ No interactions with current medications

**Follow-up**:
- If symptoms persist >48 hours, consider pyelonephritis
- Urology referral if >3 UTIs per year (already met criteria)
- Consider imaging if recurrent infections continue

**Demo Notes**:
- Shows drug allergy checking (critical safety feature)
- Demonstrates consideration of recurrent pattern
- Highlights appropriate antibiotic selection
- Mentions cancer screening (thorough differential)

---

## DEMO SCRIPT INTEGRATION

### How to Use These Scenarios

**Primary Demo (Scenario 1 - ACS)**:
- Use for main presentation (5-minute pitch)
- Shows high-stakes, time-critical decision
- Demonstrates explainability and confidence scoring
- Highlights drug interaction checking

**Backup Scenarios (2-5)**:
- Use for Q&A or extended demos
- Show breadth of capabilities
- Demonstrate handling of different patient populations
- Highlight safety features (allergies, red flags)

### Demo Flow Template

1. **Setup** (10 seconds)
   - "Let me show you a real clinical scenario"
   - Display patient demographics

2. **Input** (15 seconds)
   - Enter chief complaint
   - Select symptoms
   - Add medical history

3. **Processing** (5 seconds)
   - Show real-time RAG retrieval
   - Visualize knowledge sources being queried

4. **Results** (30 seconds)
   - Display differential diagnosis with confidence
   - Show recommended actions
   - Highlight drug interaction check

5. **Explainability** (30 seconds)
   - Click "Explain" button
   - Show reasoning steps
   - Display evidence citations
   - Demonstrate confidence breakdown

6. **Wow Factor** (10 seconds)
   - "All of this in 2 seconds"
   - "With full explainability"
   - "And it's learning from every interaction"

---

## SYNTHETIC DATA GENERATION NOTES

### For MVP Implementation

**Clinical Guidelines to Index**:
- AHA/ACC Chest Pain Guidelines
- IDSA Pneumonia Guidelines
- ADA Diabetes/DKA Guidelines
- American Headache Society Migraine Guidelines
- IDSA UTI Guidelines

**PubMed Articles to Index** (sample):
- Recent systematic reviews for each condition
- High-impact RCTs
- Meta-analyses
- Clinical decision rules (HEART score, CURB-65, etc.)

**Drug Database Entries**:
- Common medications for each scenario
- Drug-drug interactions
- Drug-allergy contraindications
- Dosing guidelines

**Expected Response Times**:
- Query processing: <500ms
- Vector retrieval: <200ms
- LLM generation: <1000ms
- Total: <2 seconds (target)

---

## TESTING CHECKLIST

Before demo:
- [ ] All 5 scenarios tested end-to-end
- [ ] Confidence scores reasonable (70-95% for clear cases)
- [ ] Evidence citations working (clickable links)
- [ ] Drug interaction checking functional
- [ ] Allergy alerts triggering correctly
- [ ] Explanation generation working
- [ ] Response times <2 seconds
- [ ] UI displaying correctly
- [ ] No errors or crashes

