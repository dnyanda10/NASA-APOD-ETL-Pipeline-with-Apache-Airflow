## 📌 Project Overview
This project implements an **ETL pipeline** using **Apache Airflow** to fetch NASA’s Astronomy Picture of the Day (APOD) data via API, transform it, and store it in a **PostgreSQL database** hosted on **AWS RDS**.  
The pipeline is fully **containerized with Docker** and deployed to **Astronomer Cloud** for automated production scheduling.

**Use Case:** Automates ingestion of NASA APOD data for analytical purposes, reporting, and visualizations.


## 🛠️ Tech Stack
- **Apache Airflow** (via Astronomer CLI)
- **Python**
- **PostgreSQL** (AWS RDS)
- **NASA API**
- **Docker**
- **Astronomer Cloud**
  

  ## 🖼️ Sample Data
The following screenshot shows a sample of the data ingested into the `apod_data` table in PostgreSQL:
![Sample Data](Images/sample_data_airflow_project.jpg)


## 📂 Project Structure
```text
.
├── .astro/                    # Astronomer configuration files
├── Architecture Diagram/      # Contains architecture diagrams for documentation
├── dags/                      # Airflow DAG scripts
├── tests/                     # Unit tests (if applicable)
├── Images/                     # Sample screenshots and data visuals
├── .dockerignore
├── .env                        # Local environment variables (ignored in Git)
├── .gitignore
├── airflow_settings.yaml       # Airflow connection setup
├── docker-compose.yml          # Local Airflow environment setup
├── Dockerfile                  # Custom image for Astronomer deployment
├── README.md
├── requirements.txt            # Python dependencies

```

## ⚙️ Airflow Connections Used
The following Airflow connections are configured for this project:

1- nasa_api
   - Type: HTTP
   - Host: https://api.nasa.gov
   - Extra: API Key stored as an environment variable (NASA_API_KEY)

2- my_postgres_connection
   - Type: Postgres
   - Host: AWS RDS endpoint
   - Login: RDS username
   - Password: RDS password
   - Database: Target PostgreSQL DB


## 📜 DAG Workflow

 - Create Table – Ensures the apod_data table exists in Postgres.
 - Extract Data – Calls NASA APOD API using HttpOperator.
 - Transform Data – Filters and structures JSON response using TaskFlow API.
 - Load Data – Inserts transformed data into Postgres using PostgresHook.


## 🚀 Deployment to Production with Astronomer.io
This project is deployed to Astronomer Cloud for production orchestration.

## Steps:
1- Set up Astronomer Cloud Workspace
    - Create a new workspace in Astronomer.io and link your GitHub repo.

2- Configure Production Environment
    - Create .env file with production credentials:

     NASA_API_KEY=your_prod_api_key
     POSTGRES_USER=your_prod_user
     POSTGRES_PASSWORD=your_prod_password
     POSTGRES_HOST=your_rds_endpoint.amazonaws.com
     POSTGRES_DB=your_prod_db

3- Set Airflow Connections in Astronomer UI
     - nasa_api → HTTP with host https://api.nasa.gov
     - my_postgres_connection → Postgres with AWS RDS hostname

4- Deploy to Astronomer
     - astro deploy <deployment-id>
     
5- Monitor & Scale
     - Use Astronomer Cloud to monitor DAG runs and adjust resources.
     
     
     
## 📅 DAG Schedule
- DAG runs daily at 10:00 UTC to retrieve the latest APOD.
- Note: Schedule can be adjusted in the DAG's schedule_interval.
  
  

## 🏆 Key Highlights
- Fully containerized Airflow setup
- Automated daily API data ingestion
- AWS RDS integration for persistence
- Production-ready deployment via Astronomer.io
  
  

## 🎯 Learning Outcomes
- How to orchestrate ETL pipelines in Airflow
- Using Airflow Hooks & Operators for API and DB operations
- Managing connections securely in Airflow
- Dockerizing Airflow with PostgreSQL setup






