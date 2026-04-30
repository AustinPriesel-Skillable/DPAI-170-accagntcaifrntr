# Use case 9 - Implement end to end agent operations for Zava’s shopping assistant in Microsoft Foundry

**Introduction**

This lab demonstrates how to implement **end-to-end agent operations**
using Azure AI Foundry by building an intelligent retail assistant named
**Cora** for Zava, a home improvement retailer. It walks through the
complete lifecycle of an AI solution—from provisioning Azure resources
and deploying applications to building, orchestrating, and evaluating AI
agents.

You will gain hands-on experience with Azure services such as **Azure AI
Search, Azure AI Agent Service, and model evaluation tools**, enabling
you to design scalable, intelligent, and production-ready AI
applications.

**Scenario**

Zava is a fictional retail company that sells home improvement products
such as paints, tools, and hardware. To enhance customer experience,
Zava introduces **Cora**, an AI-powered shopping assistant.

Cora helps customers:

- Discover suitable products for their needs

- Compare prices and availability

- Get personalized recommendations (e.g., eco-friendly options)

- Answer product-related queries

As Zava grows, Cora evolves from a **single-agent system** into a
**multi-agent architecture**, incorporating specialized agents like:

- Product Inventory Agent

- Customer Service Agent

Additionally, the solution includes **evaluation pipelines** to ensure
accuracy, quality, and safety before deployment.

**Objectives**

By completing this lab, you will be able to:

- Register required Azure resource providers and set up the environment

- Deploy an AI-powered application using Azure and GitHub Codespaces

- Configure Azure AI Search and create a product index

- Build and interact with a retail AI agent (Cora)

- Implement vector search for product retrieval

- Develop a **multi-agent system** for advanced use cases

- Generate synthetic datasets for testing and evaluation

- Evaluate AI models for performance, quality, and safety

- Apply **GenAIOps practices** for reliable and secure AI deployment

## Task 1: Register Service provider

1.  Open a browser go to +++https://portal.azure.com+++ and sign in with
    your cloud slice account below.

    Username: +++@lab.CloudPortalCredential(User1).Username+++

    Password: +++@lab.CloudPortalCredential(User1).AccessToken+++

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

    ![A login box with a red box and blue box with text AI-generated content
may be incorrect.](./media/image2.png)

2.  Click on **Subscriptions** tile.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

3.  Click on the subscription name.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

4.  Expand Settings from the left navigation menu. Click on **Resource
    providers**, enter +++Microsoft.CognitiveServices+++ and
    select it, and then click **Register**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

    ![A screenshot of a computer AI-generated content may be 
 incorrect.](./media/image7.png)

5.  Repeat the steps #4 to register the following Resource provider.

    - +++**Microsoft.AlertsManagement**+++

## Task 2: Retrieve resource group name and location

1.  Type in +++Resource group+++ in the search bar and
    select **Resource groups**.

    ![A screenshot of a computer AI-generated content may be 
 incorrect.](./media/image8.png)

2.  Click on your assigned **Resource group**.

    ![A screenshot of a computer AI-generated content may be 
 incorrect.](./media/image9.png)

3.  In **Resource group** page, copy **resource group name and
    location** and paste them in a notepad, then **Save** the notepad to
    use the information in the upcoming tasks.

    ![A screenshot of a computer AI-generated content may be 
 incorrect.](./media/image10.png)

## Task 3: Open Github Codespaces environment

1.  Open your browser, navigate to the address bar, type or paste the
    following URL: +++https://github.com/technofocus-pte/observeManageScale-agentic-ai-appsFoundry/tree/feb-2026-refresh+++

2.  Click on **fork** to fork the repo. Give unique name to the repo and
    click on **Create repo** button.

    ![](./media/image11.png)

1.  Click on **Create fork**

2.  Click on **Code > Codespaces > Codespaces**

    ![](./media/image12.png)

    ![](./media/image13.png)

    ![](./media/image14.png)

    ![](./media/image15.png)

## Task 4: Provision Services and deploy application to Azure

1.  Run the following command on the Terminal. It generates the code to
    copy. Copy the code and press Enter.

    +++az login+++

    ![](./media/image16.png)

2.  Default browser opens to enter the generated code to verify. Enter
    the code and click **Next**.

    ![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image17.png)

3.  Sign in with your Azure credentials.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

    ![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image19.png)

    ![](./media/image20.png)

3.  Open a new VS Code Terminal. Complete these steps:

    +++cd scripts+++

    +++./1-setup.sh+++

    ![](./media/image21.png)

