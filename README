# AWS Bedrock Agentic AI Coffee Shop

A production-oriented Generative AI application built on AWS that demonstrates business-value modeling, data strategy, Retrieval-Augmented Generation (RAG), specialized AI agents, and multi-agent collaboration.

The project simulates a coffee-shop platform where customers can ask questions, browse the menu, place orders, find stores, learn about promotions, and receive payment-related assistance through a coordinated AI system.

## Project Overview

This project was developed as part of an AWS Generative AI applications lab. It demonstrates how to move from AI use-case ideation to a working multi-agent application.

The solution includes:

- Interactive business-value and ROI modeling.
- Domain-specific operational and policy data sources.
- Amazon Bedrock Knowledge Bases for RAG.
- Amazon OpenSearch Serverless vector storage.
- Specialized AI agents for different business domains.
- A Barista Supervisor agent that coordinates the specialized agents.
- Natural-language testing of multi-step customer scenarios.
- Monitoring, security, responsible AI, and deployment components.

## Architecture

The application follows a multi-agent collaboration architecture:

```text
                         Customer
                            |
                            v
                 Barista Supervisor Agent
                            |
       ------------------------------------------------
       |              |             |       |          |
       v              v             v       v          v
 Orders Agent   Menu Agent   Payments   Stores   Promotions
                                 Agent     Agent      Agent
       |              |             |       |          |
       v              v             v       v          v
   DynamoDB         S3        Knowledge  Aurora     Knowledge
   Orders Data   Menu Data     Bases    MySQL      Base
```

The supervisor agent receives a customer request, determines which domain is relevant, and delegates the task to one or more specialized agents.

## Specialized Agents

### Orders Agent

Handles order-related operations, including:

- Retrieving recent orders.
- Checking order status.
- Validating requested items.
- Placing new orders.
- Applying order-related policies.

Primary integrations:

- Amazon DynamoDB.
- Amazon Bedrock Knowledge Base.

### Menu Agent

Handles menu-related questions, including:

- Listing food and drink items.
- Checking item availability.
- Checking seasonal items.
- Providing menu and nutritional information.

Primary integrations:

- Amazon S3.
- Amazon Bedrock Knowledge Base.

### Stores Agent

Handles store-related requests, including:

- Finding store locations.
- Searching stores by name.
- Checking operating hours.
- Checking store amenities.
- Answering store policy questions.

Primary integrations:

- Amazon Aurora MySQL.
- Amazon Bedrock Knowledge Base.

### Payments Agent

Handles payment-related requests, including:

- Calculating order totals.
- Explaining supported payment methods.
- Answering payment policy questions.
- Supporting payment and refund-related inquiries.

Primary integrations:

- Amazon Bedrock Knowledge Base.
- Calculation tools.

### Promotions Agent

Handles promotion-related questions, including:

- Listing available promotions.
- Explaining promotional terms.
- Troubleshooting promotion codes.
- Explaining offer redemption requirements.

Primary integrations:

- Amazon S3.
- Amazon Bedrock Knowledge Base.

### Barista Supervisor Agent

The supervisor agent coordinates the complete application by:

- Interpreting customer requests.
- Routing tasks to the appropriate specialized agent.
- Coordinating multiple agents for complex requests.
- Maintaining session context.
- Combining responses into a customer-friendly answer.

## Repository Structure

```text
.
├── 1_business_modeling/
│   └── business_value.py
│
├── 2_data_strategy/
│   ├── menu/
│   │   ├── configure_menu_data_sources.sh
│   │   ├── menu_items_kb_faqs.txt
│   │   └── menu_records.json
│   │
│   ├── orders/
│   │   ├── orders_load_helper_script.py
│   │   ├── orders_policies_kb_faqs.txt
│   │   └── orders_records.json
│   │
│   ├── payments/
│   │   ├── configure_payments_data_sources.sh
│   │   └── payments_policies_kb_faqs.txt
│   │
│   ├── promos/
│   │   ├── configure_promos_data_sources.sh
│   │   ├── promos_kb_faqs.txt
│   │   └── promos_records.json
│   │
│   └── stores/
│       ├── configure_store_data_sources.sh
│       ├── store_kb_faqs.txt
│       ├── stores_load_helper_script.py
│       └── stores_records.json
│
├── 3_proof_of_concept/
│   ├── agents/
│   │   ├── barista_supervisor_agent.py
│   │   ├── menu_agents.py
│   │   ├── orders_agents.py
│   │   ├── payments_agents.py
│   │   ├── promos_agents.py
│   │   └── stores_agents.py
│   │
│   └── knowledge_bases/
│       ├── menu_knowledge_base_setup.sh
│       ├── payments_knowledge_base_setup.sh
│       ├── promos_knowledge_base_setup.sh
│       ├── stores_knowledge_base_setup.sh
│       └── test_knowledge_bases.sh
│
├── 4_monitor_and_evaluate/
│   └── cloudwatchagent/
│
├── 5_security_rai/
│   ├── bedrock-agent-ec2-least-privilege.json
│   ├── create_and_store_guardrail.sh
│   ├── parameter_store_manager.py
│   └── validate_parameter_store.py
│
├── 6_deploy/
│   ├── agents/
│   ├── scripts/
│   └── web-app/
│
├── .gitignore
├── LICENSE
├── requirements.txt
└── README.md
```

