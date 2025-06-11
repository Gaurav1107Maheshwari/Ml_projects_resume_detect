# Ml_projects_resume_detect
Projects: AI-Powered Resume Ranker &amp;&amp; Credit Card Fraud Detection
# Semantic Resume Screening Project

## Introduction

This project implements an automated resume screening system using semantic similarity models. The goal is to efficiently match candidate resumes to a job description, ranking them by relevance for data-driven and fair shortlisting.

## Objectives

- Automatically screen and rank resumes based on semantic similarity to a job description.
- Extract and display skill matches for transparency.
- Export top candidates and provide a visual summary of scores.

## Dataset

- **Source:** `/kaggle/input/prodataset/AI_Resume_Screening.csv`
- **Fields Used:** 
  - `Resume_ID` (or resume text)
  - `Name` (candidate’s name)
  - Other fields as present in your dataset.

## Methodology

### 1. Data Loading & Cleaning

- The resumes are loaded from a CSV file.
- Each resume is cleaned by converting to lowercase and removing punctuation for uniformity.

### 2. Job Description Processing

- The job description is defined by the user and cleaned similarly.
- Key skills are extracted for additional skill matching analysis.

### 3. Semantic Similarity Calculation

- We use a pre-trained BERT-based Sentence Transformer model (`all-MiniLM-L6-v2`).
- Both resumes and job description are encoded into semantic vectors.
- Cosine similarity is used to score each resume against the job description.
- **Advantage:** Scores are almost never exactly zero, even with no keyword overlap, as the model captures semantic meaning.

### 4. Skill Extraction

- For each resume, the intersection of words with job description keywords is computed.
- The matched skills and their count are recorded for each candidate.

### 5. Ranking & Export

- Resumes are ranked by their semantic similarity score.
- An enhanced CSV report is generated including candidate name, resume ID, score, and matched skills.
- The top 5 resumes are exported as text files for easy review.

### 6. Visualization

- A bar chart visualizes the match scores of the top 5 candidates.

## Results

- The system outputs a ranked list of candidates with their names, IDs, scores, and skill matches.
- Top resumes are saved for direct inspection.
- The approach ensures fair, semantic-based matching, reducing bias from simple keyword overlap.

## Key Code Snippet

```python
from sentence_transformers import SentenceTransformer
from numpy import dot
from numpy.linalg import norm

def cos_sim(a, b):
    return dot(a, b) / (norm(a) * norm(b))

model = SentenceTransformer('all-MiniLM-L6-v2')
resume_embeddings = model.encode(data['Cleaned_Resume'].tolist(), convert_to_tensor=False)
jd_embedding = model.encode([cleaned_jd], convert_to_tensor=False)
data['Match_Score'] = [cos_sim(res_emb, jd_embedding[0]) for res_emb in resume_embeddings]
```

## Files Produced

- `enhanced_resume_match_report.csv` — Full ranked report with names, scores, and skill matches.
- `Top_Resumes/` — Folder with the top 5 resumes as text files.
- Bar chart visualizing top match scores.

## How to Run

1. Update the job description section of the code as needed.
2. Place your resume dataset at the specified path.
3. Run the script in a Python environment with required packages.
4. Review the CSV report, exported top resumes, and the score visualization.

## Requirements

- Python 3.x
- pandas
- sentence-transformers
- numpy
- matplotlib

Install requirements with:
```bash
pip install pandas sentence-transformers numpy matplotlib
```

## Conclusion

This project demonstrates an effective, modern approach to resume screening using semantic matching. It enables HR professionals to shortlist candidates based on the true meaning of their experience, not just keywords.

---

*Prepared by: [Gaurav Maheshwari]*  
*Date: June 2025*