4.  Then complete the interactive steps providing responses like this:

    1.  Enter branch name: for-release-1.0.4

    2.  Enter environment name: Ignite-PREL13

    3.  Enter Azure region: @lab.CloudResourceGroup(AgenticAI).Location

    4.  Enter Subscription ID: *your subscription id here*

    5.  Do you want to activate Azure AI Search? (yes/no): yes

    6.  Use these defaults? (yes/no): yes

    7.  Proceed with deployment? (yes/no): yes

    8.  Enter the **Resourcegroup**

    ![](./media/image22.png)

    ![](./media/image23.png)

    ![](./media/image24.png)

    ![](./media/image25.png)

    ![](./media/image26.png)

    ![](./media/image27.png)

5.  Run this script from root of repo - it will create .env with values
    extracted by Azure CLI. By default it looks for an  resource group
    but you can override it.

    +++cd ForBeginners/.azd-setup+++

    +++azd up+++

    ![](./media/image28.png)

6.  When prompted, type **y** and press Enter to log in to Azure before
    continuing with the deployment.

    ![](./media/image29.png)

    ![](./media/image30.png)

4.  Default browser opens to enter the generated code to verify. Enter
    the code and click **Next**.

    ![](./media/image31.png)

5.  Sign in with your Azure credentials.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

    ![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image19.png)

7.  This deployment will take *12-15minutes* to provision the resources
    in your account and set up the solution with sample data.

    ![](./media/image32.png)

    ![](./media/image33.png)

    **Note:** Check the deployment status in your resource group to ensure all resources are provisioned successfully.

    ![](./media/image34.png)

    ![](./media/image35.png)

    ![](./media/image36.png)

    ![](./media/image37.png)

8.  Now the deployment is complete

## Task 5: Interact with Your AI Agent Using Predefined Questions

1.  After the application has been successfully deployed, you see a URL
    displayed in the terminal. Copy the **URL**

    ![](./media/image38.png)

2.  Click on **Open** button

    ![](./media/image39.png)

3.  Wait for the web application deployment to complete.

    ![](./media/image40.png)

2.  In the **agent-template-assistant** web app page, enter the
    following text and click on the **Submit icon** as shown in the
    below image.

    +++Can you help me choose the best tools for painting my house? +++

    ![](./media/image41.png)

    ![](./media/image42.png)

3.  In the **agent-template-assistant** web app page, enter the
    following text and click on the **Submit icon** as shown in the
    below image.

    +++What are the cheapest products available? +++

    ![](./media/image43.png)

    ![](./media/image44.png)

4.  In the **agent-template-assistant** web app page, enter the
    following text and click on the **Submit icon** as shown in the
    below image.

    +++Suggest eco-friendly paint options?+++

    ![](./media/image45.png)

    ![](./media/image46.png)

5.  In the **agent-template-assistant** web app page, enter the
    following text and click on the **Submit icon** as shown in the
    below image.

    +++How much does the Synthetic Brush set cost and do you have it in stock?+++

    ![](./media/image47.png)

    ![](./media/image48.png)

## Task 6: Set up .env variables.

1.  Make sure you are authenticated with Azure CLI. We will use this to
    retrieve and create a .env file based on
    the scripts/.env.sample format

     +++az login+++

2.  Run this script from root of repo - it will create .env with values
    extracted by Azure CLI. By default it looks for
    an rg-Ignite-XXX resource group but you can override it.

     +++./scripts/1-update-env-selfguided.sh+++

3.  Enter the resourcegroup

    ![](./media/image49.png)

    ![](./media/image50.png)

    ![](./media/image51.png)

4.  We have Zava data in scripts/customization. Let's create a product
    index in Azure AI Search. Switch to the scripts/ folder and run the
    command:

     +++cd scripts/+++

     +++python 2-add-product-index.py+++

    ![](./media/image52.png)

    ![](./media/image53.png)

5.  This will first run an RBAC update script to give this user the
    right roles and access to make updates.

6.  Then it should upload 49 products to a zava-products index with
    semantic search, in Azure AI Search.

    ![](./media/image54.png)

## Task 7: Environment Setup & Validation

In this task, you will configure and validate your development
environment. This includes selecting the appropriate Python environment,
installing dependencies, and verifying connectivity to Azure services
and the Foundry project.

