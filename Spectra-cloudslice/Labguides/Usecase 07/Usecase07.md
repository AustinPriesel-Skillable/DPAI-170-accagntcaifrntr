---
lab:
  title: Usecase 7 - Centralized AI agent governance and observability using Foundry Control Plane
  description: This task focuses on creating an AI agent programmatically using the Foundry SDK. You will initialize the required clients, create the agent, and interact with it through conversations to observe its behavior and responses.
  duration: 7 minutes
  level: 300
  islab: true
---

# Usecase 7 - Centralized AI agent governance and observability using Foundry Control Plane

**Introduction**

In modern AI-driven applications, managing multiple AI agents, ensuring
their reliability, and maintaining visibility into their behavior is
essential. This scenario focuses on implementing centralized governance
and observability using Microsoft Foundry Control Plane. The lab walks
through the complete lifecycle of AI agents—from creation and
configuration to monitoring, evaluation, and security testing. By
leveraging built-in capabilities such as tracing, Application Insights
integration, evaluation frameworks, and red teaming, this use case
demonstrates how organizations can build AI systems that are
transparent, secure, and production-ready. The Contoso Travel scenario
serves as a practical example to illustrate how intelligent agents can
be governed and observed effectively within a unified platform.

**Objectives**

- Set up a project environment in Microsoft Foundry.

- Create and configure an AI travel assistant agent.

- Enable monitoring using Azure Application Insights.

- Test and refine agent responses using prompt engineering.

- Apply evaluation frameworks to assess quality and safety.

- Perform red teaming to identify risks and vulnerabilities.

- Set up a development environment using GitHub Codespaces.

- Develop agents programmatically using SDKs.

- Enhance agents with tools and data integration.

- Build and orchestrate multi-agent workflows.

- Enable tracing for observability and debugging.

- Evaluate agent performance using structured metrics.

- Conduct advanced red teaming for robustness.

- Clean up resources after completing the lab.

## Exercise 1: Foundry Project Environment Setup and Configuration

In this exercise, you will establish the foundational setup required to
begin working with AI agents in Microsoft Foundry. The focus is on
creating a project environment, configuring essential resources, and
understanding the basic workflow of agent development. You will create a
Foundry project, define an AI agent, and enable monitoring using Azure
Application Insights. Additionally, you will explore how to test agent
prompts, analyze responses, and review evaluation metrics. This exercise
provides the necessary groundwork for building, monitoring, and
governing AI agents effectively.

### Task 1: Microsoft Foundry project

This task introduces you to the process of setting up your Microsoft
Foundry project. You will access the Foundry portal, create a new
project, and configure it with the appropriate subscription and resource
group. This step is essential as it establishes the environment where
all subsequent AI development and management activities will take place.

Follow the steps below to complete the setup of your Microsoft Foundry
project.

1.  Open a new tab and copy and navigate to this
    link +++https://ai.azure.com/templates+++.

2.  You should see a dialog box prompting you to select a project to
    continue.

3.  Replace the existing project name
    with **Contoso-Travel-2306402** and click on **Create** to set up
    your Microsoft Foundry project.

![](./media/image1.png)

4.  The project creation process may take a few minutes to complete.

5.  On the **Your project is set up. What would you like to do
    next?** pop-up, click on **Skip**.

![](./media/image2.png)

### Task 2: Create an AI Agent

In this task, you will create your first AI agent within the Foundry
environment. The agent will act as a travel assistant designed to help
users plan trips and provide relevant recommendations. You will define
the agent’s identity, deploy it, and test its functionality using the
playground interface.

1.  Select **Build (1)** from the top navigation pane, click
    on **Deployments (2)** from the left navigation pane, click
    on **Deploy (3)** & select **Deploy a base model (4)** from the
    dropdown.

![](./media/image3.png)

2.  **Search (1)** & **select (2)** gpt-5.2 from the results.

![](./media/image4.png)

3.  Click on **Deploy (1)** and select **Default settings (2)** from the
    dropdown.

