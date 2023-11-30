# Access Control Strategies

## Goals

- Onboard new joiners quickly but safely 
- Ensure the Principle of least privilege

## Scope

In scope:
- Authentication/Authorization to shared servers for BAU work function (e.g. CI/CD/Monitoring)
- Authentication/Authorization to shared servers for support functions (e.g. Data storages)
- Access to 3rd Party Tools/API Keys (e.g. postman, external provider)
- Access to internal product API Keys

Out of scope:
- N/A

## Solution Overview

> *TODO: Short description of the techs/tools used. If applicable, mention about its known limitations.*

Accessing tools:

| Service/Server | Authentication | Authorization | 
|---|---|---|
| CI Server | Automatically assigned via SSO on start date | Automatically assigned. |
| CD Server | Automatically assigned via SSO on start date | Automatically assigned. |
| Logging System | Explicit request via SSO: [link](link) |  Assignment by Team Leader. |
| Production DB | Special request: [link](link) | Special request: [link](link) |
| ... | ... | ... |

Best practices:
- Use SSO whenever possible
- Use user groups/roles, not individual permissions
- Activate MFA whenever possible 
- Never use root passwords 
- Request only what you need (minimal permissions to ensure business functions). If access is required due to lack of support tools, ensure these tools are made available instead
- Keep your personal and team secrets secured and organised
- Keep a level of granularity for test/prod services

## Changes

| ADR | Date | Status | Reasons |
|---|---|---|---|
| - | - | Implicit | No standard previously defined |
