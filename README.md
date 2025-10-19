# README: WhatsNext Vision Motors Salesforce Implementation

---

### Project Overview

[cite_start]This project describes the implementation of a custom **Salesforce CRM** solution for **WhatsNext Vision Motors**, an emerging leader in the automotive sector[cite: 3]. [cite_start]The primary goal was to modernize customer interaction and operational processes, focusing on streamlining **vehicle order management**, ensuring accurate **dealer assignment**, and enhancing **customer engagement** through automation[cite: 3, 4]. [cite_start]The solution was designed to overcome issues caused by previous manual processes, such as delays, stock mismanagement, and customer dissatisfaction[cite: 5, 76].

---

### Core Objectives

[cite_start]The Salesforce implementation was guided by the following key objectives[cite: 9, 10]:

* [cite_start]**Enhance Customer Satisfaction:** Automatically suggest the nearest authorized dealer to a customer based on their location for a seamless ordering experience[cite: 11].
* [cite_start]**Ensure Order Accuracy and Fulfillment:** Implement **real-time stock validation** to prevent customers from placing orders for vehicles that are currently out of stock[cite: 12].
* [cite_start]**Streamline Operations with Automation:** Develop sophisticated automation using **Apex and Flows** to efficiently manage customer orders and test drives[cite: 13].
* [cite_start]**Maintain Data Integrity and Scalability:** Use **Batch Apex** to periodically and reliably update vehicle stock data for large data volumes[cite: 14].
* [cite_start]**Proactive Customer Communication:** Automate email reminders for scheduled test drives to reduce no-shows and improve engagement[cite: 15].

---

### Technology Stack

[cite_start]The project is built entirely on the **Salesforce Platform**, utilizing its core CRM and customization capabilities[cite: 17].

| Component | Purpose | Details |
| :--- | :--- | :--- |
| **Salesforce CRM** | [cite_start]Core platform for data management and tracking[cite: 18]. | [cite_start]Stores and manages vehicle details, stock, dealer info, customer records, orders, and test drives[cite: 18]. |
| **Apex and Apex Triggers** | [cite_start]Enforce complex, real-time business rules[cite: 19]. | [cite_start]Used for **real-time stock validation** on order creation and **automatic dealer assignment** logic[cite: 19]. |
| **Batch Apex** (`VehicleOrderBatch`) | [cite_start]Process large data volumes efficiently[cite: 21, 53]. | [cite_start]Periodically checks stock replenishment and updates pending `Vehicle_Order__c` statuses to 'Confirmed'[cite: 54]. |
| **Scheduled Apex** (`VehicleOrderBatchScheduler`) | [cite_start]Automate the execution of batch jobs[cite: 55]. | [cite_start]Schedules the `VehicleOrderBatch` to run daily at 12:00 PM[cite: 57]. |
| **Record-Triggered Flows** | [cite_start]Declarative automation for specific processes[cite: 23]. | [cite_start]Used for the **Auto Assign Dealer Flow** and the **Test Drive Reminder Flow**[cite: 38, 39, 45]. |
| **Lightning App Builder** | [cite_start]Provides a modern, consolidated user interface[cite: 24]. | [cite_start]Created the dedicated **WhatsNext Vision Motors Lightning App** for internal users[cite: 32]. |
| **Data Modelling** | [cite_start]Structuring the data for the vehicle lifecycle[cite: 22]. | [cite_start]Implemented six **Custom Objects** (`Vehicle__c`, `Vehicle_Order__c`, etc.) with essential fields and relationships[cite: 28, 29]. |

---

### Key Automation Features

#### 1. Real-Time Stock Validation (Apex Trigger)
* [cite_start]The `VehicleOrderTrigger` fires *before* the insertion of a new `Vehicle_Order__c` record[cite: 34, 35].
* [cite_start]Logic in the handler class checks the `Stock_Quantity__c` of the selected vehicle[cite: 35, 62].
* [cite_start]Prevents the order from being created if the stock quantity is zero or less, mitigating the creation of unfulfillable orders[cite: 36, 63, 64].

#### 2. Automatic Dealer Assignment (Flow)
* [cite_start]The **Auto Assign Dealer Flow** runs when a `Vehicle_Order__c` is **Created** with a status of **'Pending'**[cite: 40].
* [cite_start]It retrieves the customer's address and queries the `Vehicle_Dealer__c` object to find the nearest dealer matching the customer's location[cite: 42, 43, 69].
* [cite_start]The flow then automatically updates the Order record with the assigned dealer[cite: 44, 70].

#### 3. Proactive Test Drive Reminders (Flow)
* [cite_start]The **Test Drive Reminder Flow** is triggered when a `Vehicle_Test_Drive__c` record is Created or Updated[cite: 46].
* [cite_start]It uses a **Scheduled Path** to execute **1 Day Before** the `Test_Drive_Date__c`[cite: 47].
* [cite_start]An email action sends a reminder to the customer's email address, reducing no-shows and enhancing customer service[cite: 50, 72, 73].

---

### Project Demo

The complete working functionality and user interface of the WhatsNext Vision Motors Salesforce implementation can be viewed here:

[Project Demo Link](https://drive.google.com/file/d/1a4x6KBvcB8CUzDZfCZRBJy7eoeT9ygWC/view?usp=sharing)
