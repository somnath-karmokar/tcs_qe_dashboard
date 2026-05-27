# QE Metrics Dashboard - Full Stack Application

This document provides a comprehensive guide on how to launch the Quality Engineering (QE) Metrics Dashboard, including the React Frontend, the FastAPI Backend, and the Streamlit Admin interface. It also covers the workflow for uploading and analyzing new monthly KPI data.

---

## 1. Prerequisites

Before running the application, ensure you have the following installed on your machine:
- **Node.js & npm** (For the Frontend)
- **Python 3.9+** (For the Backend & Admin)

---

## 2. Starting the Application

The application is split into three main components. You should run each of these in a separate terminal window.

### Step A: Start the FastAPI Backend
The backend serves the API endpoints and the AI Copilot integrations.

1. Open a new terminal.
2. Navigate to the backend directory:
   ```bash
   cd d:\TCS_work\matricsdashboard_backend
   ```
3. *(Optional but recommended)* Activate your Python virtual environment if you have one.
4. Run the Uvicorn server:
   ```bash
   uvicorn app.main:app --reload
   ```
   *The backend will now be accessible at `http://127.0.0.1:8000`*

### Step B: Start the React Frontend
The frontend is built with Vite and React.

1. Open a new terminal.
2. Navigate to the frontend directory:
   ```bash
   cd d:\TCS_work\metricsdashboardapp
   ```
3. Start the development server:
   ```bash
   npm run dev
   ```
   *The frontend dashboard will now be accessible at `http://localhost:5173`*

### Step C: Start the Streamlit Admin Portal
The Admin portal is used to manage domains, portfolios, and upload new monthly datasets.

1. Open a third terminal.
2. Navigate to the backend directory:
   ```bash
   cd d:\TCS_work\matricsdashboard_backend
   ```
3. Run the Streamlit app:
   ```bash
   streamlit run streamlit_admin.py
   ```
   *The Admin portal will open automatically in your browser (usually at `http://localhost:8501`).*

---

## 3. How to Upload & Analyze a New KPI Month

When a new month concludes, you can upload the new metrics to the dashboard via the Streamlit Admin portal. 

### 1. Prepare your Dataset
Ensure you have the new month's metrics ready in the expected format (e.g., an Excel spreadsheet matching the standardized category and metric mappings used by your dashboard).

### 2. Access the Admin Portal
Navigate to the Streamlit Admin UI (`http://localhost:8501`).

### 3. Upload the File
1. In the sidebar or main interface, locate the **Data Upload** section.
2. Select the **Domain** and **Portfolio** you are uploading data for (or create a new one).
3. Select the **Target Month** from the dropdown (e.g., `Apr 2026`).
4. Upload your Excel or CSV dataset.

### 4. Trigger AI Analysis
Once the data is successfully ingested, the system needs to analyze the trends against the historical 6-month baseline to power the Copilot chat and Dashboard Insights.
1. In the Streamlit Admin portal, navigate to the **Generate Analysis** section.
2. Select the newly uploaded month (e.g., `Apr 2026`).
3. Ensure the **"Use LLM enhancement"** toggle is checked (this allows OpenAI / Azure OpenAI to parse the anomalies and build prescriptive recommendations).
4. Click **Start Monthly Analysis**.
5. The backend will process the metrics, generate insights, and update the vector database for the Chat Assistant.

### 5. View on Dashboard
1. Open the React Frontend (`http://localhost:5173`).
2. You will now see the new month available in the top-right date selector.
3. The dashboard cards, anomaly highlights, and the AI Copilot Assistant will now fully incorporate the newest data!

---

## 4. Configuring AI Services (OpenAI vs Azure OpenAI)
The backend supports dynamic switching between standard OpenAI and Azure OpenAI.
- Navigate to `d:\TCS_work\matricsdashboard_backend\.env`
- To use Azure, set `USE_AZURE_OPENAI=true` and fill in your Azure endpoints. 
- To use standard OpenAI, set `USE_AZURE_OPENAI=false` and provide your standard `OPENAI_API_KEY`.
*(Restart the FastAPI backend if you change these environment variables).*
