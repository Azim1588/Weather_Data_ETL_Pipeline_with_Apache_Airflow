# Weather_Data_ETL_Pipeline_with_Apache_Airflow
This repository contains an Apache Airflow  (DAG) for extracting, transforming, and loading weather data from the OpenWeatherMap API to an S3 bucket. The pipeline also sends notifications to a Slack channel upon completion.


## Project Overview

The DAG performs the following tasks:
1. **Extract and Transform Weather Data**: Fetches weather data for several cities using the OpenWeatherMap API, transforms it into a DataFrame, and saves it as a CSV file.
2. **Load Data to S3**: Uploads the generated CSV file to an AWS S3 bucket.
3. **Slack Notification**: Sends a notification to a Slack channel to inform about the successful execution of the pipeline.

## Prerequisites

- Apache Airflow
- AWS CLI configured with appropriate permissions
- Slack webhook URL
- Python libraries: `requests`, `pandas`

## Installation

1. **Clone the Repository**

    ```bash
    git clone https://github.com/Azim1588/airflow-weather-data-pipeline.git
    cd airflow-weather-data-pipeline
    ```

2. **Install Dependencies**

    ```bash
    pip install -r requirements.txt
    ```

3. **Configure Airflow**

    - Set up your Airflow environment according to the [Airflow documentation](https://airflow.apache.org/docs/apache-airflow/stable/).
    - Add a Slack webhook connection in Airflow with the `slack_conn_id` used in the DAG.

4. **AWS S3 Setup**

    - Make sure your AWS CLI is configured properly with the necessary permissions to upload files to your S3 bucket.

## DAG Description

### `weather_dag`

- **Schedule Interval**: Runs daily (`@daily`).
- **Tasks**:
    1. **Extract and Transform Weather Data**
        - Fetches weather data for predefined cities.
        - Transforms the data and saves it as a CSV file.
    2. **Load Data to S3**
        - Uploads the CSV file to the specified S3 bucket.
    3. **Slack Notification**
        - Sends a notification to the Slack channel upon successful completion.

## Code Explanation

### `etl_weather_data` Function

- Fetches weather data from the OpenWeatherMap API for a list of cities.
- Transforms the data into Fahrenheit and calculates other required fields.
- Saves the data into a CSV file.

### DAG Configuration

- Uses `PythonOperator` for the ETL process.
- Uses `BashOperator` to upload the CSV file to S3.
- Uses `SlackWebhookOperator` to send notifications.

## Example Output

![Weather Data Example](path/to/your/image.png)

## How to Run

1. **Start Airflow Scheduler and Webserver**

    ```bash
    airflow scheduler
    airflow webserver
    ```

2. **Trigger the DAG**

    - Open the Airflow web interface.
    - Manually trigger the `weather_dag` or wait for the scheduled interval.

## Troubleshooting

- **ModuleNotFoundError**: Ensure all required Python packages are installed.
- **AWS S3 Upload Issues**: Verify AWS CLI configuration and bucket permissions.
- **Slack Notifications**: Check Slack webhook configuration and channel permissions.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contributing

Feel free to open issues or submit pull requests if you have improvements or bug fixes.

## Contact

For any questions or feedback, please contact:

- **Email**: your.email@example.com
