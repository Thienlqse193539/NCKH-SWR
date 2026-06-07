## Citation
* **Title:** SMART-HIRING: AN EXPLAINABLE END-TO-END PIPELINE FOR CV INFORMATION EXTRACTION AND JOB MATCHING
* **Authors:** Kenza KHELKHAL, Dihia LANASRI
* **Year:** November 05, 2025
* **Source:** arXiv
* **DOI / Link:** https://arxiv.org/abs/2511.02537

---

## The Problem
The paper addresses three major problems in the recruitment process:
* **Overload and human bias:** Reviewing hundreds of CVs manually for each job opening wastes a lot of time. It also leads to mistakes and unfair decisions based on human bias.
* **Limits of keyword filtering:** Traditional keyword or rule-based filters cannot understand word meanings. For example, they fail to see that "software developer" and "application engineer" mean the same job.
* **Unstructured CV formats:** Most CVs do not follow standard ATS layouts. They use complex multi-column designs, tables, or mix two languages (like French and English), making it hard for machines to read them.

---

## The Method
The **Smart-Hiring** system uses a two-stage, end-to-end NLP pipeline:

### Stage 1: Resume Information Extraction
* **Layout Analysis:** Uses `pdfplumber` to convert standard PDFs into raw text while keeping text coordinates to handle multi-column layouts. For highly complex or graphic layouts, it uses **IBM DocLing**. Scanned images are processed via an OCR module.
* **Name Extraction:** Uses a supervised classifier trained specifically on Algerian names to solve local naming complexities (multi-word names, Arabic-origin names, or special characters).
* **Contact Info:** Extracted using Regex and simple rules.
* **Skills:** Uses fuzzy matching against a standard skill dictionary from LinkedIn (e.g., matching "JS" to "JavaScript").
* **Education & Experience:** Matches degrees (Licence, Master, PhD, Engineer in both English and French) using fuzzy matching and calculates total years of experience from date intervals.

### Stage 2: Job Matching
* Matches basic profile details (location, years of experience, education) directly from the CV with the job description (JD) requirements.
* For skills, it converts skill phrases from both CVs and JDs into math vectors using a small transformer model: **`all-MiniLM-L6-v2`**. It then calculates **Cosine similarity** between these vectors to find related skills (e.g., matching "Linux" to "Ubuntu").
* Calculates a final score using a weighted average, giving higher weight to core skills and experience based on expert input.
* **Explainability Layer:** Visually highlights matching skills, experience, and keywords on a screen so recruiters can easily see *why* a candidate was ranked high.

---

## Dataset
* **Size:** Around 1,000 real CVs and hundreds of Job Descriptions (JDs).
* **Fields:** Covers various professional areas, mostly focusing on IT and Telecommunications.
* **Languages:** Written mostly in two languages: **French** and **English**.

---

## Evaluation & Results

### Metrics Used
* **Information Extraction:** Evaluated manually by checking data quality and gathering feedback from HR experts.
* **Job Matching:** Compared the AI's recommendations directly against ranking sheets created by real HR teams.
* **Main Metrics:** Accuracy and **Top-k match rate** (specifically looking at the Top-3 match rate).

### Results
* **Extraction:** The system reached high accuracy for structured fields like education, contact info, and skills.
* **Matching:** Achieved an **impressive Top-3 match rate**, showing that the AI's choices closely matched decisions made by human experts.
* **Trust:** The explainability layer greatly improved trust and transparency, allowing HR teams to make faster decisions using highlighted visual proof.

---

## Limitations
* **Layout Errors on Complex CVs:** If a CV has too many graphics, tight text, or columns, the system sometimes reads text in the wrong order. This hurts the accuracy of the name and skill extraction tools down the line.
* **Static Rules:** Calculating years of experience and extracting degrees still relies heavily on manual rules (*heuristics*). This can fail on CVs written in non-standard ways.
* **No Automatic Feedback Loop:** The system cannot learn or adapt on its own based on whether a recruiter approves or rejects a candidate profile.

---

## Relevance to Our Topic
* **Information Extraction:** Provides a real-world pipeline for preprocessing and extracting details from complex PDFs using `pdfplumber` and `Docling`.
* **Sentence Embeddings for Semantic Matching:** A great reference for using small, fast Transformer models (like `all-MiniLM-L6-v2`) and Cosine similarity to compare texts efficiently.
* **Explainable AI (XAI):** Serves as a great example of building transparent AI user interfaces to reduce hiring bias and help humans trust automated systems.

---

## Possible Improvements
* **Use Advanced Document Models:** Integrate multi-modal models like LayoutLMv3 or Donut to handle complex graphic CV layouts without breaking the natural reading order.
* **Automate with LLMs:** Use modern Large Language Models (LLMs) for zero-shot or few-shot information extraction. This avoids having to manually maintain a static LinkedIn skill dictionary.
* **Add Continuous Learning:** Create a feedback loop that automatically tweaks matching weights (skills, experience, location) based on how recruiters actually score candidates in real-time.
* **Support Local Languages:** Train the name classifier and degree dictionaries to work well with Vietnamese names and the local education system for better practical use in the domestic market.