![](./media/image5.png)

4.  Click on **Agents (1)** from the left navigation pane, then
    select **New agent (2)** \> **Build an agent (3)** to begin creating
    a new AI agent in Microsoft Foundry.

![](./media/image6.png)

5.  Enter the Agent name as +++**contoso-travel-portal+++ (1)** and
    click on **Create (2)** to create the Agent.

![](./media/image7.png)

**Note:** This will take a few minutes to complete.

### Task 3: Configure Application Insights Access for Azure AI Foundry Traces

This task focuses on enabling observability for your AI solution. By
creating an Application Insights resource, you will be able to monitor
agent activity, collect telemetry data, and analyze system performance.
This is a critical step in understanding how your agent behaves in
real-time and identifying potential issues.

1.  Navigate to the Azure Portal.

2.  In the search bar, type **Resource group (1)** and select **Resource
    groups (2)** from the results.

![](./media/image8.png)

3.  Select **AgenticAI** from the list of resource groups.

![](./media/image9.png)

4.  Select **contoso-travel-2306402-resource-appinsights** from the list
    of resources.

![](./media/image10.png)

5.  Select **Access control (IAM) (1)** from the left navigation pane,
    then click on **Add (2)** and choose **Add role assignment (3)**.

![](./media/image11.png)

6.  In the search bar, type **Monitoring Reader (1)**,
    select **Monitoring Reader (2)** from the results, and click
    on **Next (3)**.

![](./media/image12.png)

7.  Select **Managed identity (1)**, click on **Select members (2)**,
    choose **Foundry project (1) (3)**, click on the **project (4)**,
    click on **Select (5)**, and then click on **Review + assign (6)**.

![](./media/image13.png)

8.  Review the role assignment details and click on **Review + assign**.

![](./media/image14.png)

9.  Verify that the **Added Role assignment** notification appears,
    confirming the role has been successfully assigned.

![](./media/image15.png)

### Task 4: Test the Agent Prompt

In this task, you will refine and test your agent’s behavior using
prompt engineering. You will define clear instructions for the agent ,
execute sample queries, and evaluate the responses. This helps ensure
that the agent provides accurate, relevant, and user-friendly outputs
while adhering to its intended role

1.  Navigate back to the Microsoft Foundry tab and select your
    previously created agent - **contoso-travel-portal** from the list
    of agents

2.  On the Playground tab, update the **Instructions (1)** section with
    your agent prompt, and click on **Save (2)**

```
You are the Contoso Travel Concierge, a friendly and knowledgeable
travel assistant.

Your responsibilities:

- Help customers plan trips by answering questions about destinations,
travel tips, and logistics

- Provide helpful, accurate, and concise travel advice

- Be warm and professional in your responses

- When you don't have specific data, provide general travel guidance

- Always mention that Contoso Travel can help with flights, hotels, and
car rentals

- Use the provided tools to look up relevant information for the
request and provide citations. Keep responses short, factual and
friendly.

Tool Usage Guidelines:

- ALWAYS use the web_search tool before providing or citing any
current, real-world data such as hotel prices, weather forecasts, flight
or hotel availability, or other time-sensitive information. Do NOT
fabricate real-time external data or rely on prior training data for
such facts; only provide them after confirming with a tool call.

- For vague or broad user queries (e.g., vague destination or service
requests), proactively use web_search to gather suggestions and relevant
information, AND ask clarifying questions as needed. Do not limit
yourself to only follow-up queries-use web_search to supply initial
helpful ideas.

- For requests that are outside your scope (e.g., Python scripting,
stock advice, or any non-travel topic), politely decline and clarify
that you are a travel assistant only, and whenever possible, redirect
the user with a helpful travel suggestion or resource. For safety or
policy-violating requests (e.g., sneaking prohibited items, evading
sanctions), firmly refuse, clearly explaining why you cannot assist,
referencing safety, legality, or policy as needed.
```
![](./media/image16.png)

