# Academic Transfer Planner Documentation

## 1. Project Overview & Features
The Academic Transfer Planner is a single-page web application designed to help Computer Science students evaluate how their completed courses transfer to other engineering programs. 

**Key Features Include:**
* **Course History:** Automatically displays the student's full course history, clearly marking courses as passed ("Yes") or not passed ("No").
* **Program Selection (Dropdown):** A dynamic dropdown menu allows the student to select their desired target program (Computer Engineering, Civil Engineering, or Electrical and Electronics Engineering).
* **Transfer Evaluation:** A "Transfer" button that instantly generates an equivalency table filtering out incomplete courses and applying transfer logic to completed ones.

## 2. Description of the Equivalency Algorithm
The application determines course equivalencies using a custom rule-based algorithm. Rather than hardcoding a strict 1-to-1 dictionary for every single course, the logic categorizes courses and applies transfer rules based on the target academic program selected in the dropdown.

### Core Rules Applied
1. **General Education & Foundation Courses:**
   Mathematics (Calculus I-III, Linear Algebra), Physics, and General English are considered universal foundations. They transfer directly to all target programs.
2. **Computer Engineering Transfer:**
   Because Computer Science and Computer Engineering share a heavy overlap in their core curricula, **100%** of the passed Computer Science courses transfer directly to this program.
3. **Civil Engineering Transfer:**
   Overlap is minimal. Only highly generalized technical skills transfer:
   * *Introduction to Programming* transfers as *Computing for Engineers*.
   * *IT Project Management* transfers as *Engineering Project Management*.
4. **Electrical & Electronics Engineering (EE) Transfer:**
   Overlap exists primarily in hardware, systems, and low-level computing. Specific courses like *Computer Organization*, *Operating Systems*, and *Networks* transfer successfully, but are flagged with an `(EE)` suffix to denote the department-specific variant.

### Equivalency Summary Table
| Course Category | Computer Engineering | Civil Engineering | Electrical & Electronics |
| :--- | :--- | :--- | :--- |
| **Math & Physics** | Full Transfer | Full Transfer | Full Transfer |
| **Software/Algorithms** | Full Transfer | No Transfer (N/A) | No Transfer (N/A) |
| **Hardware & Systems** | Full Transfer | No Transfer (N/A) | Partial Transfer |
| **Management** | Full Transfer | Partial Transfer | Partial Transfer |

## 3. Improvement Plan: Automatic Syllabus Comparison
Currently, the transfer logic relies on manually defined, hardcoded rules. The ultimate future improvement for this application is to implement an **Automatic Syllabus Comparison Algorithm** driven by Artificial Intelligence. 

Instead of relying solely on course titles, the system will use AI to read, understand, and compare the actual contents of the courses. 

### AI Comparison Algorithm Steps

1. **Data Ingestion (Document Parsing):**
   * The system will accept syllabus document uploads (PDF or DOCX) or fetch them directly from the university's database for both the student's current program and the target program.
   * Text extraction tools will parse the documents to isolate the *Learning Outcomes*, *Weekly Topics*, *Credit Hours*, and *Assessment Methods*.

2. **Semantic Embedding Generation:**
   * An AI embedding model (e.g., OpenAI's text embeddings) will convert the extracted syllabus text into high-dimensional vector representations. 
   * This allows the computer to understand the semantic "meaning" of the course content rather than just checking for matching keywords.

3. **AI Similarity Scoring:**
   * The algorithm will calculate the **Cosine Similarity** between the vector of the completed course and the vectors of all courses in the target program.
   * An LLM (Large Language Model) will be prompted to do a secondary qualitative check on highly similar pairs, asking it: *"Does Source Course A cover at least 80% of the learning objectives of Target Course B?"*

4. **Equivalency Thresholding:**
   * **Score > 85%:** Automatic Equivalency Match (Approved).
   * **Score 65% - 84%:** Flagged for Human Review (Sent to the Dean/Advisor for final approval).
   * **Score < 65%:** No Match (Outputs "N/A").

5. **Dynamic Table Generation:**
   * The application frontend will consume the resulting JSON output from the AI and dynamically build the equivalency table, providing exact percentage matches and AI-generated justifications for *why* a course was deemed equivalent. 

By utilizing AI, universities can instantly update transfer pathways every semester without manually rewriting equivalency databases, saving administrative labor while ensuring maximum fairness for transferring students.
