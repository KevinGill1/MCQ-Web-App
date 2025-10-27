# MCQ-Web-App
Interactive Web App for MCQs with mathematical typesetting and instant or deferred feedback. It runs entirely in your browser; no data are uploaded to a server. Questions can be imported in JSON format.

---

## How to Use

1. **Open the webpage** in your browser. Can be found @ https://kevingill1.github.io/MCQ-Web-App/

2. Use the **Controls** panel on the left:
   - **Shuffle questions** — randomizes question order
   - **Instant feedback** — shows correctness immediately after answering
   - **Show correct answers after submit** — reveals answers when grading is complete
   - **Auto-save progress** — retains progress locally in your browser

3. Load a **question set**:
   - Click **Import .json** to upload a JSON question file  
     *(the file is never uploaded — it remains in your browser only)*  
   **or**
   - Click **Paste JSON (I)** and paste JSON text directly

4. Click **Start / Reset (R)** to begin the quiz.

5. Answer the questions, then press **Submit All (S)** to view your score and feedback.

6. Optionally, click **Export Attempt** to save your results.

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| **R** | Start / Reset Quiz |
| **S** | Submit All |
| **I** | Paste JSON to import questions |
| **J** | Jump to next unanswered question |

---

## Data Privacy

- The app runs **100% locally** in your web browser.
- **No data is uploaded** or sent to any server.
- If **Auto-save** is enabled, your progress is stored **only in this browser**.
- If disabled, progress is cleared when the tab is closed.

---

## JSON Question File Format

Your question file must be a **JSON array**.  
Each object in the array is one question.

### Example (`questions.json`)

```json
[
  {
    "id": 1,
    "type": "tf",
    "prompt": "In incompressible flow, the continuity equation is $\\nabla\\cdot\\mathbf{v}=0$.",
    "options": ["True", "False"],
    "correct": [0],
    "feedback": "Divergence-free velocity implies constant density."
  },
  {
    "id": 2,
    "type": "mc",
    "prompt": "Which term represents the convective transport of a scalar $\\phi$?",
    "options": [
      "$\\partial_t(\\rho \\phi)$",
      "$\\nabla\\cdot(\\Gamma\\nabla\\phi)$",
      "$\\nabla\\cdot(\\rho\\phi\\mathbf{v})$",
      "$S_\\phi$"
    ],
    "correct": [2],
    "feedback": "The term $\\nabla\\cdot(\\rho\\phi\\mathbf{v})$ is the convective flux."
  }
]
```
### Supported Question Types

| Type      | Description                                      | Required Fields                                                                                 |
|-----------|--------------------------------------------------|-------------------------------------------------------------------------------------------------|
| `tf`      | True / False question                             | `id`, `type`, `prompt`, `options` (2 values), `correct` (index array), *(optional)* `feedback`  |
| `mc`      | Single-answer multiple choice                     | `id`, `type`, `prompt`, `options` (≥2 values), `correct` (single index array), `feedback`       |
| `multi`   | Multiple-answer selection                         | `id`, `type`, `prompt`, `options` (≥2 values), `correct` (array of correct indices), `feedback` |
| `numeric` | Numeric answer with tolerance range               | `id`, `type`, `prompt`, `numeric: { "answer": number, "tol": number }`, `feedback`              |
| `matching`| Match each item on the left to one on the right   | `id`, `type`, `prompt`, `matching: { "left":[], "right":[], "answers":[] }`, `feedback`         |
