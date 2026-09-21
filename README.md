\# AI Day 1 Lab

\## Agentic AI: Foundations and Open-Source Practice

This lab compares three approaches for solving the same college course-fee problem:

1\. \*\*Plain LLM Chatbot\*\*

2\. \*\*Rule-Based Workflow\*\*

3\. \*\*Tool-Using AI Agent\*\*

The purpose of the lab is to understand the difference between a chatbot, a deterministic workflow, and an agent that can select and use tools.

\---
# AI Day 1 Lab

## Agentic AI: Foundations and Open-Source Practice

This lab compares three approaches for solving the same college course-fee problem:

1. **Plain LLM Chatbot**
2. **Rule-Based Workflow**
3. **Tool-Using AI Agent**

The purpose of the lab is to understand the difference between a chatbot, a deterministic workflow, and an agent that can select and use tools.

---

## 1. Objective

The objectives of this lab are:

- Set up a Python environment for AI application development.
- Connect an application to an LLM using Groq.
- Build a plain LLM chatbot.
- Build a rule-based workflow.
- Build a tool-using AI agent.
- Compare the three approaches using the same questions.
- Observe the agent's tool-calling process.
- Test the systems with a new challenge question.

---

## 2. Technologies Used

- Python 3.13.5
- OpenAI Python SDK
- Groq API
- `openai/gpt-oss-20b`
- python-dotenv
- Git
- GitHub

---

## 3. Project Structure

