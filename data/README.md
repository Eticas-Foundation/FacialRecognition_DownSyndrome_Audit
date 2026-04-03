# Data

This directory contains three datasets reconstructed from the published audit findings. No raw images or individual-level biometric data are included or available — see Limitations below.

---

## azul-aggregate-results.csv

**Provenance:** Aggregate statistics reported in the audit report (Section 3.2). The Azul testing was conducted with 40 participants recruited through Cedown Jerez (DS group, n=20) and a control group (NoDS, n=20). Eticas researchers observed each participant's session with Azul and recorded its outputs for age, BMI, and smoking status, comparing these against actual values.

**Structure:** Long-format table with one row per reported statistic.

| Field | Description |
|---|---|
| `metric` | Category of measurement (e.g. `sample_size`, `age_error`, `bmi_error`) |
| `variable` | Specific variable within the metric |
| `group` | `DS` (Down Syndrome) or `NoDS` (control) |
| `value` | Numeric value (where applicable) |
| `unit` | Unit of measurement |
| `source_note` | Contextual note from the audit report |

---

## deepface-dataset-composition.csv

**Provenance:** Dataset characteristics described in Section 3.3 and the Phase I Technical Note. Images were collected from the internet and manually labelled by the Eticas research team. Ethnicity labels were derived from search terms; age from Wikipedia/IMDb; gender and emotion manually assigned from visual inspection.

**Structure:** One row per dataset × attribute × category combination.

| Field | Description |
|---|---|
| `dataset` | `DS` (60 images of individuals with Down Syndrome) or `NoDS` (60 images of public figures without DS) |
| `attribute` | Attribute being described (e.g. `gender`, `ethnicity`, `emotion`, `age_range`) |
| `category` | Sub-category (e.g. `male`, `female`, `Asian`) |
| `count` | Number of images in this category |
| `notes` | Additional context |

---

## deepface-results.csv

**Provenance:** Classification results from running the DeepFace framework (Serengil & Ozpinar) across both datasets. Full metric tables extracted from `Deep Face analysis.pdf` (Phase I fieldwork analyses). Results cover gender, emotion, ethnicity, and age prediction tasks, including intersectional breakdowns by gender × ethnicity and gender × emotion.

**Structure:** Long-format table with one row per metric × task × group × subgroup combination.

| Field | Description |
|---|---|
| `task` | Classification task: `gender`, `emotion`, `ethnicity`, `age`, `gender_x_ethnicity`, `ethnicity_x_gender`, `gender_x_emotion` |
| `metric` | Metric type: `accuracy`, `recall`, `false_positive_rate`, `mean_absolute_error`, `mean_confidence_true_label`, etc. |
| `group` | `DS` or `NoDS` |
| `subgroup` | Demographic subgroup (gender, ethnicity, emotion category), or blank for overall metrics |
| `value` | Numeric metric value |
| `notes` | Calculation basis and interpretive notes |

---

## What Is NOT in This Repository

### Raw images
The two DeepFace test datasets (120 images total) are not included. The DS dataset contains images of identifiable individuals with Down Syndrome sourced from the internet. The NoDS dataset contains images of public figures. Neither dataset is redistributed here. Researchers wishing to replicate the study should compile equivalent datasets following the composition described in `deepface-dataset-composition.csv`.

### Individual Azul session recordings
Individual participant data from the Azul testing (age, BMI, smoking outputs per person) was not retained in a structured format. The audit report presents aggregate and illustrative statistics only. The raw session data, to the extent it existed, would be subject to GDPR and the informed consent agreements signed with participants.

### Smoking classification results
Insufficient smokers in the DS sample (n=1) precluded any analysis of smoking classification accuracy for that group.

---

## Limitations

- The Azul sample (N=40) is small and not population-representative. Results are illustrative.
- The DeepFace image datasets are not random samples. The DS dataset draws from internet-available images, which may skew toward certain age ranges, expressions, and contexts. The NoDS dataset of public figures is not demographically representative of the general population.
- Emotion labels were assigned manually by the research team based on visual inspection — a subjective process.
- Ethnicity labels were derived from internet search terms, representing oversimplified categories. The DeepFace framework's six ethnicity classes (Asian, Black, Indian, Latino Hispanic, Middle Eastern, White) do not reflect the full complexity of ethnic identity.
- DeepFace version and exact model weights used are not specified in the original analysis documents.

---

## Collaboration Agreements

A signed collaboration agreement (`Acuerdo cooperación CDOWN_signedEDS.pdf`, April 2023) between Eticas and CEDOWN Jerez governs the DS participant data. Informed consent forms in Spanish (`Consentimiento Informado SP.docx`) and English (`Informed consent EN.docx`) were used with all participants. These documents are held on Eticas's internal SharePoint.
