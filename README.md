# FabricDemo

# 🎓 Student Assignment (Microsoft Fabric)

## 📌 Objective

This project simulates a data pipeline inspired by Microsoft Fabric's medallion architecture. It demonstrates how to:
* Ingest and store raw data in the **Bronze layer**.
* Clean, transform, and model data in the **Silver layer**.
* Derive analytical insights for business intelligence in the **Gold layer**.
* Automate pipeline orchestration **CI/CD** with **Development Pipelines in Fabric**.

---

## 🛠️ Technologies Used

* **PySpark**: For distributed data processing and transformations.
* **OneLake**: Serving as the unified data lake for storing all data assets (Bronze, Silver, Gold layers) within a Microsoft Fabric-like environment. This implies **Delta Lake** is used as the underlying storage format within OneLake.
* **Notebooks**: Utilized for developing, testing, and interactively analyzing the data transformations within the pipeline.
* **Development Pipelines in Fabric**: For automated Continuous Integration and Continuous Deployment (CI/CD).

---

## 📊 Dataset Overview

The pipeline processes simulated data across four CSV files, each containing 100 records. These files are expected to be located in the `data/raw` directory:

* `students.csv`: Contains student information.
* `assignments.csv`: Contains assignment details.
* `courses.csv`: Contains course details.
* `submissions.csv`: Contains submission records for assignments.

---
## 🚀 Getting Started

Follow these steps to set up and run the project locally.


### Step-by-Step Execution

# Bronze Layer Data Ingestion

This module is responsible for ingesting raw CSV files into OneLake Delta tables in the Bronze layer.

## Data Sources

The following CSV files are ingested from the `source_file` directory in the Git repository:

- `students.csv`
- `assignments.csv`
- `courses.csv`
- `submissions.csv`

## Data Ingestion Process

This module is responsible for ingesting raw CSV files into tables within Microsoft Fabric's Bronze layer using a data pipeline.

- Reads the raw CSV files from the `source_file` directory.
- Stores the resulting Delta tables in the Bronze layer on OneLake.

## Input

| File Name       | Location           |
|-----------------|--------------------|
| students.csv    | `source_file/`     |
| assignments.csv | `source_file/`     |
| courses.csv     | `source_file/`     |
| submissions.csv | `source_file/`     |

## Output

| Table Name  | Storage Location on OneLake            |
|-------------|--------------------------------------|
| students    | Bronze layer Delta table in OneLake  |
| assignments | Bronze layer Delta table in OneLake  |
| courses     | Bronze layer Delta table in OneLake  |
| submissions | Bronze layer Delta table in OneLake  |



# 2. Data Cleaning and Joining (Silver Layer)

Data cleaning and joining to create refined data in the Silver layer are performed using notebooks within Microsoft Fabric.

* **Input**: Bronze layer Delta tables.
* **Transformations**:
    * Null handling for relevant columns.
    * Type casting, especially for date/timestamp columns like `submitted_at` and `due_date`.
* **Output**: Delta tables stored in the `data/silver` directory:
    * `silver_student_submission_view`: A joined view of `students`, `submissions`, and `assignments`.
    * `silver_assignment_course_view`: A joined view of `assignments` and `courses`.
    * `silver_submission_status_view`: A matrix showing the submission status for each student-assignment pair.

# 3. Analytical Outputs (Gold Layer)

The final analytical outputs based on the Silver layer tables are performed using notebooks within Microsoft Fabric.

* **Input**: Silver layer Delta tables.
* **Output**: Delta tables stored in the `Gold` layer:
    * `gold_not_submitted_assignment_101`: Lists students who did not submit `Assignment_101`.
    * `gold_submission_rate_per_course`: Calculates the percentage of actual versus expected submissions per course.
    * `gold_overdue_assignments_per_student`: Counts the number of late submissions for each student.

# 4. Getting the Output After the Full Pipeline Runs Succeccfully

Executing the Generating_output notebook produces the final JSON output by leveraging PySpark queries to retrieve the data.