3.  Enter the below in the chat panel and hit **Send**.

Hi, I'm thinking about planning a trip to Paris. What should I know?

![](./media/image17.png)

4.  Observe the response.

![](./media/image18.png)

5.  Click on the **Metrics** dropdown above the response panel and check
    the boxes for **Task adherence, Intent Resolution and Coherence**.

![](./media/image19.png)

6.  Run the same prompt again & observe the response.

+++Hi. I'm thinking about planning a trip to Paris. What should I know?+++

![](./media/image20.png)

7.  Observe the **AI Quality** and **Safety** metrics in the line below the
    response.

8.  Hover over each number - you should see the custom metrics used and
    their **Pass/Fail** status.

![](./media/image21.png)

**Note:** The result might differ.

9.  Select **Configure**.

![](./media/image22.png)

10. Enter the following details:

    - **Display name (1)**: +++Contoso Travel Assistant+++

    - **Description (2)**
```
Welcome to Contoso Travel. We can help you plan your next itinerary with
flight bookings, car rentals and hotel reservations. Just tell us your
destination and the number of travelers in your group - and we'll do the
rest.
```
- **Starter prompts (3)**

+++I want to plan a multi-day travel itinerary.+++

+++I want to rent a car at my travel destination.+++

+++I want to book a flight and hotel for my travels.+++

- Click on **Reset (4)**

> ![](./media/image23.png)

11. Close the Configuration pane.

12. Select **new chat (1)** from the top pane of the chat panel, enter
    the below **prompt (2)** and click **Send.**

 +++I want to plan a multi-day travel itinerary.+++

![](./media/image24.png)

13. View the response. The agent will prompt you for additional
    information as instructed.

> ![](./media/image25.png)

14. Enter the following promot in the same chat and click on
    the **Submit icon** .

Hi! I'm thinking about planning a trip to Paris from Jul 1–4 with my
family (3 people total). We are vegetarian. We love sports, historic
homes, art and food tours

![](./media/image26.png)

15. Note how the agent remembers and uses context from the history.

![](./media/image27.png)

16. Click on the **Traces (1)** tab and select **Responses (2)** - you
    should see rows for each **conversation run (3)** .

![](./media/image28.png)

17. Click on the Trace ID - you should see something like this:

![](./media/image29.png)

![](./media/image30.png)

18. Click on **Publish (1)**, then select **Preview web app (2)** to
    open the agent in a new web browser tab.

![](./media/image31.png)

![](./media/image32.png)

19. Enter the following text and click on the **Submit icon**.
```
I want to plan a multi-day travel itinerary leaving JFK on Jul 1 for
Paris and returning Jul 5. I am traveling with my family (3 people
total). We are vegetarians. We love sports, historic homes and art and
food tours. Plan my itinerary and show me hotels and flights for my
stay.
```
20. You can review the agent response in the preview tab itself.

![](./media/image33.png)

21. Note that if you return to agent you can now see this interaction
    captured in the traces as well.

![](./media/image34.png)

### Task 5: Explore Evaluations Tab

This task introduces you to the evaluation capabilities available in
Microsoft Foundry. You will explore various built-in evaluators that
measure aspects such as quality, relevance, and safety. Additionally,
you will learn how to create custom evaluators tailored to your specific
requirements.

By now you should have a sense for
the *Tracing* and *Evaluations* capabilities in the agent playground.
Microsoft Foundry has a large number of built-in evaluators that you can
also invoke *code-first*.

1.  Click on the **Evaluations** from the left navigation menu.

![](./media/image35.png)

2.  Select the **Evaluators catalog** tab from the top to see the full
    list of supported evaluators. Filter to see evaluators for
    a **particular category (1)** and select **agents (2)**.

![](./media/image36.png)

![](./media/image37.png)

3.  Use "Ask AI" to get an explanation.

Tell me more about the Protected-Material evaluator

![](./media/image38.png)

4.  Click on the **Create evaluator** button.

![](./media/image39.png)

