# powerBi-task-3

# **Company name** : CODETECH IT SOLUTIONS
# **Name** : Mudunuru Rahul varma
# **Intern ID** :CT04DN302
# **Domain** : Power BI
# **Duration** : 4 weeks
# **Mentor** :Neela Santosh
# Description
Setting up a real-time dashboard using streaming data in **Power BI** enables organizations to monitor live information and react instantly to changes. Whether you're tracking IoT devices, monitoring system health, or visualizing sales performance, Power BI provides robust tools to integrate real-time data from services like **Azure Event Hubs**, **Azure Stream Analytics**, or custom **API feeds**. Here's a comprehensive explanation of how to set up such a dashboard using either Azure or a simulated feed.

---

## What Is a Real-Time Dashboard?

A real-time dashboard in Power BI displays data that updates automatically as new data points are pushed into the system. This contrasts with traditional dashboards that require periodic refreshes. Real-time dashboards are built on **streaming datasets**, which are continuously updated through external services or APIs.

---

## Streaming Data Architecture

A typical real-time data pipeline involves the following components:

1. **Data Source**: This can be a device (IoT sensor, system log, etc.), an application emitting events, or a simulated feed.
2. **Data Ingestion**:

   * Use **Azure Stream Analytics**, **Azure Event Hub**, or a custom app.
   * For simulations, a script (e.g., Python) can push data periodically to a Power BI endpoint.
3. **Streaming Dataset** in Power BI: Accepts incoming data through the Power BI REST API.
4. **Dashboard**: Consumes the dataset to display dynamic, live visuals.

---

## Step-by-Step Setup Using a Simulated API Feed

### 1. Create a Streaming Dataset in Power BI

Log in to the Power BI service ([https://app.powerbi.com](https://app.powerbi.com)) and navigate to **My Workspace > Datasets > + Create > Streaming Dataset**.

Choose **API** as the source. Define the schema for your dataset based on your use case. For example, a sensor dataset might include:

```json
{
  "timestamp": "datetime",
  "temperature": "number",
  "humidity": "number",
  "device": "text"
}
```

Enable **historic data analysis** if you plan to use reports, not just dashboards. Click **Create**, and Power BI will provide a unique **Push URL** for the dataset.

### 2. Simulate Real-Time Data Push with Python

A Python script can simulate sensor readings and push data to Power BI every few seconds using the REST API:

```python
import requests, json, random, time
from datetime import datetime

URL = 'https://api.powerbi.com/beta/your_push_url'

while True:
    data = [{
        "timestamp": datetime.utcnow().isoformat(),
        "temperature": round(random.uniform(20.0, 30.0), 2),
        "humidity": round(random.uniform(30.0, 60.0), 2),
        "device": "Sensor-A"
    }]
    response = requests.post(URL, json=data)
    print(f"Pushed: {data} | Status: {response.status_code}")
    time.sleep(5)
```

Replace `"your_push_url"` with your actual Push URL from Power BI.

This script pushes new data every 5 seconds, mimicking live telemetry or streaming input.

### 3. Build the Real-Time Dashboard

In Power BI Service:

* Go to your dashboard
* Click **+ Add tile > Real-time data**
* Select your streaming dataset
* Choose a visual type (e.g., line chart, card, gauge)
* Configure your visual with appropriate fields (e.g., timestamp vs. temperature)

Power BI will now automatically update the visual as new data arrives.

---

## Using Azure for Enterprise-Grade Streaming

For production-grade systems, **Azure Stream Analytics** is recommended. The workflow involves:

1. **Input**: Azure IoT Hub or Event Hub
2. **Stream Analytics Job**: Filters/transforms data
3. **Output**: Power BI streaming dataset

You must authorize Power BI in the Azure portal, create a Stream Analytics job, and route the output to Power BI.

---

## Benefits of Real-Time Dashboards

* **Immediate insights**: Monitor live metrics such as temperature, traffic, or sales.
* **Automation**: Trigger alerts or workflows based on threshold breaches.
* **Scalability**: Handle thousands of events per second using Azure infrastructure.

---

In conclusion, setting up a real-time dashboard in Power BI—whether with Azure services or a simulated feed—is a powerful way to gain live visibility into your data. For testing or small-scale use, a script-based simulation is sufficient. For enterprise applications, Azure Stream Analytics provides a robust, scalable pipeline for continuous data analysis and visualization.

# OUTPUT


