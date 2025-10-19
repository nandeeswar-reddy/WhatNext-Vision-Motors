# README: WhatsNext Vision Motors Salesforce Implementation

---

### Project Overview

This project describes the implementation of a custom **Salesforce CRM** solution for **WhatsNext Vision Motors**, an emerging leader in the automotive sector.The primary goal was to modernize customer interaction and operational processes, focusing on streamlining **vehicle order management**, ensuring accurate **dealer assignment**, and enhancing **customer engagement** through automation.The solution was designed to overcome issues caused by previous manual processes, such as delays, stock mismanagement, and customer dissatisfaction.

---

### Core Objectives

[cite_start]The Salesforce implementation was guided by the following key objectives[cite: 9, 10]:

* **Enhance Customer Satisfaction:** Automatically suggest the nearest authorized dealer to a customer based on their location for a seamless ordering experience.
* **Ensure Order Accuracy and Fulfillment:** Implement **real-time stock validation** to prevent customers from placing orders for vehicles that are currently out of stock.
* **Streamline Operations with Automation:** Develop sophisticated automation using **Apex and Flows** to efficiently manage customer orders and test drives.
* **Maintain Data Integrity and Scalability:** Use **Batch Apex** to periodically and reliably update vehicle stock data for large data volumes.
* **Proactive Customer Communication:** Automate email reminders for scheduled test drives to reduce no-shows and improve engagement.

---

### Technology Stack

The project is built entirely on the **Salesforce Platform**, utilizing its core CRM and customization capabilities.

| Component | Purpose | Details |
| :--- | :--- | :--- |
| **Salesforce CRM** | Core platform for data management and tracking | Stores and manages vehicle details, stock, dealer info, customer records, orders, and test drives. |
| **Apex and Apex Triggers** | Enforce complex, real-time business rules. | Used for **real-time stock validation** on order creation and **automatic dealer assignment** logic. |
| **Batch Apex** (`VehicleOrderBatch`) | Process large data volumes efficiently. | Periodically checks stock replenishment and updates pending `Vehicle_Order__c` statuses to 'Confirmed'. |
| **Scheduled Apex** (`VehicleOrderBatchScheduler`) | Automate the execution of batch jobs. | Schedules the `VehicleOrderBatch` to run daily at 12:00 PM. |
| **Record-Triggered Flows** | Declarative automation for specific processes. | Used for the **Auto Assign Dealer Flow** and the **Test Drive Reminder Flow**. |
| **Lightning App Builder** | Provides a modern, consolidated user interface. | Created the dedicated **WhatsNext Vision Motors Lightning App** for internal users. |
| **Data Modelling** | Structuring the data for the vehicle lifecycle. | Implemented six **Custom Objects** (`Vehicle__c`, `Vehicle_Order__c`, etc.) with essential fields and relationships. |

---

### Key Automation Features

#### 1. Real-Time Stock Validation (Apex Trigger)
* The `VehicleOrderTrigger` fires *before* the insertion of a new `Vehicle_Order__c` record.
* Logic in the handler class checks the `Stock_Quantity__c` of the selected vehicle.
* Prevents the order from being created if the stock quantity is zero or less, mitigating the creation of unfulfillable orders.

#### 2. Automatic Dealer Assignment (Flow)
* The **Auto Assign Dealer Flow** runs when a `Vehicle_Order__c` is **Created** with a status of **'Pending'**.
* It retrieves the customer's address and queries the `Vehicle_Dealer__c` object to find the nearest dealer matching the customer's location.
* The flow then automatically updates the Order record with the assigned dealer.

#### 3. Proactive Test Drive Reminders (Flow)
* The **Test Drive Reminder Flow** is triggered when a `Vehicle_Test_Drive__c` record is Created or Updated.
* It uses a **Scheduled Path** to execute **1 Day Before** the `Test_Drive_Date__c`.
* An email action sends a reminder to the customer's email address, reducing no-shows and enhancing customer service.

---

### Project Demo

The complete working functionality and user interface of the WhatsNext Vision Motors Salesforce implementation can be viewed here:

[Project Demo Link](https://drive.google.com/file/d/1a4x6KBvcB8CUzDZfCZRBJy7eoeT9ygWC/view?usp=sharing)