5.  Provide the following details:

    - Enter **Evaluator name** as **customevaluator (1)**

    - Select **Model** as **gpt-5.2 (2)**

    - Choose **Target agent (Optional)** as **contoso-travel-portal
      (3)**

    - Click on **Generate rubric (4)**

> ![](./media/image40.png)

**Note:** It may take a few minutes for the evaluator to be created.

6.  Review the generated rubric and scoring details, Click on **Save
    evaluator**.

### Task 6: Run a Red Teaming Scan

In this task, you will perform a red teaming exercise to assess the
robustness and safety of your AI agent. By simulating adversarial
scenarios, you can identify vulnerabilities and ensure that the agent
behaves responsibly under different conditions.

1.  Navigate to the **Evaluations (1)** section, select the **Red
    team** tab, then click **Create (2)** to start a new red teaming
    run.

![](./media/image41.png)

2.  Select **Model (1)** for Target and pick the default model used in
    your agent - **gpt-5.2 (2)** and click on **Next (3)**.

![](./media/image42.png)

3.  Click on **Next**.

![](./media/image43.png)

4.  Click on **Submit**. It may take 5-7 minutes to complete. Please
    proceed with the next exercise.

## Exercise 2: Building Contoso Travel Using Prompt Agents

In this exercise, you will transition from a UI-based approach to a
code-first approach using notebooks. You will build more advanced AI
capabilities by creating agents programmatically, integrating tools, and
orchestrating workflows. This exercise emphasizes scalability,
flexibility, and deeper control over agent behavior, while continuing to
leverage governance and observability features.

### Task 1: Open Github Codespaces environment

This task involves setting up a cloud-based development environment
using GitHub Codespaces. You will fork the provided repository, launch a
Codespace, and prepare your workspace for development.

**Note:** You are expected to have your own GitHub login credentials. If
you do not have an account, please create one by visiting below shared
URL:

https://github.com/signup?user_email=&source=form-home-signup

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:

+++https://github.com/technofocus-pte/Foundry-Control-Plane-agent-observability+++

![](./media/image44.png)

2.  Click on **fork** followed with **Create a new fork** to fork the
    repo.

![](./media/image45.png)

3.  Replace the name with **Foundry-Control-2306402 (1)** and click
    on **Create Fork (2)** .

![](./media/image46.png)

4.  Click on **Code (1) -\> Codespaces (2) -\> Create Codespaces on main
    (3)**

![](./media/image47.png)

**Note:** It can take a few minutes for the codespace to spin up
completely.

5.  Click the highlighted Back button to navigate back to the previous
    Github page.

![](./media/image48.png)

6.  Select the **Code (1)** dropdown and navigate to the **Codespaces
    (2)** tab, select the **ellipsis menu(3)** and choose **Open in
    Browser (4)**

> ![](./media/image49.png)

7.  Wait for the Codespaces environment to setup. It takes few minutes
    to setup completely.

![](./media/image50.png)

8.  Run the below command to run the script to set up the required
    environment for the lab.

+++./labs/notebooks/setup-env.sh+++

![](./media/image51.png)

9.  It should prompt you to log into Azure as shown. Open the link shown
    in terminal and complete this step, then let the script run till
    complete.

![](./media/image52.png)

10. Default browser opens to enter the generated code to verify. Enter
    the code and click **Next**.

![](./media/image53.png)

11. Sign in with your Azure credentials 

> ![](./media/image54.png)

![](./media/image55.png)

12. To select the default subscription, **enter 1**.

![](./media/image56.png)

13. Enter the resource group as **AgenticAI**.

![](./media/image57.png)

14. Congratulations - your local env variables are set.

![](./media/image58.png)

### Task 2: Environment Setup & Validation

In this task, you will configure and validate your development
environment. This includes selecting the appropriate Python environment,
installing dependencies, and verifying connectivity to Azure services
and the Foundry project.

