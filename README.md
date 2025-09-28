[README.md](https://github.com/user-attachments/files/22583963/README.md)
# Talent Filter and Similarity Matching Engine

This project is a **Talent Filtering and Similarity Matching Engine** built with **FastAPI**.  
It helps recruiters or hiring managers find the **Top 5 employees** that best fit a given **Job Description** by applying strict filtering (education + experience) and ranking results based on **semantic similarity**.

---

## 🚀 Features
- **Strict Filtering**: Employees must match required degree and minimum years of experience.
- **Semantic Skill Matching**: Uses embeddings (Sentence Transformers) to compare job description text with employee profiles.
- **Ranking**: Returns Top 5 best-fit employees with similarity scores and alignment summaries.
- **Flexible Database Format**: Supports JSONL (default), but can be extended to CSV, Excel, or SQL.

---

## 📂 Project Structure

```
JD-TOP5/
│── app/
│   ├── main.py          # FastAPI entrypoint (server & endpoints)
│   ├── matching.py      # Filtering + similarity ranking logic
│   ├── models.py        # Pydantic models for requests
│── data/
│   ├── employees.jsonl  # Employee database (JSON Lines format)
│── utils/
│   ├── loader.py        # Data loading utilities (JSONL, CSV, Excel, SQL)
│── README.md            # Project documentation
```

---

## ⚙️ Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/JD-TOP5.git
   cd JD-TOP5
   ```

2. Create a virtual environment & activate it:
   ```bash
   python -m venv venv
   venv\Scripts\activate   # On Windows
   source venv/bin/activate  # On Mac/Linux
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

---

## ▶️ Running the API

Start the FastAPI server:
```bash
uvicorn app.main:app --reload
```

Server runs at: [http://127.0.0.1:8000](http://127.0.0.1:8000)  

Interactive API docs available at: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## 📊 Example Request (Postman or cURL)

**POST** `/match-job`  

### Request Body
```json
{
  "job_description": "Looking for a Python developer skilled in AWS and data visualization",
  "required_degree": "Bachelor of Science",
  "min_years_experience": 2
}
```

### Response Example
```json
[
  {
    "rank": 1,
    "Employee_ID": "105",
    "score": 0.87,
    "alignment_summary": [
      "Strong Python expertise",
      "AWS project experience",
      "Data visualization with Tableau"
    ]
  },
  {
    "rank": 2,
    "Employee_ID": "101",
    "score": 0.82,
    "alignment_summary": [
      "Python development",
      "Good cloud knowledge",
      "Experience with data reporting"
    ]
  }
]
```

---

## 📂 Database Format (JSONL)

Each employee is a single JSON object on one line:
```json
{"Employee_ID": "101", "Degree_Canonical": "Bachelor of Science", "Years_Experience": 3, "Profile_Text": "Expertise in Python, AWS, Tableau"}
{"Employee_ID": "102", "Degree_Canonical": "Master of Science", "Years_Experience": 5, "Profile_Text": "Java development, agile project management"}
```

---

## 🛠️ Extending the Database
- **CSV/Excel** → Use `pandas.read_csv` or `pandas.read_excel` in `loader.py`
- **SQL Database** → Use `sqlite3` or SQLAlchemy queries in `loader.py`

---

## 📌 Key Workflow

1. **Data Ingestion** → Load employees from JSONL (or CSV/Excel/DB in future).  
2. **Strict Filtering** → Keep only employees with required degree & minimum experience.  
3. **Semantic Search** → Encode Job Description + Employee Profiles using `sentence-transformers`.  
4. **Ranking** → Compute cosine similarity, sort employees, return Top 5.  

---

## 🤝 Contribution
Pull requests are welcome!  
For major changes, please open an issue first to discuss what you would like to change.

---

## 📜 License
MIT License

