# cursor_ai_use_cases

Prompt to provide code context to fix bugs

With the change of contexts, projects, team scopes and/or project scopes, there is a big problem related to the contextualization of developers in relation to the project operation, which services are called and where each implementation of a specific feature/component code is.

To help with this pain for developers, we suggest using Cursor AI in conjunction with Jira CLI:
-> Fetch the context of a task/bug (here we will specifically look at bugs due to the need for low SLA);
-> Combine with the context of a repo added to the cursor code base;
-> Provide a prompt and some default settings to automate we can have a highly assertive assessment.

With these points we intend to reduce the time to resolve a bug, improving the relationship of trust between the client and the company.

The steps we followed:

1. Configured the jira cli;
2. Attach the prompt below to the AI Cursor Agent context.
note: the code below has been considered and tested using macOS, and where there is BEESEDI-33394 replace it with the code for the required task.
3. Consider one or more repos for the codebase, which attached to the context will be the object of study for the analysis.
note: The model used was Claude-3.7-Sonnet


Here's an example of a case with a single repo as context:

![Captura_01](https://github.com/erikadeolima-abinbev/cursor_ai_use_cases/blob/main/captura_01.png?raw=true)
![Captura_02](https://github.com/erikadeolima-abinbev/cursor_ai_use_cases/blob/main/captura_02.png?raw=true)
![Captura_03](https://github.com/erikadeolima-abinbev/cursor_ai_use_cases/blob/main/captura_03.png?raw=true)
![Captura_04](https://github.com/erikadeolima-abinbev/cursor_ai_use_cases/blob/main/captura_04.png?raw=true)
![Captura_05](https://github.com/erikadeolima-abinbev/cursor_ai_use_cases/blob/main/captura_05.png?raw=true)

Here's an example of a case with a multi repo as context:

![Captura_06](https://github.com/erikadeolima-abinbev/cursor_ai_use_cases/blob/main/captura_06.png?raw=true)
![Captura_07](https://github.com/erikadeolima-abinbev/cursor_ai_use_cases/blob/main/captura_07.png?raw=true)

Here is the prompt we used:

```
# Prompts for Bug Analysis

Consider bees-android as a code repo for mobile android
Consider bees-ios as a code repo for mobile ios
Consider nfa-rewards as a code repo for web version (browser of any type, desktop or mobile)
Consider loyalty-bussiness-service as a code repo for api service for mobile versions
Consider rewards-bussiness-service as a code repo for api service for mobile versions
Topic: Analyze the task to be defined using the command below:
Run command jira issue view BEESEDI-33394 --raw to get the Story template (don't use any extra syntax like “| cat”)
With the return of this command considered as part of the context, and using the data of this return of this command together with the context of the cursor there, make an analysis of the bug to have a possible justification for the error, being something of the front end (mobile and web) or back-end (services)
Based on this task and the context attached to the cursor there, give me an analysis based on the template below.

## 1. Initial Bug Analysis

Describe the bug and provide:
1. Detailed description of the incorrect behavior
2. Version of the affected system/component
3. Frequency of occurrence
4. Impact on the system/business
5. Users/components affected

## 2. Technical Context Analysis

Analyze the technical context of the bug:
1. Technology stack involved
2. Dependencies and their versions
3. Integrated services/systems
4. Event environment (SIT, UAT, PROD)
5. Recent code changes

## 3. Analysis of Technical Symptoms

Identify the technical symptoms:
1. logs and error messages
2. Abnormal system behavior
3. Patterns of occurrence
4. Conditions that reproduce the bug
5. Known workarounds

## 4. Technical Cause Analysis

Explore the possible technical causes:
1. Source code problems
2. Integration problems
3. Configuration problems
4. Dependency problems
5. Infrastructure problems

## 5. Technical Impact Analysis

Assess the technical impact:
1. Severity of the bug
2. Complexity of the fix
3. Implementation risks
4. Dependencies affected
5. Need for changes in other repositories

## 6. Analysis of technical solutions

Propose technical solutions considering:
1. Short-term fixes
2. Necessary refactorings
3. Changes to dependencies
4. Estimated implementation time
5. Tests required

## Template for Dependency Analysis

Analyze the dependencies of the bug:
1. Related repositories:
   - [List of required repositories]
2. External dependencies:
   - [List of libraries/packages]
3. Integrated services:
   - [List of services]
4. Required configurations:
   - [List of configurations]
5. Access limitations:
   - [List of limitations]

## Template for the 5 Whys Method (Technical Context)

Bug: [DESCRIPTION]
1. Why is the bug occurring?
   Answer: [IMMEDIATE CAUSE]
   Repositories/Dependencies: [LIST]
2. Why is [IMMEDIATE CAUSE] happening?
   Answer: [SECONDARY CAUSE]
   Repositories/Dependencies: [LIST]
3. Why is [SECONDARY CAUSE] happening?
   Answer: [TERTIARY CAUSE]
   Repositories/Dependencies: [LIST]
4. Why is [TERTIARY CAUSE] happening?
   Answer: [QUATERNARY CAUSE]
   Repositories/Dependencies: [LIST]
5. Why is [QUATERNARY CAUSE] happening?
   Answer: [ROOT CAUSE]
   Repositories/Dependencies: [LIST]

## Usage Tips:
1. Always check the dependencies and related repositories
2. Document which repositories need to be attached to the context
3. Identify dependencies that need to be installed
4. Consider the impact on other services/systems
5. Keep a record of technical analysis and decisions
## Usage Example:

Analyze the [DESCRIPTION] bug and provide:
1. Technical description of the problem
2. Context and technical environment
3. Symptoms and logs
4. Possible technical causes
5. Impact on the system
6. Proposed technical solutions
7. Necessary repositories and dependencies
```