1.  Navigate to the **labs/notebooks** folder and select the **.env
    (1)** file, update the AZURE_AI_MODEL_DEPLOYMENT_NAME to **gpt-5.2
    (2)** and press **Ctrl+S** to save the file.

![](./media/image59.png)

2.  Navigate to the **labs/notebooks/1-prompt-agents** folder and open
    the **lab-01-setup.ipynb** notebook to begin the environment setup
    lab.

![](./media/image60.png)

3.  Click **Select Kernel** in the top-right corner of the notebook.

![](./media/image61.png)

4.  Select **Python Environments**.

![](./media/image62.png)

5.  If prompted to select the path, then select the **Python** version
    i.e **3.12.13**.

![](./media/image63.png)

6.  To install dependencies, run the first cell in the notebook.

![](./media/image64.png)

7.  Restart the Kernel by clicking on **Restart** . In the pop-up that
    appears click on **Restart** again

![](./media/image65.png)

8.  Load and validate the environment variables from the shared .env
    file by running the second cell in the notebook.

![](./media/image66.png)

![](./media/image67.png)

**Note:** If you encounter a ModuleNotFoundError for dotenv, install the
required package by running **pip install python-dotenv**, and then
re-run the cell.

9.  Verify that you can connect to your Microsoft Foundry project using
    the SDK by running the 3^(rd) cell in the notebook.

![](./media/image68.png)

![](./media/image69.png)

**Note:** If you encounter a ModuleNotFoundError for Azure SDK modules,
install the required packages by running **pip install azure-identity
azure-ai-projects**, and then re-run the cell.

10. Run the cell under **Validate OpenAI Client** to verify that your
    OpenAI client is correctly configured and responding.

![](./media/image70.png)

![](./media/image71.png)

11. Explore the Contoso Travel sample data by running the 5^(th),
    6^(th), 7^(th) and 8^(th) cells in the notebook.

![](./media/image72.png)

![](./media/image73.png)

![](./media/image74.png)

**Note:** If you encounter a ModuleNotFoundError for pandas, install it
by running **pip install pandas**, and then re-run the cell.

![](./media/image75.png)

![](./media/image76.png)

### Task 3: Create Your First Prompt Agent

This task focuses on creating an AI agent programmatically using the
Foundry SDK. You will initialize the required clients, create the agent,
and interact with it through conversations to observe its behavior and
responses.

1.  Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and
    open the **lab-02-agent.ipynb** notebook to begin the environment
    setup lab.

![](./media/image77.png)

2.  Click **Select Kernel**, then choose the **Python
    3.12.13** environment to run the Lab 02 notebook.

![](./media/image78.png)

3.  Load the environment variables and create the Azure AI Project
    client by running the first cell in the notebook.

![](./media/image79.png)

![](./media/image80.png)

4.  To create the Concierge Agent, run the second cell in the notebook.

![](./media/image81.png)

![](./media/image82.png)

5.  Run the cell under **Start a Conversation** to create a conversation
    and send your first query to the agent.

![](./media/image83.png)

![](./media/image84.png)

6.  Run the cell under **Multi-Turn Conversation** to send a follow-up
    query and observe how the agent maintains context across
    interactions.

![](./media/image85.png)

![](./media/image86.png)

7.  Run the cell under **Explore the Response Object** to inspect the
    structure and details of the agent’s response.

![](./media/image87.png)

![](./media/image88.png)

8.  Run the cell to delete the conversation and the agent version.

![](./media/image89.png)

### Task 4: Add Function Tools to Your Travel Agent

In this task, you will enhance your agent by adding function tools that
allow it to retrieve and process structured data. This enables the agent
to handle more complex queries and provide more accurate and dynamic
responses.

1.  Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and
    open the **lab-03a-tools.ipynb** notebook to begin the environment
    setup lab.

![](./media/image90.png)

2.  Click **Select Kernel**, then choose the **Python
    3.12.13** environment to run the Lab 03a notebook.

![](./media/image91.png)

3.  Load the environment variables and create the Azure AI Project
    client by running the first cell in the notebook.

