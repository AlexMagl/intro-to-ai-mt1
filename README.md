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
1. **General Education & Foundation Courses:** Mathematics (Calculus I-III, Linear Algebra), Physics, and General English are considered universal foundations. They transfer directly to all target programs.
2. **Computer Engineering Transfer:** Because Computer Science and Computer Engineering share a heavy overlap in their core curricula, **100%** of the passed Computer Science courses transfer directly to this program.
3. **Civil Engineering Transfer:** Overlap is minimal. Only highly generalized technical skills transfer:
   * *Introduction to Programming* -> *Computing for Engineers*
   * *IT Project Management* -> *Engineering Project Management*
4. **Electrical & Electronics Engineering (EE) Transfer:** Overlap exists primarily in hardware, systems, and low-level computing. Specific courses like *Computer Organization* and *Operating Systems* transfer successfully, but are flagged with an `(EE)` suffix.

### Equivalency Summary Table
| Course Category | Computer Engineering | Civil Engineering | Electrical & Electronics |
| :--- | :--- | :--- | :--- |
| **Math & Physics** | Full Transfer | Full Transfer | Full Transfer |
| **Software/Algorithms** | Full Transfer | No Transfer (N/A) | No Transfer (N/A) |
| **Hardware & Systems** | Full Transfer | No Transfer (N/A) | Partial Transfer |
| **Management** | Full Transfer | Partial Transfer | Partial Transfer |

### Code Implementation Example
Here is a snippet of the JavaScript logic used to dynamically route the courses based on the selected program:

```javascript
// Check for universal transfer first
if (generalAndMath.includes(courseName)) {
    return courseName; 
}

// Program-specific routing
if (program === "Computer Engineering") {
    return courseName; 
} else if (program === "Civil Engineering") {
    if (courseName === "Introduction to Programming") return "Computing for Engineers";
    if (courseName === "IT Project Management") return "Engineering Project Management";
    return "N/A";
}
// ... additional logic for Electrical & Electronics Engineering
