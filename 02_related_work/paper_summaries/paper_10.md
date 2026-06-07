## Citation
* **Title:** Exploring the Implementation of AI in Early Onset Interviews to Help Mitigate Bias
* **Authors:** Nishka Lal, Omar Benkraouda
* **Year:** December 18, 2024
* **Source:** New York University (NYU)
* **DOI / Link:** https://www.alphaxiv.org/abs/2501.09890

---

## The Problem
The paper addresses the issue of subjective human bias during early-stage job interviews:
* **Multiple human biases:** Human interviewers are often affected by personal interviewer bias, social desirability, confirmation bias, and the halo effect. This leads to unfair hiring and hurts company diversity.
* **Sentiment bias:** Human recruiters tend to give higher grades to candidates who show a highly positive attitude (such as an optimistic tone and using positive words). They also heavily penalize candidates with a negative attitude, regardless of their actual technical skills for the job.

---

## The Method
The paper proposes a Python-based automated interview bot (`AI interview-bot`) to screen candidates based on knowledge rather than emotional sentiment:

### 1. End-to-End Audio Pipeline
* Candidates upload audio files of their answers to the app via FastAPI (using the `/talk` endpoint).
* The system uses the **OpenAI Whisper API** to convert the candidate's speech into text (Speech-to-Text).
* The dialogue text is sent to **OpenAI's ChatGPT** to analyze the context of the interview history (stored in a JSON file) and generate a fitting response.
* The system converts ChatGPT's text response back into speech using the **ElevenLabs API** to play it back to the candidate, creating a real-time interactive interview experience.

### 2. Analytics & Evaluation Logic
* **Sentiment Analysis:** Uses the **TextBlob** library (via the `/analyze` endpoint) to measure the emotional polarity (positive, negative, neutral) of the candidate's answers.
* **Competency Grading (1-5 Scale):** Measures knowledge from level 1 (Uninformed) to level 5 (Proficient) using a standard math question (*"49 * 54"*) targeted for a Front-end React Developer role.
* **Controlled Experiment Setup:** The researchers created 10 simulated test profiles by crossing 5 technical knowledge levels (1-5) with 2 emotional states (Positive/Negative). They used ElevenLabs computer voices to keep the audio delivery identical.
* **Human Baseline Comparison:** They asked 2 experienced human recruiters (>10 years of experience from Tech Mahindra) to read the transcripts and score them independently on a 1-5 scale to measure the impact of sentiment bias.

---

## Dataset
* **Type:** Small-scale controlled experimental dataset.
* **Data Sources Shared:**
  * **10 simulated interview logs** (10 mock candidate profiles) built specifically for a Front-end React Developer position.
  * Control evaluation grades from **2 professional hiring managers** (1 male, 1 female) to prevent gender rater bias.

---

## Evaluation & Results

### Metrics Used
* **Score Comparison:** Comparing the technical skill grades given by the AI (`AI Rating`) and humans (`Human Rating`) for identical candidate profiles that only differed in emotional attitude.
* **Bias Reduction Rate:** Measuring the percentage (%) drop in emotional bias when using the system.
* **Slope Analysis Graphs:** Plotting the score slopes to visually track how sensitive both humans and AI are to a candidate's mood.

### Results
* **Human Sentiment Bias:** Humans were heavily affected by the candidate's mood. They boosted average scores by **0.62 points** for positive candidates and dropped scores by **1.28 points** for negative candidates. This created a massive **2.06 bias gap** on a 5-point scale.
* **AI Performance:** The AI scoring line was much flatter and accurately tracked the candidate's actual technical knowledge, completely ignoring whether the candidate sounded positive or negative.
* **Bias Mitigation Effectiveness:** Deploying the automated AI interview bot successfully reduced emotional sentiment bias by **41.2%** during early candidate evaluations.

---

## Limitations
* **Very Small Sample Size:** Only tested on 10 simulated profiles, which is not enough data to make broad, long-term claims.
* **Limited to Hard Technical Tasks:** The model values hard technical skills over soft skills. Therefore, it is not suitable for job positions that heavily require high emotional intelligence (EQ), communication skills, or customer service.
* **Few Human Reviewers:** The study only used 2 human recruiters for comparison. A larger panel of human testers is needed to completely eliminate personal human rater bias.

---

## Relevance to Our Topic
* **AI Interviewing Bots:** Provides a clear pipeline blueprint for integrating multiple APIs (FastAPI, Whisper, ChatGPT, ElevenLabs) to build interactive voice-chat interview systems.
* **AI Ethics and Fair Hiring:** Offers concrete experimental proof of how AI can remove emotional noise and force the hiring process to focus on real candidate skills.
* **Text Sentiment Analysis:** Demonstrates a practical use case of using the TextBlob library to measure speech polarity in human resource applications.

---

## Possible Improvements
* **Scale Up the Experiment:** Expand testing to hundreds of real-world job candidates and use a larger panel of human HR experts to make the statistical data more trustworthy.
* **Develop Soft Skills Assessment Agents:** Add natural language agents to evaluate communication skills, behavioral traits, and problem-solving flexibility instead of relying purely on static math/technical questions.
* **Add Local Language and Dialect Support:** Fine-tune the Whisper and ElevenLabs systems to properly handle regional Vietnamese accents, dialects, and localized idioms for practical use in the domestic hiring market.