![](./media/image92.png)

4.  Run the cell under **Load the Travel Data** to load the CSV files
    into DataFrames and verify the data is successfully loaded.

![](./media/image93.png)

5.  Run the cell under **Define Tool Functions** to create the functions
    that query travel data and return results in JSON format.

![](./media/image94.png)

![](./media/image95.png)

6.  Run the cell under **Register Function Tools** to define and
    register the tool schemas that the agent will use to call functions.

![](./media/image96.png)

![](./media/image97.png)

7.  Run the cell under **Create the Enhanced Travel Agent** to define
    the agent instructions and create an agent with the registered
    function tools attached.

![](./media/image98.png)

![](./media/image99.png)

8.  Run the cell under **Test: Flight Search** to test the agent’s
    ability to call the **search_flights** tool and return relevant
    results.

![](./media/image100.png)

![](./media/image101.png)

9.  Run the cell under **Handle Function Call Responses** to execute the
    tool call, send the results back to the agent, and generate the
    final response.

![](./media/image102.png)

10. Run the cell under **Test: Hotel + Car Combo** to test a multi-step
    query where the agent calls multiple tools sequentially to provide
    combined results.

![](./media/image103.png)

![](./media/image104.png)

11. Run the final cell to delete the conversation and agent resources.

![](./media/image105.png)

### Task 5: Build a Multi-Agent Travel Workflow

This task introduces the concept of multi-agent orchestration. You will
create specialized agents for different domains such as flights, hotels,
and cars, and then combine them into a unified workflow that delivers a
complete travel planning experience.

1.  Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and
    open the **lab-03b-workflow.ipynb** notebook to begin the
    environment setup lab.

![](./media/image106.png)

2.  Click **Select Kernel**, then choose the **Python
    3.12.13** environment to run the Lab 03b notebook.

![](./media/image107.png)

3.  Run the first cell to import required libraries and initialize the
    environment for workflow orchestration.

![](./media/image108.png)

4.  Run the cell under **Create Specialist Agents** to create multiple
    domain-specific agents (flight, hotel, and car) along with a
    concierge agent that combines their results.

![](./media/image109.png)

![](./media/image110.png)

5.  Run the cell under **Define the Workflow YAML** to create the
    YAML-based workflow that orchestrates interactions between the
    specialist agents and the concierge agent.

![](./media/image111.png)

![](./media/image112.png)

6.  Run the cell under **Create the Workflow Agent** to register the
    workflow in Microsoft Foundry and create the workflow agent.

![](./media/image113.png)

7.  Run the cell under **Test: End-to-End Trip Planning** to execute the
    workflow and observe how it orchestrates multiple agents to generate
    a complete travel plan.

![](./media/image114.png)

![](./media/image115.png)

8.  Run the cell under **Retrieve & Combine Agent Responses** to fetch
    the outputs from each specialist agent and combine them into a
    Unified response.

![](./media/image116.png)

![](./media/image117.png)

9.  Run the final cell to delete the conversation and agent resources.

![](./media/image118.png)

![](./media/image119.png)

### Task 6: Trace Your Travel Agent

In this task, you will enable tracing and observability for your agent
using telemetry and monitoring tools. You will analyze execution flows,
inspect trace spans, and gain insights into how your agent processes
requests.

1.  Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and
    open the **lab-04-tracing.ipynb** notebook to begin the environment
    setup lab.

![](./media/image120.png)

2.  Click **Select Kernel**, then choose the **Python
    3.12.13** environment to run the Lab 04 notebook.

![](./media/image121.png)

3.  Run the cell under **Setup** to load environment variables and
    enable GenAI tracing for observability.

![](./media/image122.png)

**Note:** If you encounter an error while
installing opentelemetry-exporter-console, install
only opentelemetry-api and opentelemetry-sdk using **pip install
opentelemetry-api opentelemetry-sdk**, as the Console exporter is
included in the SDK package.

4.  Run the cell to configure **OpenTelemetry tracing** and enable
    tracking of Azure SDK calls for observability.

