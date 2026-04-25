# Note on AI Use

## AI Usage Declaration

In the interest of academic and professional transparency, I acknowledge the use of Artificial Intelligence (Large Language Models) during the development of this project. AI tools were utilized strictly as developmental assistants under human oversight. 

Specific applications include:
* **Code Refinement:** Assisting with syntax formatting, debugging Python scripts, and troubleshooting specific `Plotly.js` and `Leaflet.js` visualization parameters.
* **Documentation & Formatting:** Polishing the English prose in this `README.md`, structuring Markdown elements, and formatting HTML code snippets.

**Crucially, no AI was used to:**
* Fabricate, alter, or synthesize the raw ACLED data.
* Generate the foundational geopolitical analysis or formulate the conclusions.
* Design the logic of the Disobedience Severity Index methodology.

All data parsing, methodological design, and analytical interpretations remain my original intellectual work. I have thoroughly reviewed, tested, and verified all AI-assisted outputs for accuracy and validity prior to publication.

## AI Usage Explanation

In the interest of academic transparency, I acknowledge the use of Google's **Gemini Pro** model as an assistant during the development of this project. 

My workflow and the specific applications of AI were as follows:

* **Data Processing & Code Generation:** I initially provided the AI with brief, structured prompts detailing how I wanted to process the raw ACLED datasets. I then used an iterative chat process to refine the code and make small adjustments to the interactive dashboard. The two prompts are `Prompt/Prompt_creating_code.md` and `Prompt/Prompt_creating_dashboard.md`.
* **`Prompt/Prompt_creating_dashboard.md`**: A record of the iterative AI prompts utilized to refine the HTML, CSS, and JavaScript components of the interactive web dashboard.
* **Debugging & Methodological Reflection:** When my premium AI usage quota was exhausted, I transitioned to manually reviewing the code and troubleshooting errors alongside the AI. While time-consuming, this phase was the most educational. It forced me to deeply understand the Python syntax, HTML/Markdown formatting, and my own methodology.
* **Human Oversight & Correcting AI Bias:** During the debugging phase, I actively identified and corrected logical flaws introduced by the AI. For example, the AI's initial code failed to account for events with zero fatalities, which resulted in many valid disobedience events being wrongly nullified during the Disobedience Index calculation. I recognized this error and corrected the mathematical formula to `(Fatalities + 1)` to ensure all events were accurately weighted.
* **Translation & Copyediting:** I outlined most of my analytical thoughts and project structure in a mix of Chinese and English. I utilized the AI to translate (润色), polish the academic tone, and check the final English grammar.

Ultimately, while AI significantly accelerated the coding and writing process, all final data parsing, methodological logic, debugging, and analytical interpretations remain my original intellectual work.
