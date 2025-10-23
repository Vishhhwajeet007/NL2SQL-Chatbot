# 🤖 MySQL Chatbot: Talk to Your Data with LangChain and Groq

Welcome to the repository for a cutting-edge **Natural Language MySQL Chatbot**! This project demonstrates how to build a user-friendly application that allows you to interact with your MySQL database using plain English.

By leveraging the power of **LangChain** for orchestration, an **LLM via Groq** for language-to-SQL translation, and **Streamlit** for a slick user interface, this chatbot turns complex data querying into a simple conversation.

---

## ✨ Features

* **Natural Language to SQL:** Translate user questions (e.g., "What are the top 5 highest-selling products?") directly into executable MySQL queries using a Large Language Model.
* **Real-time Database Interaction:** Connects securely to any MySQL instance to execute the generated queries and fetch results.
* **Conversational Memory:** Utilizes LangChain's history management to understand follow-up questions within the same chat session.
* **Streamlit GUI:** A dynamic, intuitive, and easy-to-use web interface for chatting with your database.
* **Groq Integration:** Uses the **Groq API** for high-speed, low-latency LLM inference, making the chat experience feel instantaneous.
* **Modular Python Code:** Built entirely in Python using modern libraries, making it easy to understand, extend, and adapt.

---

## 🛠️ Tech Stack

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| **Orchestration** | **LangChain** | Manages the sequence of calls (prompting, SQL execution, result formatting). |
| **LLM Inference** | **Groq** (`openai/gpt-oss-120b`) | Provides a fast and powerful LLM for generating SQL and natural language responses. |
| **Database** | **MySQL** | The backend database queried by the chatbot. |
| **Frontend** | **Streamlit** | Creates the interactive web-based chat interface. |
| **Environment** | **`python-dotenv`** | Securely manages API keys and connection details. |

---

## ⚙️ How It Works

The chatbot follows a two-step **LangChain** sequence, designed for robustness and accuracy:

1.  **SQL Generation Chain:** The user's natural language question, along with the database **schema** and **chat history**, is passed to the LLM. The LLM's task is strictly to generate the corresponding, unformatted **MySQL query** only.
2.  **Response Synthesis Chain:**
    * The generated SQL query is executed against the connected MySQL database using `db.run()`.
    * The resulting data (SQL Response) is then combined with the original **question**, **schema**, and **chat history**.
    * This complete context is passed back to the LLM, which synthesizes a final, easy-to-read **natural language answer** for the user.

---

## 🚀 Getting Started

### Prerequisites

1.  **Python:** Ensure you have Python 3.9+ installed.
2.  **MySQL Database:** You need access to a running MySQL instance and a database you want to query.
3.  **Groq API Key:** Get an API key from [Groq Console](https://console.groq.com/keys).

### Installation

1.  **Clone the Repository:**
    ```bash
    git clone [YOUR_REPO_URL]
    cd [YOUR_REPO_NAME]
    ```

2.  **Create a Virtual Environment (Recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Linux/macOS
    .\venv\Scripts\activate    # On Windows
    ```

3.  **Install Dependencies:**
    Create a `requirements.txt` file (if you haven't already) containing the following:

    ```
    langchain
    langchain-core
    langchain-community
    langchain-groq
    streamlit
    python-dotenv
    mysql-connector-python
    ```

    Install them with:
    ```bash
    pip install -r requirements.txt
    ```

4.  **Set Up Environment Variables:**
    Create a file named **`.env`** in the root directory and add your Groq API key:
    ```
    GROQ_API_KEY="YOUR_GROQ_API_KEY_HERE"
    ```

### Running the App

1.  **Launch Streamlit:**
    ```bash
    streamlit run app.py
    ```
    *(Assuming your main script is named `app.py`)*

2.  **Connect to MySQL:**
    * The Streamlit app will open in your browser.
    * Use the **Sidebar** to enter your MySQL connection details: `Host`, `Port`, `User`, `Password`, and `Database Name`.
    * Click the **"Connect"** button.

3.  **Start Chatting!**
    Once connected, you can type your questions in the chat interface.

---

## 📂 Code Structure Overview

The core logic is contained within your main application file (`app.py`):

| File/Function | Description |
| :--- | :--- |
| **`app.py`** | Main Streamlit application file containing all setup and logic. |
| `init_database()` | Initializes the `SQLDatabase` object for LangChain using user-provided credentials. |
| `get_sql_chain(db)` | The chain responsible for generating the raw SQL query. |
| `get_response()` | The full chain that executes the SQL, retrieves the data, and generates the final natural language response. |
| **Streamlit UI** | Handles session state, input forms, and rendering the chat messages. |