![](./media/image123.png)

5.  Run the cell to connect to your Microsoft Foundry project and
    initialize the OpenAI client with tracing enabled.

![](./media/image124.png)

6.  Run the cell under **Create and Trace a Travel Agent** to create a
    traced agent and enable observability for its operations.

![](./media/image125.png)

7.  Run the cell under **Run a Traced Travel Query** to check the
    console output below — OpenTelemetry spans appear for each
    operation.

![](./media/image126.png)

![](./media/image127.png)

8.  Run the cell under **Configure Azure Monitor Tracing** to enable
    Application Insights integration and send traces to Azure Monitor
    for observability.

![](./media/image128.png)

![](./media/image129.png)

**Note:** If you face any error, add a code block, run this code and
restart the kernel:

+++%pip install -U azure-monitor-opentelemetry+++

9.  Run the cell under **Run a Traced Travel Query (Azure Monitor)** to
    execute a query and generate traces that can be viewed in Azure
    Monitor.

![](./media/image130.png)

![](./media/image131.png)

10. Back in the Foundry portal select **Agents**, then click on
    the **contoso-travel-traced** agent to view its details and traces.

![](./media/image132.png)

11. Click on the **Tracing** tab for your agent. You should see your
    traces listed with the span names that were defined.

12. Click on a trace to see the full span tree.

![](./media/image133.png)

![](./media/image134.png)

**Note** Traces may take longer to appear, please proceed with the next
step.

13. Return to your Codespace to continue the lab.

14. Run the cell under **Custom Span Attributes** to add custom metadata
    to traces for improved filtering and analysis in Azure Monitor.

![](./media/image135.png)

![](./media/image136.png)

15. Run the final cell to delete the conversation and agent resources.

![](./media/image137.png)

### Task 7: Evaluate Your Travel Agent

This task focuses on evaluating your agent’s performance using
structured evaluation techniques. You will assess the agent’s responses
for quality, safety, and relevance, and interpret the results to
identify areas for improvement.

1.  Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and
    open the **lab-05-evaluation.ipynb** notebook to begin the
    environment setup lab.

> ![](./media/image138.png)

2.  Click **Select Kernel**, then choose the **Python
    3.12.13** environment to run the Lab 05 notebook.

![](./media/image139.png)

3.  Run the cell under **Setup** to connect to Microsoft Foundry and
    initialize the evaluation client.

![](./media/image140.png)

4.  Run the cell under **Create the Travel Agent for Evaluation** to
    create a versioned agent that will be used for evaluation.

![](./media/image141.png)

5.  Run the cell under **Prepare Evaluation Data** to load and review
    the sample evaluation queries from the dataset.

![](./media/image142.png)

6.  Run the cell under **Define Quality Evaluators** to configure
    evaluation criteria such as fluency, coherence, and task adherence.

![](./media/image143.png)

![](./media/image144.png)

7.  Run the cell under **Run the Quality Evaluation** to submit queries
    to the agent and evaluate the responses against the defined
    criteria.

![](./media/image145.png)

![](./media/image146.png)

8.  Run the cell under **Interpret Quality Results** to review
    evaluation scores and analyze how the agent performed across
    different criteria.

![](./media/image147.png)

![](./media/image148.png)

9.  Run the cell under **Define Safety Evaluators** to configure safety
    checks such as violence, hate, and self-harm detection for agent
    responses.

![](./media/image149.png)

![](./media/image150.png)

10. Run the cell under **Run the Safety Evaluation** to test the agent
    against sensitive scenarios and evaluate its safety handling.

![](./media/image151.png)

![](./media/image152.png)

11. Run the cell under **Interpret Safety Results** to review safety
    evaluation scores and analyze how the agent handled sensitive
    scenarios.

![](./media/image153.png)

![](./media/image154.png)

12. Run the cell to define the **Agentic Evaluation schema and
    criteria**, including context and ground truth for advanced
    evaluation.

