# Academic Transfer Planner Documentation

## 1. Project Overview
The Academic Transfer Planner is a single-page web application designed to help Computer Science students evaluate how their completed courses transfer to other engineering programs. 

## 2. Equivalency Algorithm Logic
The application determines course equivalencies using a custom rule-based algorithm. Rather than hardcoding a strict 1-to-1 dictionary for every single course, the logic categorizes courses and applies transfer rules based on the target academic program.

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
   Overlap exists primarily in hardware, systems, and low-level computing. Specific courses like *Computer Organization*, *Operating Systems*, and *Networks* transfer successfully, flagged with an `(EE)` suffix to denote the department-specific variant.

### Equivalency Summary Table
| Course Category | Computer Engineering | Civil Engineering | Electrical & Electronics |
| :--- | :--- | :--- | :--- |
| **Math & Physics** | Full Transfer | Full Transfer | Full Transfer |
| **Software/Algorithms** | Full Transfer | No Transfer (N/A) | No Transfer (N/A) |
| **Hardware & Systems** | Full Transfer | No Transfer (N/A) | Partial Transfer |
| **Management** | Full Transfer | Partial Transfer | Partial Transfer |

### Code Implementation Example
The logic is handled by the `getEquivalentCourse(program, courseName)` function. Here is a snippet demonstrating the routing logic:

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
    return "N/A";
}
// ... additional logic for EE