1.  Navigate to the **labs/setup/** folder and open the
    **00-validate-setup.ipynb** notebook to begin the environment setup
    lab.

    ![](./media/image55.png)

2.  Click **Select Kernel** in the top-right corner of the notebook and
    choose the appropriate Python environment to run the lab.

    ![](./media/image56.png)

3.  If prompted to select the path, then select the **Python** version
    i.e **3.12.11**

    ![](./media/image57.png)

7.  To import required libraries, run the first cell in the notebook

    ![](./media/image58.png)

    ![](./media/image59.png)

8.  Click the **Run (▶)** button to execute the cell and verify that all
    required Azure AI Foundry environment variables are properly set.

    ![](./media/image60.png)

9.  Click the **Run (▶)** button to execute the cell and validate that
    all required Azure AI Search configuration variables are correctly
    set.

    ![](./media/image61.png)

    ![](./media/image62.png)

10. Click the **Run (▶)** button to execute the cell and confirm that
    all embedding model configuration variables are properly set.

    ![](./media/image63.png)

## Task 8: Build “Cora for Zava” – An AI-Powered Retail Shopping Assistant Using Azure AI Agent Service

**Cora** is a customer service chatbot for **Zava** - a fictitious
retailer of home improvement goods for DIY enthusiasts. Zava offers a
wide range of products including paint, power tools, hand tools,
hardware, electrical supplies, and plumbing materials. Cora helps
customers find products, check inventory, and provides personalized
assistance for home improvement projects.

1.  Navigate to the **labs/setup/** folder and open the
    **11-build-cora-retail-agent.ipynb** notebook to begin the
    environment setup lab.

    ![](./media/image64.png)

2.  Click the **Run (▶)** button to execute the cell and verify that all
    required Python packages are installed successfully.

    ![](./media/image65.png)

3.  Click the **Run (▶)** button to execute the cell and load
    environment variables from the .env file into your notebook.

    ![](./media/image66.png)

4.  Click the **Run (▶)** button to execute the cell and confirm that
    all required environment variables are loaded and ready.

    ![](./media/image67.png)

5.  Click the **Run (▶)** button to execute the cell and establish a
    connection to Azure AI Foundry using the configured credentials.

    ![](./media/image68.png)

6.  Click the **Run (▶)** button to execute the cell to create Cora agent
   
    ![](./media/image69.png)    

    ![](./media/image70.png) 

8.  The notebook cell successfully uploads paint product files from the
    specified folder, showing a confirmation message that 10 files were
    uploaded after execution.

    ![](./media/image71.png)

9.  The notebook cell reads and displays the uploaded paint product
    files, listing each file name along with its product title and price
    extracted from the file content.

    ![](./media/image72.png)

10.  The cell executes successfully, creating a vector store named
    **"Zava-Paint-Products"** using the uploaded files, and confirms
    that the vector store was created with 10 files.

    ![](./media/image73.png) 

11. Run the cell to update the agent by attaching the file search tool,
    enabling it to query and retrieve information from the created
    vector store of uploaded product files.

    ![](./media/image74.png) 

12. Run the cell to create a new conversation thread and display a
    confirmation message indicating that the thread has been
    successfully created.

    ![](./media/image75.png) 

13. Run the cell to create a user message in the conversation thread and
    display a confirmation message indicating that the message has been
    successfully sent to Cora.

    ![](./media/image76.png) 

14. Run the cell to execute the agent, allowing it to process the user
    message using the file search tool, and display a confirmation
    message indicating that the agent run has completed successfully.

    ![](./media/image77.png)

15. Run the cell to retrieve all messages from the conversation thread
    and display Cora’s response along with the user’s message in a
    formatted conversation view.

    ![](./media/image78.png)

    ![](./media/image79.png)

16. Run the cell to define a helper function that sends a message to
    Cora, processes it using the agent, and retrieves the assistant’s
    response from the conversation thread.

    ![](./media/image80.png)

    ![](./media/image81.png)

17. Run the cell to test Cora with Paint related questions.

    ![](./media/image82.png)

    ![](./media/image83.png)

    ![](./media/image84.png)

    ![](./media/image85.png)

    ![](./media/image86.png)

    ![](./media/image87.png)

    ![](./media/image88.png)

## Task 9: Cora-For-Zava: Building a Multi-Agent Retail Assistant System

**Cora** is a customer service chatbot for **Zava** - a fictitious
retailer of home improvement goods for DIY enthusiasts. As Zava retail
stores grow, Cora needs to handle more complex customer needs. This
notebook shows you how to evolve from a single agent to a multi-agent
system, with specialized agents for inventory management and customer
service. You'll learn to orchestrate multiple agents working together to
provide sophisticated and role-specific assistance.

1.  Navigate to the **labs/agents/** folder and open the
    **12-agent-framework-orchestration.ipynb** notebook to begin the
    environment setup lab.

    ![](./media/image89.png)

2.  Click **Select Kernel**, then choose the **Python 3.12.11**
    environment to run the Lab 02 notebook

    ![](./media/image90.png)

3.  Click the **Run (▶)** button to execute the cell and verify that all
    required Python packages are installed successfully.

    ![](./media/image91.png)

    ![](./media/image92.png)

    ![](./media/image93.png)

4.  Run the cell to verify your Azure login by creating Azure CLI
    credentials and confirming that a token is successfully retrieved.

    ![](./media/image94.png)

5.  Run the cell to connect to the Azure AI Project, retrieve the Azure
    AI Search connection, and confirm that the project client has been
    successfully created.

    ![](./media/image95.png)

6.  Run the cell to define the Product Inventory Agent instructions and
    display a confirmation message along with the instruction length.

    ![](./media/image96.png)

    ![](./media/image97.png)

7.  Run the cell to create the Product Inventory Agent with Azure AI
    Search capabilities and display a confirmation message indicating
    that the agent has been successfully created.

    ![](./media/image98.png)

    ![](./media/image99.png)

8.  Run the cell to test the Product Inventory Agent by sending a sample
    query, processing it with Azure AI Search, and displaying the
    agent’s response along with relevant citations.

    ![](./media/image100.png)

    ![](./media/image101.png)

9.  Run the cell to test the Customer Service Agent by sending the same
    query, processing it with Azure AI Search, and displaying the
    agent’s response along with relevant citations.

    ![](./media/image102.png)

    ![](./media/image103.png)

    ![](./media/image104.png)

    ![](./media/image105.png)

    ![](./media/image106.png)

    ![](./media/image107.png)

## Task 10: Cora-For-Zava: Generating Synthetic Test Datasets for Evaluation

**Cora** is a customer service chatbot for **Zava** - a fictitious
retailer of home improvement goods for DIY enthusiasts. To ensure Cora
provides accurate and helpful responses about hardware and home
improvement products, you need quality test data. This notebook helps
you generate synthetic query-response pairs based on your product
catalog, creating a robust evaluation dataset to measure Cora's
performance before deployment.

1.  Navigate to the **labs/models/** folder and open the
    **21-simulated-dataset.ipynb** notebook to begin the environment
    setup lab.

    ![](./media/image108.png)

2.  Click **Select Kernel**, then choose the **Python 3.12.11**
    environment to run the Lab 02 notebook

    ![](./media/image109.png)

3.  Click **Run All** to execute all the cells in the notebook and
    observe the outputs.

    ![](./media/image110.png)

    ![](./media/image111.png)

    ![](./media/image112.png)

    ![](./media/image113.png)

    ![](./media/image114.png)

    ![](./media/image115.png)

    ![](./media/image116.png)

    ![](./media/image117.png)

    ![](./media/image118.png)

    ![](./media/image119.png)

    ![](./media/image120.png)

    ![](./media/image121.png)

    ![](./media/image122.png)

## Task 11: Cora-For-Zava: Evaluating and Selecting the Best AI Model

**Cora** is a customer service chatbot for **Zava** - a fictitious
retailer of home improvement goods for DIY enthusiasts. To ensure Cora
provides the best customer experience, you need to select the right
foundation model. With multiple Azure OpenAI models available (GPT-4o,
GPT-4o-mini, GPT-4), you need to evaluate which model delivers the best
balance of quality, safety, and performance for your retail use case.

1.  Navigate to the **labs/models/** folder and open the
    **22-evaluate-models.ipynb** notebook to begin the environment setup
    lab.

    ![](./media/image123.png)

2.  Click **Select Kernel**, then choose the **Python 3.12.11**
    environment to run the Lab 02 notebook

    ![](./media/image124.png)

4.  Click **Run All** to execute all the cells in the notebook and
    observe the outputs.

    ![](./media/image110.png)

    ![](./media/image125.png)

    ![](./media/image126.png)

    ![](./media/image127.png)

    ![](./media/image128.png)

    ![](./media/image129.png)

    ![](./media/image130.png)

    ![](./media/image131.png)

    ![](./media/image132.png)

    ![](./media/image133.png)

    ![](./media/image134.png)

    ![](./media/image135.png)

    ![](./media/image136.png)

    ![](./media/image137.png)

## Task 12: Cora-For-Zava: Getting Started with Your First AI Evaluation Flow

**Cora** is a customer service chatbot for **Zava** - a fictitious
retailer of home improvement goods for DIY enthusiasts. Before deploying
Cora to help customers, you need to ensure it provides accurate, safe,
and helpful responses. Evaluation is the foundation of trust in AI
applications, making it a critical part of the Generative AI Ops
(GenAIOps) lifecycle. Without rigorous evaluation, Cora could produce
content that is fabricated, irrelevant, harmful, or vulnerable to
adversarial attacks.

1.  Navigate to the **labs/** **4-evaluation/** folder and open the
    42-**first-evaluation-run.ipynb** notebook to begin the environment
    setup lab.

    ![](./media/image138.png)

2.  Click **Select Kernel**, then choose the **Python 3.12.11**
    environment to run the Lab 02 notebook

    ![](./media/image139.png)

3.  Click **Run All** to execute all the cells in the notebook and
    observe the outputs.

    ![](./media/image110.png)

    ![](./media/image140.png)

    ![](./media/image141.png)

    ![](./media/image142.png)

    ![](./media/image143.png)

    ![](./media/image144.png)

    ![](./media/image145.png)

    ![](./media/image146.png)

    ![](./media/image147.png)

    ![](./media/image148.png)

    ![](./media/image149.png)

    ![](./media/image150.png)

    ![](./media/image151.png)

    ![](./media/image152.png)

    ![](./media/image153.png)

## Task 13: Cora-For-Zava: Exploring AI Response Quality Evaluators

**Cora** is a customer service chatbot for **Zava** - a fictitious
retailer of home improvement goods for DIY enthusiasts. Cora must
provide accurate, relevant, and coherent responses about hardware and
home improvement products to Zava customers. This notebook helps you
assess response quality using specialized evaluators for groundedness,
relevance, coherence, fluency, and similarity—ensuring Cora meets the
high standards expected in a production retail environment.

1.  Navigate to the **labs/** **4-evaluation/** folder and open the
    **42-evaluate-quality.ipynb** notebook to begin the environment
    setup lab.

    ![](./media/image154.png)

2.  Click **Select Kernel**, then choose the **Python 3.12.11**
    environment to run the Lab 02 notebook

    ![](./media/image155.png)

3.  Click **Run All** to execute all the cells in the notebook and
    observe the outputs.

    ![](./media/image110.png)

    ![](./media/image156.png)

    ![](./media/image157.png)

    ![](./media/image158.png)

    ![](./media/image159.png)

    ![](./media/image160.png)

    ![](./media/image161.png)

    ![](./media/image162.png)

    ![](./media/image163.png)

    ![](./media/image164.png)

    ![](./media/image165.png)

    ![](./media/image166.png)

    ![](./media/image167.png)

    ![](./media/image168.png)

    ![](./media/image169.png)

    ![](./media/image170.png)

    ![](./media/image171.png)

    ![](./media/image172.png)

    ![](./media/image173.png)

    ![](./media/image174.png)

    ![](./media/image175.png)

    ![](./media/image176.png)

    ![](./media/image177.png)

## Task 14: Cora-For-Zava: Exploring AI Safety Evaluators for Secure Responses

**Cora** is a customer service chatbot for **Zava** - a fictitious
retailer of home improvement goods for DIY enthusiasts. Before deploying
Cora to serve Zava customers, you must ensure it generates safe,
appropriate content and is protected against adversarial attacks. This
notebook guides you through Azure AI Foundry's safety evaluators,
helping you identify and mitigate risks like harmful content, jailbreak
attempts, and protected material violations to maintain a secure and
trustworthy customer experience.

1.  Navigate to the **labs/** **4-evaluation/** folder and open the
    **43-evaluate-safety.ipynb** notebook to begin the environment setup
    lab.

2.  Click **Select Kernel**, then choose the **Python 3.12.11**
    environment to run the Lab 02 notebook

    ![](./media/image178.png)

4.  Click **Run All** to execute all the cells in the notebook and
    observe the outputs.

    ![](./media/image110.png)

    ![](./media/image179.png)

    ![](./media/image180.png)

    ![](./media/image181.png)

    ![](./media/image182.png)

    ![](./media/image183.png)

**Summary**

In this lab, you implemented a complete **end-to-end AI solution** for a
retail assistant using Azure AI Foundry. Starting from environment setup
and deployment, you built Cora, enhanced it with search capabilities,
and evolved it into a multi-agent system.

You also explored critical aspects of production AI systems, including:

- Data indexing and retrieval

- Agent orchestration

- Model evaluation and selection

- Safety and quality validation

By the end of this exercise, you gained practical experience in
designing, deploying, and managing **scalable, intelligent AI
applications** that deliver real-world business value.
