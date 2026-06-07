## Citation
* **Title:** Fairness in AI-Driven Recruitment: Challenges, Metrics, Methods, and Future Directions
* **Authors:** Dena F. Mujtaba, Nihar R. Mahapatra
* **Year:** May 18, 2025
* **Source:** arXiv
* **DOI / Link:** https://arxiv.org/abs/2405.19699

---

## The Problem
The paper studies and addresses algorithmic bias and fairness in AI tools used for hiring:
* **Spreading and growing bias:** Recruitment is moving fast toward AI-driven systems (scanning resumes, writing job ads, and automated interviews). However, training AI on historical hiring data causes the algorithms to learn and amplify existing human biases (such as gender, race, age, and disability).
* **Bad impacts on society and companies:** Algorithmic bias systematically hurts minority candidate groups, lowers workplace diversity, reduces public trust in AI, and exposes companies to serious legal risks.
* **Research gap:** There are not enough systematic reviews that connect fairness metrics and bias removal methods across all hiring stages (sourcing, screening, interviewing, and selection).

---

## The Method
This paper is a **systematic review**. The authors analyze and group algorithmic fairness concepts into a clear structure:

1.  **Organizational Psychology Theory:** Connects AI fairness to the concepts of trust and organizational justice (Distributive, Procedural, and Interactional justice).
2.  **Legal Frameworks and Ethical Principles:** Summarizes ethical standards from FAT/ML, NIST, and the FTC. It covers current laws like Title VII of the Civil Rights Act in the US, the EU AI Act, and New York City’s bias audit laws. It defines two types of discrimination based on the EEOC's 4/5ths rule (80% rule): *Disparate Treatment* and *Disparate Impact*.
3.  **Sources of Bias:** Identifies 5 main causes of bias: biased training data, unclear target labels, poor feature selection, proxies (like using home addresses or school names to guess race/income), and intentional masking of bias.
4.  **Bias Mitigation Techniques:** Groups fixes into 3 main types:
    * **Pre-processing:** Changing the data distribution or labels before training the AI model.
    * **In-processing:** Adding fairness rules directly into the model's optimization math during training.
    * **Post-processing:** Adjusting the model's output decision thresholds after it makes predictions.

---


## Dataset
* **Type:** This is a systematic review paper (Survey Paper), so it does not use a single, new experimental dataset.
* **Data Sources:** The authors collected, summarized, and analyzed **195 scientific papers and legal documents** published up to December 2024.
* **Real-world Case Studies Analyzed:** The paper uses famous real-world examples of AI bias from tech giants as part of its study pool, including Amazon (Document [13]), Facebook (Document [14]), Google (Document [35]), and HireVue (Document [36]).
---

## Evaluation & Results

### Risk Analysis by Hiring Stage
The paper evaluates the state of AI hiring tech by looking at bias risks in each step:
* **Candidate Sourcing:** Using gender or age-biased words in Job Descriptions (JDs), and bias in how social media algorithms show job ads to users.
* **Candidate Screening:** Bias in Large Language Models (LLMs) and word embeddings when scoring CVs based on a candidate's name or background.
* **Candidate Interviews:** Audio/video tools giving lower scores to candidates with regional accents or speech disabilities, and the lack of scientific proof behind automatic personality tests.
* **Selection & Offer:** Unfair salary offers caused by AI analyzing a candidate's past salary history.

### Main Results
* Successfully creates a complete picture of challenges, fairness metrics, and bias-fixing methods for each step of the HR process.
* Proves that simply hiding sensitive data (like gender or race) does not work because AI can still guess these traits using other proxy data fields.
* Provides a step-by-step roadmap for AI engineers and HR policymakers to build fair, trackable, and auditable hiring systems.

---

## Limitations
* **Trade-offs between fairness metrics:** Different mathematical definitions of fairness often clash with each other. For example, a system cannot always achieve group fairness and individual fairness at the same time, forcing companies to make hard choices.
* **Limits of current bias tools:** Open-source bias libraries mostly support simple binary choices. They are very hard to use on complex models like candidate ranking, multi-agent systems, or Generative AI.
* **Missing candidate viewpoint:** Most current research focuses on fixing algorithms for the recruiter. They ignore how candidates feel about fairness when interacting with AI.
* **Legal gap:** Laws move much slower than the rapid development of Large Language Models and Generative AI.

---

## Relevance to Our Topic
* **AI Ethics and Algorithmic Fairness:** Provides core theories on how to define, measure, and remove bias in machine learning models.
* **HR Tech Software Development:** Offers guidance on building recruitment software that follows EEOC standards (the 4/5ths rule), the EU AI Act, and modern laws.
* **LLM Safety Evaluation:** Gives methods to design benchmarks to test hidden biases in LLMs when they read CVs or conduct interviews.

---

## Possible Improvements
* **Create Fairness Audits for Generative AI (LLMs):** Research new fairness metrics designed specifically for text generation tasks, such as writing neutral JDs or objective rejection letters.
* **Build Fair Ranking Algorithms:** Create specialized post-processing methods for listwise ranking outputs (like tournament-based or graph-based ranking) to ensure balanced final leaderboards.
* **Improve Accessibility for Disabled Candidates:** Train speech and facial expression models to not penalize candidates with speech or facial muscle conditions during video interviews.
* **Add Real-time Bias Alerting:** Develop a module that immediately warns recruiters if the selection rate between different candidate groups breaks the EEOC 4/5ths rule during screening.
