# Invoice Accounting Automation for ACME

This Robotic Process Automation (RPA) project, developed with **UiPath**, automates the registration of sales invoices in the **ACME System 1** web application. The solution is built using the **REFramework** and follows a Dispatcher/Performer architecture to ensure efficiency, scalability, and robust error handling.

## Process Description

The goal of this project is to eliminate the manual workload associated with invoice accounting. The automated process is responsible for:
1.  Reading a sales report containing multiple invoices.
2.  Extracting relevant data from each invoice (Vendor Tax ID, number, date, and amount).
3.  Registering each invoice individually in the ACME System 1 web portal.

## Solution Architecture

The project uses a **Dispatcher/Performer** model to separate responsibilities and improve process robustness.

### 1. Dispatcher
- **Responsibility**: Reads the input file with the list of invoices.
- **Actions**:
    - Iterates through each row of the sales report.
    - Validates the basic data of each invoice.
    - Adds each invoice as a new transaction item to a **Queue** in UiPath Orchestrator.

### 2. Performer
- **Responsibility**: Processes each invoice individually.
- **Actions**:
    - Gets a transaction item from the Orchestrator Queue.
    - Logs into the ACME System 1 web application.
    - Enters the invoice data into the corresponding form.
    - Updates the transaction item's status (Successful, Application Exception, or Business Rule Exception).

## Key Features
- **Framework**: Built on **REFramework** for robust transaction and exception handling.
- **Scalability**: The use of Orchestrator Queues allows for processing a high volume of invoices by simply adding more robots to the Performer process.
- **Resilience**: If an item fails, it can be automatically retried without stopping the entire process. Business Rule Exceptions (e.g., incorrect data) are logged for manual review.
- **Security**: ACME system credentials are managed securely using Orchestrator **Assets**.
- **Modularity**: The Dispatcher and Performer logic is completely separate, facilitating maintenance and future updates.

## Technologies Used
- **UiPath Studio**: For developing the automation workflows.
- **UiPath Orchestrator**: For managing Queues, Assets, and running the robots.
- **REFramework**: As the base template for both the Dispatcher and Performer processes.

## Prerequisites
- UiPath Studio and a Robot (Attended or Unattended) installed and configured.
- Access to a UiPath Orchestrator instance connected to Studio.
- Login credentials for the [ACME System 1](https://acme-test.uipath.com/login) web application.

## Environment Setup

To run this project, follow these setup steps in UiPath Orchestrator:

1.  **Create the Queue**:
    - Go to your Tenant > Queues.
    - Create a new queue. The name of this queue must match the `OrchestratorQueueName` value in the `Config.xlsx` file.

2.  **Create the Assets**:
    - Go to your Tenant > Assets.
    - Create a **Credential** type asset to store the ACME username and password. The name of this asset must match the `ACME_Credential` value in the `Config.xlsx` file.

3.  **Configure the `Config.xlsx` File**:
    - Open the project in UiPath Studio.
    - Navigate to the `Data` folder and open the `Config.xlsx` file.
    - In the **Settings** sheet, ensure that the values for `OrchestratorQueueName` and `ACME_Credential` match the names you created in Orchestrator.
    - In the **Constants** sheet, verify that the `ACME_URL` value is correct.

## Running the Process

1.  **Run the Dispatcher**:
    - Open the Dispatcher project in UiPath Studio.
    - Run the `Main.xaml` file.
    - The robot will read the input data and load the invoices into the Orchestrator queue.

2.  **Run the Performer**:
    - Open the Performer project in UiPath Studio.
    - Run the `Main.xaml` file.
    - The robot will start getting and processing invoices from the queue one by one until no items are left. You can also run this process directly from Orchestrator. 

## Citation & License
Please cite as: Molina Delgado, M. (2025). AI Agents & Automation: Complement or Competition for IT Ops?

## Citation & License
Please cite as: Molina Delgado, M. (2025). RPA Invoice Accounting Automation.

## Author & Mentor
**Author** Miqueas Molina Delgado 
**Tutor:** Andrés Díaz Romero