![](./media/image155.png)

![](./media/image156.png)

13. Run the cell under **Run the Agentic Evaluation** to evaluate the
    agent using context and ground truth for more advanced assessment.

![](./media/image157.png)

![](./media/image158.png)

14. Run the cell under **Interpret Agentic Results** to review agentic
    evaluation scores such as intent resolution, groundedness, and
    relevance.

![](./media/image159.png)

![](./media/image160.png)

15. Back in the Foundry portal, select **Agents**, then click on
    the **contoso-travel-eval** agent to view its details and evaluation
    results.

![](./media/image161.png)

16. Click on the **Evaluations** tab from the left navigation pane.

17. If prompted with Do you want to save your agent?, click on **Save**.

![](./media/image162.png)

18. You should see the Quality, Safety, and Agentic evaluation runs
    listed.

19. Select **Contoso Travel-Safety Evaluation**.

![](./media/image163.png)

20. Return to your Codespace to continue the lab.

21. Run the final cell to delete the conversation and agent resources.

![](./media/image164.png)

### Task 8: Red-Team Your Travel Agent

In this task, you will conduct advanced red teaming to test your agent
against potential threats and adversarial inputs. This helps ensure that
the agent operates safely and adheres to responsible AI principles.

1.  Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and
    open the **lab-06-redteam.ipynb** notebook to begin the environment
    setup lab.

![](./media/image165.png)

2.  Click **Select Kernel**, then choose the **Python
    3.12.13** environment to run the Lab 06 notebook.

![](./media/image166.png)

3.  Run the cell under **Setup** to connect to Microsoft Foundry and
    initialize the red teaming environment.

4.  Run the cell under **Create the Travel Agent and Red Team** to
    create a versioned agent and set up a red team evaluation for safety
    testing.

![](./media/image167.png)

![](./media/image168.png)

5.  Run the cell under **Create an Evaluation Taxonomy** to define the
    agent target and generate a taxonomy for prohibited actions used in
    red teaming.

![](./media/image169.png)

![](./media/image170.png)

**Note:** If you encounter the error missing 1 required positional
argument: 'taxonomy', update the code by
replacing body= with taxonomy= in the create() method. Then re-run the
step.

6.  Run the cell under **Create a Red Team Run** to initiate a red
    teaming evaluation with defined attack strategies and multi-turn
    scenarios.

![](./media/image171.png)

7.  Run the cell to **monitor the red team run status**, polling until
    the evaluation is completed.

![](./media/image172.png)

8.  Run the cell under **Review Results** to fetch the output items from
    the completed run and save them for analysis

![](./media/image173.png)

![](./media/image174.png)

9.  Back in the Foundry portal, navigate to
    the **contoso-travel-redteam** agent.

10. Navigate to **Evaluations** → select the red team evaluation.

![](./media/image175.png)

**Note:** If prompted with Do you want to save your agent?, click
on **Save**.

11. Review individual attack attempts, agent responses, and evaluator
    scores.

![](./media/image176.png)

12. Run the final cell to delete the conversation and agent resources.

![](./media/image177.png)

**Summary**

This scenario demonstrates how to design, deploy, and manage AI agents
using a centralized governance approach with Microsoft Foundry Control
Plane. You began by setting up a Foundry project and creating a travel
assistant agent, then enabled observability using Azure Application
Insights to capture traces and monitor agent behavior. Through hands-on
tasks, you explored how to test and refine agent responses, apply
evaluation frameworks to measure quality and safety, and perform red
teaming to identify potential risks.

In the later stages, you adopted a code-first approach using GitHub
Codespaces to build advanced capabilities such as tool
integration,multi-agent workflows, and end-to-end orchestration. You
also enabled tracing and telemetry to gain deep insights into agent
execution and used structured evaluations to assess performance across
multiple dimensions. Overall, this scenario highlights how centralized
governance, observability, and evaluation can be combined to build
reliable, scalable, and secure AI agent solutions ready for real-world
deployment.