```text
AI-Day-1-Lab/
│
├── .gitignore
├── requirements.txt
├── config.py
├── check_setup.py
├── chatbot.py
├── workflow.py
├── tools.py
├── agent.py
└── challenge.py

.env contains the Groq API key and is intentionally excluded from GitHub using .gitignore.

4. Course Fee Data

The private course-fee data used in this lab is:

Course	Fee
CS101	₹12,000
AI202	₹18,000
DS303	₹15,000
5. Questions Used
Q1

What is the fee for AI202?

Q2

What is the total fee for CS101 and AI202 after a 10% scholarship?

Q3

Is DS303 more expensive than CS101, and by how much?

Q4

Write a two-line welcome message for new AI students.

6. System 1 — Plain LLM Chatbot

The chatbot sends the question directly to the LLM without providing the private course-fee data or any tools.

Output
Q1
Q: What is the fee for AI202?

A: I’m happy to help! Could you let me know which college or university you’re referring to? The fee for a course labeled “AI202” can vary depending on the institution, program level (undergraduate vs. graduate), and whether it’s a credit or non-credit course. Once I have that information, I can give you the exact fee.
Q2
Q: What is the total fee for CS101 and AI202 after a 10% scholarship?

A: Sure! To calculate the total fee after a 10% scholarship, I’ll need the original tuition amounts for each course. Could you let me know the fees for CS101 and AI202? Once I have those, I can compute the discounted total for you.
Q3
Q: Is DS303 more expensive than CS101, and by how much?

A: I’m not sure of the current prices for those courses. Could you let me know how much DS303 and CS101 cost? Once I have the numbers, I can tell you whether DS303 is more expensive and by how much.
Q4
Q: Write a two-line welcome message for new AI students.

A: Welcome to the AI Academy!
Embark on a journey where curiosity fuels innovation and every challenge becomes an opportunity.
Observation

The chatbot could generate general text, but it did not have access to the private course-fee information.

7. System 2 — Rule-Based Workflow

The workflow uses predefined rules and does not use an LLM.

Output
=== SYSTEM 2: RULE-BASED WORKFLOW (no LLM) ===

Q: What is the fee for AI202?
A: Fee for AI202: Rs. 18,000

Q: What is the total fee for CS101 and AI202 after a 10% scholarship?
A: Total fee: Rs. 27,000

Q: Is DS303 more expensive than CS101, and by how much?
A: Sorry, I do not have a rule for this type of question.

Q: Write a two-line welcome message for new AI students.
A: Sorry, I can only answer questions about course fees.
Observation

The workflow was reliable for questions covered by its predefined rules, but it could not handle questions outside those rules.

8. System 3 — Tool-Using AI Agent

The agent uses an LLM together with two tools:

get_course_fee — retrieves the fee of a course.
calculator — performs arithmetic calculations.

The agent can decide which tools are required, execute them, observe the results, and continue until it can produce an answer.

Output
Q1
Q: What is the fee for AI202?

step 1: get_course_fee({'course_code': 'AI202'}) -> 18000

A: The fee for AI202 is ₹18,000.
Q2
Q: What is the total fee for CS101 and AI202 after a 10% scholarship?

step 1: get_course_fee({'course_code': 'CS101'}) -> 12000
step 2: get_course_fee({'course_code': 'AI202'}) -> 18000
step 3: calculator({'expression': '(12000+18000)*0.9'}) -> 27000.0

A: The total fee for CS101 and AI202 after a 10% scholarship is ₹27,000.
Q3
Q: Is DS303 more expensive than CS101, and by how much?

step 1: get_course_fee({'course_code': 'DS303'}) -> 15000
step 2: get_course_fee({'course_code': 'CS101'}) -> 12000
step 3: calculator({'expression': '15000-12000'}) -> 3000

A: Yes. DS303 costs ₹15,000, while CS101 costs ₹12,000.
Difference: DS303 is ₹3,000 more expensive than CS101.
Q4
Q: Write a two-line welcome message for new AI students.

A: Welcome to the AI program!
We're thrilled to have you join our community of innovators and thinkers.
9. Challenge Question
Question

I can pay Rs. 30,000. Which two courses can I take together within this budget?

Workflow Output
--- WORKFLOW ---
Sorry, I can only answer questions about course fees.

The workflow could not handle the new type of question because no predefined rule existed for this task.

Agent Output
--- AGENT ---

step 1: get_course_fee({'course_code': 'CS101'}) -> 12000
step 2: get_course_fee({'course_code': 'AI202'}) -> 18000
step 3: get_course_fee({'course_code': 'DS303'}) -> 15000
step 4: calculator({'expression': '12000+18000'}) -> 30000
step 5: calculator({'expression': '12000+15000'}) -> 27000

The agent identified the following combinations:

Courses	Total Fee
CS101 + AI202	₹30,000
CS101 + DS303	₹27,000

Both combinations are within the ₹30,000 budget.

10. Observations

The following table is based on the actual runs performed during the lab.

Criterion	Chatbot	Workflow	Agent
Q1 correct? (Y/N)	N	Y	Y
Q2 correct? (Y/N)	N	Y	Y
Q3 correct? (Y/N)	N	N	Y
Q4 handled well? (Y/N)	Y	N	Y
Challenge question handled? (Y/N)	Not tested	N	Y
Same output on a repeat run? (Y/N)	Not tested	Not tested	Not tested
Approximate response time	~3.84 s	~0.99 s	~7.2 s
Number of LLM calls per question	1	0	Varies
One strength	Simple and conversational	Fast and predictable	Flexible and tool-using
One weakness	No access to private data	Rigid predefined rules	Depends on LLM/tool-calling
Best suited for	General conversation	Fixed rule-based tasks	Dynamic tasks requiring tools
11. Agent Trace — Question 2
Question

What is the total fee for CS101 and AI202 after a 10% scholarship?

Step	Tool called and arguments	Result (observation)
1	get_course_fee({'course_code': 'CS101'})	12000
2	get_course_fee({'course_code': 'AI202'})	18000
3	calculator({'expression': '(12000+18000)*0.9'})	27000.0
12. Response Time Measurements

The response times were measured using PowerShell Measure-Command.

Chatbot
TotalSeconds : 3.8363288

Approximate time:

~3.84 seconds
Workflow
TotalSeconds : 0.9887608

Approximate time:

~0.99 seconds
Agent

First measurement:

TotalSeconds : 7.4108674

Second measurement:

TotalSeconds : 6.9904537

Approximate time:

~7.2 seconds
13. Key Comparison
Chatbot
Uses only the LLM.
Does not have access to private course-fee data.
Can generate natural-language responses.
Cannot reliably answer questions requiring unavailable private information.
Workflow
Uses predefined rules.
Does not require an LLM.
Fast and predictable.
Fails when a question is outside the predefined rules.
Agent
Uses an LLM together with tools.
Can select appropriate tools.
Can combine multiple tool results.
Can perform calculations using the calculator tool.
Can handle new questions more flexibly.
Tool-calling behavior depends on the LLM.
14. Setup
Create Virtual Environment
python -m venv venv

Activate on Windows PowerShell:

venv\Scripts\Activate.ps1
Install Dependencies
pip install -r requirements.txt
Required Packages
openai>=1.40.0
python-dotenv>=1.0.0
Environment Variables

Create a .env file locally:

PROVIDER=groq
GROQ_API_KEY=YOUR_GROQ_API_KEY
MODEL=openai/gpt-oss-20b

Never commit or share the .env file because it contains the API key.

15. How to Run
Check Setup
python check_setup.py
Run Chatbot
python chatbot.py
Run Workflow
python workflow.py
Run Tools
python tools.py
Run Agent
python agent.py
Run Challenge
python challenge.py
16. Result

The experiment demonstrated the differences between a plain LLM chatbot, a rule-based workflow, and a tool-using AI agent.

The chatbot was able to generate natural-language responses but did not have access to private course-fee data. The workflow was fast and predictable for predefined cases but was rigid when presented with new question types. The agent used tools to retrieve course information and perform calculations, allowing it to handle the challenge question by combining multiple tool results.
\## 1. Objective

The objectives of this lab are:

\- Set up a Python environment for AI application development.

\- Connect an application to an LLM using Groq.

\- Build a plain LLM chatbot.

\- Build a rule-based workflow.

\- Build a tool-using AI agent.

\- Compare the three approaches using the same questions.

\- Observe the agent's tool-calling process.

\- Test the systems with a new challenge question.

\---

\## 2. Technologies Used

\- Python 3.13.5

\- OpenAI Python SDK

\- Groq API

\- \`openai/gpt-oss-20b\`

\- python-dotenv

\- Git

\- GitHub

\---

\## 3. Project Structure

\`\`\`text

AI-Day-1-Lab/

│

├── .gitignore

├── requirements.txt

├── config.py

├── check\_setup.py

├── chatbot.py

├── workflow.py

├── tools.py

├── agent.py

└── challenge.py

.env contains the Groq API key and is intentionally excluded from GitHub using .gitignore.

##4. Course Fee Data

The private course-fee data used in this lab is:

CourseFee

CS101₹12,000

AI202₹18,000

DS303₹15,000

\---

##5. Questions Used

Q1

What is the fee for AI202?

Q2

What is the total fee for CS101 and AI202 after a 10% scholarship?

Q3

Is DS303 more expensive than CS101, and by how much?

Q4

Write a two-line welcome message for new AI students.

\---

##6. System 1 — Plain LLM Chatbot

The chatbot sends the question directly to the LLM without providing the private course-fee data or any tools.

Output

Q1

Q: What is the fee for AI202?

A: I’m happy to help! Could you let me know which college or university you’re referring to? The fee for a course labeled “AI202” can vary depending on the institution, program level (undergraduate vs. graduate), and whether it’s a credit or non-credit course. Once I have that information, I can give you the exact fee.

Q2

Q: What is the total fee for CS101 and AI202 after a 10% scholarship?

A: Sure! To calculate the total fee after a 10% scholarship, I’ll need the original tuition amounts for each course. Could you let me know the fees for CS101 and AI202? Once I have those, I can compute the discounted total for you.

Q3

Q: Is DS303 more expensive than CS101, and by how much?

A: I’m not sure of the current prices for those courses. Could you let me know how much DS303 and CS101 cost? Once I have the numbers, I can tell you whether DS303 is more expensive and by how much.

Q4

Q: Write a two-line welcome message for new AI students.

A: Welcome to the AI Academy!

Embark on a journey where curiosity fuels innovation and every challenge becomes an opportunity.

Observation

The chatbot could generate general text, but it did not have access to the private course-fee information.

\---

##7. System 2 — Rule-Based Workflow

The workflow uses predefined rules and does not use an LLM.

Output

\=== SYSTEM 2: RULE-BASED WORKFLOW (no LLM) ===

Q: What is the fee for AI202?

A: Fee for AI202: Rs. 18,000

Q: What is the total fee for CS101 and AI202 after a 10% scholarship?

A: Total fee: Rs. 27,000

Q: Is DS303 more expensive than CS101, and by how much?

A: Sorry, I do not have a rule for this type of question.

Q: Write a two-line welcome message for new AI students.

A: Sorry, I can only answer questions about course fees.

Observation

The workflow was reliable for questions covered by its predefined rules, but it could not handle questions outside those rules.

\---

##8. System 3 — Tool-Using AI Agent

The agent uses an LLM together with two tools:

get\_course\_fee — retrieves the fee of a course.

calculator — performs arithmetic calculations.

The agent can decide which tools are required, execute them, observe the results, and continue until it can produce an answer.

Output

Q1

Q: What is the fee for AI202?

step 1: get\_course\_fee({'course\_code': 'AI202'}) -> 18000

A: The fee for AI202 is ₹18,000.

Q2

Q: What is the total fee for CS101 and AI202 after a 10% scholarship?

step 1: get\_course\_fee({'course\_code': 'CS101'}) -> 12000

step 2: get\_course\_fee({'course\_code': 'AI202'}) -> 18000

step 3: calculator({'expression': '(12000+18000)\*0.9'}) -> 27000.0

A: The total fee for CS101 and AI202 after a 10% scholarship is ₹27,000.

Q3

Q: Is DS303 more expensive than CS101, and by how much?

step 1: get\_course\_fee({'course\_code': 'DS303'}) -> 15000

step 2: get\_course\_fee({'course\_code': 'CS101'}) -> 12000

step 3: calculator({'expression': '15000-12000'}) -> 3000

A: Yes. DS303 costs ₹15,000, while CS101 costs ₹12,000.

Difference: DS303 is ₹3,000 more expensive than CS101.

Q4

Q: Write a two-line welcome message for new AI students.

A: Welcome to the AI program!

We're thrilled to have you join our community of innovators and thinkers.

\---

##9. Challenge Question

Question

I can pay Rs. 30,000. Which two courses can I take together within this budget?

Workflow Output

\--- WORKFLOW ---

Sorry, I can only answer questions about course fees.

The workflow could not handle the new type of question because no predefined rule existed for this task.

Agent Output

\--- AGENT ---

step 1: get\_course\_fee({'course\_code': 'CS101'}) -> 12000

step 2: get\_course\_fee({'course\_code': 'AI202'}) -> 18000

step 3: get\_course\_fee({'course\_code': 'DS303'}) -> 15000

step 4: calculator({'expression': '12000+18000'}) -> 30000

step 5: calculator({'expression': '12000+15000'}) -> 27000

The agent identified the following combinations:

CoursesTotal Fee

CS101 + AI202₹30,000

CS101 + DS303₹27,000

Both combinations are within the ₹30,000 budget.

\---

##10. Observations

The following table is based on the actual runs performed during the lab.

CriterionChatbotWorkflowAgent

Q1 correct? (Y/N)NYY

Q2 correct? (Y/N)NYY

Q3 correct? (Y/N)NNY

Q4 handled well? (Y/N)YNY

Challenge question handled? (Y/N)Not testedNY

Same output on a repeat run? (Y/N)Not testedNot testedNot tested

Approximate response time~3.84 s~0.99 s~7.2 s

Number of LLM calls per question10Varies

One strengthSimple and conversationalFast and predictableFlexible and tool-using

One weaknessNo access to private dataRigid predefined rulesDepends on LLM/tool-calling

Best suited forGeneral conversationFixed rule-based tasksDynamic tasks requiring tools

\---

##11. Agent Trace — Question 2

Question

What is the total fee for CS101 and AI202 after a 10% scholarship?

StepTool called and argumentsResult (observation)

1get\_course\_fee({'course\_code': 'CS101'})12000

2get\_course\_fee({'course\_code': 'AI202'})18000

3calculator({'expression': '(12000+18000)\*0.9'})27000.0

\---

##12. Response Time Measurements

The response times were measured using PowerShell Measure-Command.

Chatbot

TotalSeconds : 3.8363288

Approximate time:

~3.84 seconds

Workflow

TotalSeconds : 0.9887608

Approximate time:

~0.99 seconds

Agent

First measurement:

TotalSeconds : 7.4108674

Second measurement:

TotalSeconds : 6.9904537

Approximate time:

~7.2 seconds

\---

##13. Key Comparison

Chatbot

Uses only the LLM.

Does not have access to private course-fee data.

Can generate natural-language responses.

Cannot reliably answer questions requiring unavailable private information.

Workflow

Uses predefined rules.

Does not require an LLM.

Fast and predictable.

Fails when a question is outside the predefined rules.

Agent

Uses an LLM together with tools.

Can select appropriate tools.

Can combine multiple tool results.

Can perform calculations using the calculator tool.

Can handle new questions more flexibly.

Tool-calling behavior depends on the LLM.

\---

##14. Setup

Create Virtual Environment

python -m venv venv

Activate on Windows PowerShell:

venv\\Scripts\\Activate.ps1

Install Dependencies

pip install -r requirements.txt

Required Packages

openai>=1.40.0

python-dotenv>=1.0.0

Environment Variables

Create a .env file locally:

PROVIDER=groq

GROQ\_API\_KEY=YOUR\_GROQ\_API\_KEY

MODEL=openai/gpt-oss-20b

Never commit or share the .env file because it contains the API key.

\---

##15. How to Run

Check Setup

python check\_setup.py

Run Chatbot

python chatbot.py

Run Workflow

python workflow.py

Run Tools

python tools.py

Run Agent

python agent.py

Run Challenge

python challenge.py

16\. Result

The experiment demonstrated the differences between a plain LLM chatbot, a rule-based workflow, and a tool-using AI agent.

The chatbot was able to generate natural-language responses but did not have access to private course-fee data. The workflow was fast and predictable for predefined cases but was rigid when presented with new question types. The agent used tools to retrieve course information and perform calculations, allowing it to handle the challenge question by combining multiple tool results.
