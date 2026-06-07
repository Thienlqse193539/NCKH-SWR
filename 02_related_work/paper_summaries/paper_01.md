# Research Summary: AI-Driven Decision-Making System for Hiring Process

## Citation
* **Title:** AI-Driven Decision-Making System for Hiring Process
* **Authors:** Vira Filatova, Andrii Zelenchuk, Dmytro Filatov
* **Year:** 17 December 2025.
* **Source:** arXiv.
* **DOI / Link:** https://arxiv.org/html/2512.20652v1

---

## The Problem
The paper focuses on fixing the slow bottleneck at the **early stage of hiring candidates**. 
* **Real-world challenge:** HR staff usually have to manually read and check a huge amount of mixed data from CVs, basic interview answers, coding tests, and public social media accounts.
* **Current limits:** Existing automation tools (like ATS or basic chatbots) work alone and miss the "big picture" of a candidate. Also, they act like "black boxes"—giving scores without explaining why, making it hard for recruiters to trust them.

---

## The Method
The paper proposes a **multi-agent, multimodal hiring assistant** powered by a Large Language Model (specifically GPT-4o) using a 5-step process:

1.  **Preprocessing:** 
    * Extract text from CVs using `PaddleOCR` (to prevent harmful code hidden in files).
    * Use `ffmpeg` to cut interview videos into images (1 frame every 5 seconds) and extract the audio.
    * Use `GPT-4o Vision` to check how professional the background and clothes look, and use `Whisper` to change speech into text.
    * Convert all data into Markdown format using `Docling`.
2.  **Initial Context:** Use `GPT-4o` to save candidate profiles into clean JSON files (skills, education, history) and fix skill names using an alias map.
3.  **Context Augmentation:** Use Model Context Protocol (MCP) and DuckDuckGo to search for candidates on social media (LinkedIn, GitHub, X, etc.) to check if their data matches and look for red flags.
4.  **LLM Analysis:** 
    * Match skills with concrete proof using text entity tools (NER, ED, NEL).
    * Test the candidate's code by running test cases and checking code quality with the LLM.
    * Calculate scores for technical fit, culture fit (7 areas), and a risk penalty score.
5.  **Candidates Ranking & Human-in-the-loop:** Rank candidates using a math formula with a adjustable weight. The top 10 candidates and their detailed score reports are sent to a Gradio web page so the recruiter can make the final choice.

---

## Dataset
* **Size:** 64 real candidate profiles applying for a **Mid-level Python Backend Engineer** role.
* **Baseline:** The profiles were also checked by two real human recruiters to compare results:
    * A senior recruiter (> 5 years of experience) -> Used as the **Ground Truth**.
    * A junior recruiter (~ 1 year of experience).

---

## Evaluation & Results

### Metrics Used
* **Classification:** Precision and Recall compared to the senior recruiter's choices.
* **Total Time :** The average time needed to find 1 good candidate, based on screening time, technical interview time, precision, recall, and the rate of good candidates.
* **Cost:** Comparing OpenAI API costs (GPT-4o, Whisper, Embeddings, Vision) against human hourly pay.

### Results
* **Hiring Time :** The AI system was much faster, taking only **1.70 hours** to find a good candidate (compared to **3.33 hours** for the senior recruiter). The AI processed **3.28 candidates per hour** (the expert did 1.07).
* **Hiring Cost:** The AI cost was very low, at only **$2.29** per good candidate (including API costs), compared to **$50** for the senior recruiter and **$95** for the junior recruiter.
* **Accuracy:** The system's choices closely matched the expert recruiter (correctly picking 16/21 good candidates and correctly rejecting 41/43 unfit candidates).

---

## Limitations
1.  **Small Dataset:** Only tested on 64 candidates for just one specific job role (Python Backend).
2.  **Rater Bias:** The ground truth comes from just one expert recruiter, which might include personal bias or specific company preferences.
3.  **Privacy and Legal Issues:** Scanning public social media data automatically can run into privacy laws like GDPR.
4.  **Gaming the System:** The system can still be tricked by CVs that are overly optimized or written by AI just to get high scores.

---

## Relevance to Our Topic
* **Business Process Automation:** A great example of using multiple AI agents together to handle a complex, step-by-step business task.
* **Multimodal AI:** Shows how to combine text (CV), sound (Whisper), and video/images (GPT-4o Vision) to understand a user completely.
* **Human-in-the-loop AI:** Features an Explainable AI design that helps humans make faster choices instead of letting the AI decide everything alone.

---

## Possible Improvements
* **Use Local LLMs:** Run open-source models like Llama 3 or Mistral locally via Ollama. This protects candidate privacy and removes third-party API costs.
* **Better Video Analysis:** Use specialized models to check soft skills through voice tone, speech speed, or facial expressions (instead of just checking clothes or background).
* **AI-Generated Resume Detector:** Add a tool to flag CVs made entirely by AI to keep the process fair for everyone.
* **Reduce Rater Bias:** Have at least 5 expert recruiters grade the candidates together for a fairer ground truth, and use statistical math tests (like paired bootstrap or permutation tests) to prove the system works.
