## Citation
* **Title:** GraphRank Pro+: Advancing Talent Analytics Through Knowledge Graphs and Sentiment-Enhanced Skill Profiling
* **Authors:** Dr. Sirisha Velampalli, Chandrashekar Muniyappa
* **Year:** February 25, 2025
* **Source:** arXiv 
* **DOI / Link:** https://arxiv.org/pdf/2502.18315

---

## The Problem
The paper addresses two core problems in talent analytics and hiring:
* **Unstructured and diverse CVs:** Resumes have many different formats and personal writing styles. This makes traditional keyword filters or static models easily miss important contextual data.
* **Limits of basic keyword filtering:** Simply counting how many times a skill keyword (like "C++") appears does not show a candidate's actual proficiency. Recruiters need to know which projects the candidate used the skill in, how complex those projects were, and how long they worked on them.

---

## The Method
The proposed system, **GraphRank Pro+**, uses graph databases, NLP, and Deep Learning to represent candidate abilities through a Knowledge Graph:

1.  **Information Extraction:** Converts CVs into text using `Apache Tika`. It then uses the `SpaCy` library for POS tagging (identifying parts of speech) and Named Entity Recognition (NER) to extract specific nodes: Job Seeker (`<JobSeeker>`), Skill (`<Skill>`), Company (`<Organization>`), and Project (`<Project>`).
2.  **Skill-Sentiment Gazetteer:** Builds a specialized dictionary of positive keywords linked to skills to assign scores. For example, in software development, words like *scalability*, *robust*, or *distributed* will increase the proficiency score of the related skill.
3.  **Graph Building and Linking (Neo4j):**
    * **Skill-to-Project edge:** The connection score is based on finding positive keywords in the project description.
    * **Candidate-to-Skill edge:** Calculated by taking the average of the candidate's skill-project scores and adding the total duration of the projects.
    * **Company-to-Skill edge:** Calculated by taking the average skill-project edges of all candidates who worked at that company using that specific skill.
4.  **Advanced Querying:** The system easily handles both simple queries (like "top C++ candidates") and complex queries that include specific years of experience for each skill (e.g., "C++ 8-10 years, Java 6-8 years, Python 2-3 years").

---

## Dataset
* **Size:** 1,000 real candidate resumes.
* **Industries:** Covers 15 different fields (IT, Healthcare, Engineering, Finance, etc.).
* **Experience Levels:** Entry-Level (30%), Mid-Level (45%), Senior (25%).
* **Diversity:** Candidates come from 25 countries with different education levels: Bachelor's (40%), Master's (35%), PhD (15%), Others (10%).
* **Average Content:** Each resume contains about 12 skills and 2 projects.

---

## Evaluation & Results

### Metrics Used
* **Skill Extraction Accuracy:** Precision, Recall, and F1-Score.
* **Sentiment Analysis Accuracy:** Checking if words around a skill are Positive, Negative, or Neutral (Accuracy, Precision, Recall).
* **Graph-based Ranking Performance:** Measuring accuracy when recommending the Top 3, Top 5, and Top 10 most suitable candidates.
* **Baselines:** Directly compared against 3 common methods: Keyword Search, Rule-based systems, and Semantic-based systems.

### Results
* **Skill Extraction:** Reached 92% Precision, 88% Recall, and a 90% F1-Score (much higher than Keyword Search at 72% and Rule-based at 85%).
* **Sentiment Analysis:** Reached 85% Accuracy (86% Precision, 84% Recall), beating traditional Semantic-based methods (82%).
* **Candidate Ranking:**
    * Reached **78% accuracy for the Top 3 candidates** (compared to only 40% for Keyword Search and 55% for Rule-based).
    * Reached **85% for the Top 5 candidates** and **90% for the Top 10 candidates**.
    * The results prove that adding sentiment analysis (understanding the project context where a skill was used) makes ranking candidates much more accurate than just counting raw keywords.

---

## Limitations
1.  **Manual Weight Setup:** The initial scores (from 0 to 1) for the sentiment keyword dictionary were set manually by the researchers, which might introduce human bias.
2.  **Missing Complex Negations:** The system averages single words, so it can make mistakes with negative sentences. For example, "never worked with robust systems" might still get a positive point because of the word *robust*.
3.  **No Project Cleaning:** The system does not group projects with the same name or similar tasks across different candidates. This can make the graph grow too large with duplicated data.
4.  **Static Scoring:** Connection scores mostly use simple mathematical averages instead of using dynamic information-spreading algorithms across the graph.

---

## Relevance to Our Topic
* **Knowledge Graphs:** A great reference model for designing a graph schema that connects different entities (People, Projects, Skills, Companies) using Neo4j.
* **Semi-structured Data Mining:** Provides a clean solution to analyze data from CVs and project descriptions by combining traditional NLP (`SpaCy`, POS tagging) with dictionary-based sentiment analysis.
* **Recommendation & Ranking Systems:** Highly useful for building multi-criteria ranking algorithms for Job-Candidate Matching tasks.

---

## Possible Improvements
* **Use Graph Neural Networks (GNNs):** Replace static average scores with GNN models (like GCN or GAT) or graph embedding methods (like DeepWalk) to automatically learn hidden patterns and predict job shifts.
* **Integrate LLMs for Deep Context:** Use an LLM (via prompting or fine-tuning) to analyze full project description sentences. This will help catch negative phrases or complex descriptions that a simple dictionary misses.
* **Project Entity Resolution:** Build a module to group similar projects based on text meaning. This keeps the graph clean and speeds up search queries.
* **Multi-language Dictionary Support:** Add skill-sentiment dictionaries in other languages (especially Vietnamese) to make the system more useful in practice.