## AWS Services Used

The project demonstrates integration with the following AWS services:

- Amazon Bedrock.
- Amazon Bedrock Knowledge Bases.
- Amazon DynamoDB.
- Amazon Aurora MySQL.
- Amazon S3.
- Amazon OpenSearch Serverless.
- AWS Lambda.
- AWS Secrets Manager.
- AWS Systems Manager Parameter Store.
- Amazon CloudWatch.
- Amazon Cognito.
- Amazon EC2.

The exact resources, identifiers, account values, and regions should be configured through environment variables and should not be committed to GitHub.

## Business Value Modeling

The project includes an interactive Streamlit application for evaluating potential AI use cases.

Run the application with:

```bash
streamlit run 1_business_modeling/business_value.py
```

The application allows users to explore:

- Order-taking automation.
- Customer-support automation.
- Inventory-management use cases.
- Operating costs.
- Time savings.
- Automation rates.
- Productivity gains.
- Customer-experience improvements.
- Estimated return on investment.

Business-value modeling helps determine whether an AI use case is worth implementing before investing in production development.

## Data Strategy

The data strategy separates operational data from policy and FAQ content.

### Operational Data

Operational data is used by agents to answer real-time business questions and perform actions.

Examples include:

- Customer orders stored in DynamoDB.
- Store information stored in Aurora MySQL.
- Promotion-related data accessed through application tools.

### Knowledge-Base Data

Policy and FAQ documents are stored in Amazon S3 and indexed for semantic retrieval.

Examples include:

- Order cancellation and refund policies.
- Menu and nutritional information.
- Store policies and amenities.
- Payment methods and troubleshooting.
- Promotions and offer terms.

This separation allows the agents to combine structured database queries with unstructured policy retrieval.

## Retrieval-Augmented Generation

The project uses Amazon Bedrock Knowledge Bases to implement Retrieval-Augmented Generation.

The RAG workflow is:

```text
Policy documents
      |
      v
Amazon S3
      |
      v
Knowledge Base ingestion
      |
      v
Text chunking and embeddings
      |
      v
Amazon OpenSearch Serverless
      |
      v
Semantic retrieval
      |
      v
Agent response generation
```

This approach allows agents to retrieve relevant business policies before generating a response, helping improve accuracy and reduce unsupported answers.

## Installation

### Prerequisites

You need:

- An AWS account with appropriate permissions.
- Python 3.11 or later.
- AWS CLI configured.
- Bash shell.
- Access to Amazon Bedrock models in the selected AWS Region.
- Required Python dependencies.
- Access to the required AWS data services.

Install the Python dependencies:

```bash
pip install -r requirements.txt
```

For deployment-related dependencies:

```bash
pip install -r 6_deploy/agents/requirements.txt
```

## Configuration

Do not commit AWS credentials or private environment configuration files.

Create your local environment configuration from a template:

```bash
cp .env.example .env
```

Then update the values for your environment.

Example configuration:

```bash
export AWS_REGION="your-aws-region"
export ORDERS_TABLE_NAME="your-orders-table"
export WORKSHOP_S3_BUCKET="your-s3-bucket"
export OPENSEARCH_COLLECTION_ARN="your-opensearch-collection-arn"
export ROLE_ARN="your-bedrock-role-arn"
```

Load the configuration before running the application:

```bash
source env.sh
```

The actual `env.sh`, `setup_env.sh`, and other environment-specific files should remain local and should not be committed.

## Data-Source Setup

The data-source scripts configure the application’s domain-specific data.

Examples:

```bash
cd 2_data_strategy/orders
python orders_load_helper_script.py
```

```bash
cd 2_data_strategy/stores
bash configure_store_data_sources.sh
```

```bash
cd 2_data_strategy/menu
bash configure_menu_data_sources.sh
```

```bash
cd 2_data_strategy/payments
bash configure_payments_data_sources.sh
```

```bash
cd 2_data_strategy/promos
bash configure_promos_data_sources.sh
```

These scripts may create or modify AWS resources. Review every script and confirm that the configured AWS Region and account are correct before execution.

## Knowledge-Base Setup

Knowledge bases are configured in:

```text
3_proof_of_concept/knowledge_bases/
```

To configure the remaining domain knowledge bases:

```bash
cd 3_proof_of_concept/knowledge_bases

bash stores_knowledge_base_setup.sh
bash menu_knowledge_base_setup.sh
bash payments_knowledge_base_setup.sh
bash promos_knowledge_base_setup.sh
```

To test knowledge-base retrieval:

```bash
bash test_knowledge_bases.sh
```

