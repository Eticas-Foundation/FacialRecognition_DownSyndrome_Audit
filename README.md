# Adversarial Audit: Facial Recognition & Down Syndrome

**Eticas Foundation** | Adversarial Audit  
**Published:** August 2023  
**Report title:** *Invisible No More: The Impact of Facial Recognition on People with Disabilities*  
**Systems audited:** Azul (Zurich Insurance Group) · DeepFace framework (Serengil & Ozpinar)  
**Community partner:** Cedown Jerez (DS participant recruitment)

---

## Overview

This repository contains the datasets and reproducible analysis code supporting Eticas Foundation's adversarial audit of facial recognition technology as applied to individuals with Down Syndrome (DS). The audit examined two systems:

1. **Azul by Zurich Insurance Group** — a live FR system that estimates age, BMI, and smoking status from a webcam feed to generate insurance quotes. Tested with 40 participants (20 DS, 20 without DS).

2. **DeepFace** — an open-source Python facial attribute analysis framework. Tested against two curated image datasets (60 DS images, 60 non-DS images) balanced by gender and ethnicity across six categories.

The audit found systematic and statistically meaningful disparities in FR performance for individuals with DS, particularly for women and for intersectional subgroups of DS women of colour.

---

## Repository Structure

```
.
├── data/
│   ├── azul-aggregate-results.csv         # Group-level Azul test statistics (age, BMI, smoking)
│   ├── deepface-dataset-composition.csv   # Image dataset composition (gender, ethnicity, emotion)
│   ├── deepface-results.csv               # Full DeepFace performance metrics (accuracy, recall, MAE, fairness)
│   └── README.md                          # Data provenance, field definitions, limitations
│
├── analysis/
│   └── audit_analysis.ipynb              # Reproducible Python analysis notebook (8 figures)
│
└── README.md
```

---

## Key Findings

### Azul (live testing, N=40)

| Metric | DS group | NoDS group | Disparity |
|---|---|---|---|
| Age MAE | 7.19 years | 4.45 years | +62% higher error |
| Age deviation range | −14 to +21 years | −9 to +18 years | Wider and directionally biased |
| BMI MAE | 3.82 kg/m² | 2.98 kg/m² | +28% higher error |
| Age bias (women, DS) | Severely underestimated | — | Predicted as low as 5–8 years old |
| Age bias (men, DS) | Overestimated | — | Overestimated by up to 12 years |

The underestimation of DS women's ages to the point of predicting them as minors raises serious legal and ethical concerns about compliance with contractual age restrictions.

### DeepFace (image datasets, N=120)

| Task | DS dataset | NoDS dataset | Reported benchmark |
|---|---|---|---|
| Gender accuracy | 71.7% | 97.4% | 97.44% |
| Gender recall — women | 43.3% | 80.0% | — |
| Gender recall — men | 100% | 100% | — |
| Ethnicity accuracy | 38.3% | 66.7% | 68% |
| Emotion accuracy | 56.7% | 58.3% | 57% |
| Age MAE | ±10.583 years | ±9.167 years | ±4.65 years |

**Intersectional findings:** Asian DS women had 0% correct gender classification. White DS women had the highest recall among DS women (83%). Middle Eastern and South Asian DS men had the lowest ethnicity classification accuracy.

---

## Running the Analysis

Requires Python 3.9+ and:

```bash
pip install pandas matplotlib numpy jupyter
```

Run the notebook:

```bash
jupyter notebook analysis/audit_analysis.ipynb
```

The notebook generates 8 figures covering sample composition, error distributions, gender and ethnicity classification performance, intersectional breakdowns, and a complete summary table.

---

## Data Notes

- Raw images from both DeepFace test datasets are **not included** — the DS dataset contains images of identifiable individuals; the NoDS dataset contains images of public figures. Researchers wishing to replicate should compile equivalent datasets per the composition in `data/deepface-dataset-composition.csv`.
- Individual Azul session data is **not available** in structured form. The audit report presents aggregate and illustrative statistics only.
- A signed collaboration agreement with Cedown Jerez (April 2023) and informed consent forms govern DS participant data. These are held on Eticas's internal SharePoint.

See `data/README.md` for full provenance, field definitions, and limitations.

---

## Team

**Project Lead & Research Director:** Dr. Gemma Galdon-Clavell, Founder of Eticas  
**Researchers:** Matteo Mastracci (Team Leader), Miguel Azores (Ethics & Technology Researcher)  
**Contributors:** Luis Rodrigo González Vizuet, Iliyana Nalbantova, Fran Segarra, Isabela Miranda, Sam Danello, Patricia Vázquez, Mireia Orra  
**Community partner:** Cedown Jerez

---

## License

The audit report is © Eticas Foundation (2023). The datasets and analysis code in this repository are released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Attribution required: *Eticas Foundation, "Invisible No More: The Impact of Facial Recognition on People with Disabilities," 2023.*
