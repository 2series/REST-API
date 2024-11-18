# Loading Data from a REST API using DLT

1. <thinking>
   a. Load data from a REST API using DLT. The provided text explains the process step by step.  The approach will be to extract the key steps and information from the tutorial and present them concisely.

   b. Plan of Steps:
      1. Briefly introduce DLT and its purpose in this context.
      2. Outline the prerequisites for following the tutorial.
      3. Summarize the process of setting up a new DLT project.
      4. Explain the core components of the `rest_api_source` configuration.
      5. Describe the options for handling data updates (append, replace, merge).
      6. Explain how to implement incremental loading.

2. Chain of Thought:
   1. DLT simplifies data extraction from REST APIs by handling pagination, authentication, and loading.
   2. Prerequisites include Python 3.9+, a virtual environment, and DLT installed.
   3. Project setup involves initializing a project with `dlt init rest_api duckdb` and installing dependencies.
   4. `rest_api_source` configuration includes `client` (base URL), `resource_defaults` (default parameters), and `resources` (resources to load).
   5. `write_disposition` controls data updates: `append` (default), `replace`, or `merge` (requires a primary key).
   6. Incremental loading uses the `since` parameter with `type: "incremental"`, `cursor_path`, and `initial_value`.

</thinking>

1. <output>
DLT (Data Load Tool) simplifies extracting data from REST APIs and loading it into various destinations. This summary outlines the steps involved in loading data from a REST API using DLT into a DuckDB database.

**Prerequisites:**

* Python 3.9 or higher
* Virtual environment
* DLT installed (`pip install dlt`)

**Project Setup:**

1. Initialize a new DLT project: `dlt init rest_api duckdb`
2. Install project dependencies: `pip install -r requirements.txt`

**REST API Source Configuration:**

The core of the process lies in configuring the `rest_api_source`.  This involves:

* **`client`:** Specifies the `base_url` of the API.
* **`resource_defaults`:** Sets default parameters for all resources, such as pagination limits.
* **`resources`:** Lists the API resources to load. DLT uses conventions to determine endpoint URLs.  DLT automatically handles pagination for REST APIs that follow best practices.
* **`write_disposition`:**  Controls how data is loaded into the destination. Options include:
    * `append`: Adds new data to the existing table (default).
    * `replace`: Replaces the entire table with new data.
    * `merge`: Updates existing data and adds new data based on a primary key.

**Incremental Loading:**

For APIs that support it, incremental loading fetches only new or changed data. This is achieved using the `since` parameter within the `resources` configuration:

* `type`: Set to `"incremental"`.
* `cursor_path`: Specifies the JSON path to the field used for tracking changes (e.g., `updated_at`).
* `initial_value`: Provides the starting value for the incremental parameter.

**Running the Pipeline:**

Execute the pipeline using `python <your_pipeline_script>.py`.

**Data Exploration:**

Use the built-in data browser (requires `pip install streamlit`) to explore the loaded data: `dlt pipeline <pipeline_name> show`.

This summary provides a concise overview of loading data from REST APIs using DLT. Refer to the full DLT documentation for more advanced configurations and details.
</output>