The test queries cover topics such as:

- Order issues.
- Menu and caffeine information.
- Store amenities.
- Payment methods.
- Promotional offers.

## Running the Multi-Agent Application

Navigate to the agents directory:

```bash
cd 3_proof_of_concept/agents
```

Load the environment variables:

```bash
source ../../env.sh
```

Start the Barista Supervisor agent:

```bash
python barista_supervisor_agent.py
```

Example questions to test:

```text
What drinks do you currently offer?
```

```text
I would like to order a medium cold brew.
```

```text
What do you have to eat?
```

```text
Can I find a store with a drive-through?
```

```text
What payment methods do you accept?
```

```text
How can I use the current promotions?
```

The supervisor should route each question to the appropriate specialized agent.

## Example Multi-Step Workflow

A typical order workflow may follow these steps:

1. The customer asks for available drinks.
2. The supervisor routes the question to the Menu Agent.
3. The Menu Agent checks menu availability.
4. The supervisor routes the request to the Payments Agent.
5. The Payments Agent calculates the total.
6. The customer confirms the order.
7. The supervisor routes the request to the Orders Agent.
8. The Orders Agent places the order and returns a confirmation.

This demonstrates how multiple specialized agents can collaborate to complete a single customer task.

## Security and Responsible AI

Security is an important part of this project.

Recommended practices include:

- Never commit AWS access keys, secret keys, passwords, or tokens.
- Use IAM roles instead of hardcoded credentials.
- Follow least-privilege permissions.
- Store secrets in AWS Secrets Manager or Systems Manager Parameter Store.
- Use Amazon Bedrock Guardrails where appropriate.
- Avoid placing personal, identifying, or confidential information in sample data.
- Validate agent inputs before performing business actions.
- Require confirmation before irreversible actions such as placing orders.
- Monitor agent activity and AWS resource usage.
- Restrict access to data sources according to business need.

Sensitive local files should be excluded using `.gitignore`.

## Monitoring and Evaluation

The monitoring components demonstrate how to observe application behavior and AWS workloads.

Recommended metrics include:

- Agent request count.
- Response latency.
- Error rate.
- Knowledge-base retrieval failures.
- Tool invocation failures.
- Token usage and model cost.
- Successful and failed order operations.
- Suspicious or unexpected agent behavior.

The monitoring files are located in:

```text
4_monitor_and_evaluate/
```

Evaluation should consider both technical and business outcomes, including:

- Response accuracy.
- Policy adherence.
- Correct agent routing.
- Tool-selection accuracy.
- Response latency.
- User satisfaction.
- Cost per interaction.
- Successful task completion rate.

## Deployment

Deployment-related files are located in:

```text
6_deploy/
```

This directory includes:

- Agent runtime configuration.
- Deployment scripts.
- Frontend files.
- Container configuration.
- Authentication configuration.
- Observability configuration.

Review the deployment scripts and replace environment-specific placeholders before using them in another AWS account.

## Important GitHub Safety Notes

Before pushing this project to GitHub, check that the following are excluded:

```text
.env
env.sh
setup_env.sh
check_env.sh
*.pem
*.key
credentials
__pycache__/
*.pyc
```

Check the files that Git is tracking:

```bash
git status
git ls-files
```

Search the project for possible secrets:

```bash
grep -RniE "aws_access_key_id|aws_secret_access_key|password|secret|token|api_key" . \
  --exclude-dir=.git \
  --exclude-dir=__pycache__
```

If credentials have already been pushed:

1. Revoke or rotate the credentials immediately.
2. Remove the sensitive files from the repository.
3. Remove them from Git history if necessary.
4. Review AWS CloudTrail and billing activity.

## Limitations

This repository is an educational and demonstration project.

It may require adaptation before production use, including:

- Stronger authentication and authorization.
- More comprehensive error handling.
- Automated testing.
- Data validation.
- Rate limiting.
- Cost controls.
- Production-grade logging.
- Human approval for high-impact actions.
- Improved prompt and response evaluation.
- Data retention and privacy controls.
- Infrastructure-as-code deployment.
- Multi-environment configuration management.

AWS services may incur costs when used outside a controlled training environment.

## Learning Outcomes

This project demonstrates the following capabilities:

- Generative AI use-case ideation.
- Quantitative AI business-value modeling.
- Streamlit application development.
- Multi-source data strategy design.
- Structured and unstructured data integration.
- Retrieval-Augmented Generation.
- Vector search with OpenSearch Serverless.
- Amazon Bedrock Knowledge Bases.
- Specialized AI agent development.
- Multi-agent collaboration.
- Tool-based agent workflows.
- AWS security and responsible AI considerations.
- Monitoring and evaluation of agentic applications.
- Deployment of an AI-powered web application.

## License

See the `LICENSE` file for the terms applicable to this repository.

## Disclaimer

This project is intended for learning and demonstration purposes. It is not an official AWS product and should not be used in production without additional security, testing, governance, privacy, reliability, and cost-control measures.
