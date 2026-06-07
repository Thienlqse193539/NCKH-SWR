
## Citation
* **Title:** Agentic AI for Human Resources: LLM-Driven Candidate Assessment
* **Authors:** Kamer Ali Yuksel, Abdul Basit Anees, Ashraf Elneima, Sanjika Hewavitharana, Mohamed Al-Badrashiny, Hassan Sawaf
* **Year:** March 17, 2026
* **Source:** arXiv 
* **DOI / Link:** https://arxiv.org/abs/2603.26710

---

## The Problem
The paper addresses major weak points in current hiring and candidate evaluation tools:
* **Weak ATS tools:** Current screening systems rely too much on simple keyword filters or shallow matching. This makes them easily miss great talent and fail to see deeper details.
* **Human overload and bias:** Human recruiters often suffer from cognitive overload, show inconsistent grading between different reviewers, and are affected by hidden biases.
* **Limits of current LLM ranking:** Simple embedding-based matching is too superficial. Meanwhile, using LLMs to compare candidates in pairs creates too much noise, relies heavily on specific prompts, and cannot scale up to handle large candidate pools efficiently.

---

## The Method
The paper proposes an explainable multi-agent framework that combines dynamic criteria creation with an active tournament ranking system:

### 1. Multi-Agent Architecture
* **Criteria Generation Agent:** Automatically reads the Job Description (JD) and creates a detailed grading schema (a YAML file with 12 to 20 evaluation areas and definitions for each level).
* **Video Question Generation Agent:** Generates custom interview questions for each candidate to answer on video.
* **Assessment Generator Agent:** Combines data from CVs, interview video transcripts, facial expression checks, audio data, and HR notes to write a detailed report in Markdown format (categorized into Low, Medium, and High levels).
* **Feedback Integration Module:** Takes post-hiring performance reviews and employee retention data to fine-tune the system over time.
* **Support Agents:** Includes a Formatter Agent (to standardize files), a Comparison Agent (for side-by-side checks), and a Ranking Agent (to add new candidates).

### 2. Active Listwise Tournament Ranking
* **Mini-tournaments:** Instead of comparing just two candidates at a time, the system groups candidates into small batches ($K = 5$ to $10$ people). The LLM reads and ranks the whole batch at once based on the job criteria.
* **Plackett–Luce (PL) Model:** Combines the small batch results to calculate global scores for all candidates, creating a single, fair master leaderboard.
* **Active Learning Loop:** Uses smart mathematical algorithms (like MC-KG or KL-UCB) to pick the most informative groups of candidates for the next mini-tournaments. This quickly stabilizes the ranking and cuts down on expensive LLM API costs.

---

## Dataset
* **Content:** Real-world candidate pools across multiple corporate levels and complex roles (including technical roles like *AI Research Scientist* and *Staff Machine Learning Engineer*, as well as executive roles like *VP of Product* and *CTO*).
* **Testing:** The system was evaluated using **30 active learning loops** on a fixed pool of candidates whose true ranks were already decided by expert human recruiters.

---

## Evaluation & Results

### Metrics Used
* **Expert Agreement:** Checking how often the system's scores match or stay within 1 level (Low/Medium/High) of human expert grades.
* **Ranking Quality (Ranking Fidelity):** Using **NDCG@K** at different cut off points compared against the human expert rankings.
* **Ranking Convergence:** Tracking **Kendall-$\tau$** scores between ranking rounds and the movement of the Plackett-Luce score vector ($\Delta u$) to see how quickly the system finds a stable list.

### Results
* **Agreement Rate:** **87%** of the system's grades were within an acceptable range (maximum 1 score band difference) compared to human experts. The system successfully identified soft skills (like leadership maturity and communication style) to separate candidates with similar technical CVs.
* **Ranking Performance:** The NDCG score improved steadily across rounds, peaking at an NDCG@25% of **0.5703** (NDCG@10% was 0.5134, NDCG@15% was 0.5455, and NDCG@20% was 0.5655).
* **Fast Convergence:** The Kendall-$\tau$ score rose quickly and the score movement ($\Delta u$) dropped significantly after round 10. This proves the Active Querying mechanism helps the system find a stable, trustworthy global ranking with very few LLM questions.

---

## Limitations
* **Relies on Input Quality:** If a CV lacks details or a job description is written poorly, the system's evaluation accuracy drops heavily.
* **Limited Non-Verbal Analysis:** The video module currently only tracks facial expressions. It cannot analyze deep voice tones or full-body gestures yet.
* **Hidden LLM Logic:** Even though the final reports are highly detailed, the exact logical steps the LLM takes to read between the lines during complex tasks remain a "black box."
* **Manual Prompt Tweaking:** Users still need to manually adjust prompts to make the system work well for highly unique or niche job positions.

---

## Relevance to Our Topic
* **Multi-Agent System Design:** Serves as a great architectural blueprint for dividing complex HR workflows into specialized AI agents that execute tasks step-by-step.
* **Ranking and Matching Algorithms:** Provides solid mathematical theory on using the Plackett-Luce model alongside Active Learning to rank multiple profiles using an LLM.
* **Multimodal Integration:** Offers a useful reference for combining standard text data with video and audio inputs to assess candidates.

---

## Possible Improvements
* **Advanced Video/Audio Analysis:** Integrate specialized deep learning models to check soft skills by tracking voice tone, speech rate, and body gestures during video interviews.
* **Rubric Drift Control:** Build semantic rules to make sure the evaluation criteria do not change or lose their original meaning during continuous review loops.
* **Real-time Interview Assistant:** Use the system to suggest deep follow-up questions to human recruiters in real-time based on live answers given by a candidate during an interview.
* **Fairness Constraints:** Add fairness and anti-bias math rules into the Plackett-Luce model to stop the AI from copying or amplifying historical human biases (like gender or race discrimination).
