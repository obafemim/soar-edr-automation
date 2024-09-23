# SOAR & EDR Automation Project

This project automates the detection and response process using **LimaCharlie** for endpoint detection and response (EDR) and **Tines** for security orchestration and automation (SOAR). The system triggers alerts when suspicious activity is detected and provides users with options to isolate affected machines or allow continued network access.

## Table of Contents
1. [Overview](#overview)
2. [Technologies Used](#technologies-used)
3. [Architecture](#architecture)
4. [Setup Instructions](#setup-instructions)
5. [Process Workflow](#process-workflow)
6. [Results](#results)
7. [Future Improvements](#future-improvements)

---

## Overview
This project demonstrates a fully automated **SOAR & EDR** system that responds to detected threats by using **LimaCharlie** to identify suspicious activity and **Tines** to automate the response. When a tool like **LaZagne** is executed, an alert is triggered, and the system offers users the option to isolate the affected machine or allow it to continue normal operation.

---

## Technologies Used
- **LimaCharlie**: Endpoint detection and response (EDR) system used to detect suspicious activity on machines.
- **Tines**: Security orchestration and automation (SOAR) platform used to automate responses and trigger user interaction.
- **Slack** (optional): For sending user notifications and allowing communication during decision points.

---

## Architecture

The architecture of this system involves the following components:
- **LaZagne**: A post-exploitation tool that simulates suspicious activity and serves as the trigger for the workflow.
- **LimaCharlie**: Detects the execution of LaZagne and triggers alerts.
- **Tines**: Receives alerts from LimaCharlie and orchestrates the workflow by prompting the user for a response.
- **User Decision Point**: The user is prompted with two options:
   - **Isolate the machine** from the network.
   - **Allow the machine** to continue accessing the network.

---

## Setup Instructions

### Prerequisites
- **LimaCharlie** account and sensor deployed on the endpoint.
- **Tines** account to create the workflow automation.
- **LaZagne** executable to simulate suspicious activity.

### Steps to Set Up:
1. **Deploy LimaCharlie** on the target endpoint (Windows, macOS, or Linux).
   - Use LimaCharlie to monitor the machine and configure detection for **LaZagne** execution.
2. **Create a Workflow in Tines**:
   - Set up an integration between LimaCharlie and Tines to receive alerts.
   - Build a Tines workflow to handle incoming alerts and prompt the user for action.
3. **Configure User Actions** in Tines:
   - Option 1: **Isolate the machine** via LimaCharlie’s commands.
   - Option 2: **Allow continued access**, clearing the alert.

---

## Process Workflow

1. **Step 1: Execute LaZagne**  
   The **LaZagne** executable is downloaded and run on the endpoint.  
   LimaCharlie monitors the activity and detects the execution.

   ![LaZagne Execution](images/Screenshot%202024-09-22%20143651.png)

2. **Step 2: LimaCharlie Detection**  
   Upon execution of LaZagne, **LimaCharlie** triggers an alert.  
   The alert is forwarded to **Tines**.

   ![LimaCharlie Detection](images/Screenshot%202024-09-22%20180129.png)

3. **Step 3: Tines User Prompt**  
   Tines receives the alert and triggers a workflow.  
   The user is prompted via a **Tines interface** (or through a Slack message) with two options:  
   - **Isolate the machine**.  
   - **Allow the machine** to continue.

   ![Tines User Prompt](images/Screenshot%202024-09-22%20201224.png)

4. **Step 4: User Decision**  
   Based on the user's decision:
   - **Isolation**: The machine is isolated from the network using LimaCharlie’s endpoint isolation feature.
   - **Allow access**: No further action is taken, and the machine remains connected.

   ![User Decision](images/Screenshot%202024-09-22%20172900.png)

5. **Step 5: Final Action**  
   The system either isolates the machine or allows continued access based on the decision.  
   The final logs and alerts are recorded.

   ![Final Action - Logs](images/Screenshot%202024-09-22%20180458.png)

---

## Results
- Successfully detected the execution of **LaZagne** on the endpoint using **LimaCharlie**.
- Automated response via **Tines**, prompting the user to decide between isolation or continued network access.
- Reduced response time to incidents by automating the detection and response process.

---

## Future Improvements
- Integrating **additional triggers** for other potentially malicious executables or activities.
- Adding further automation, such as integrating **Slack** for real-time notifications of incidents.
- Improving the isolation process by adding more granular control over which network services are blocked.

---

