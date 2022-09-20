# Application Standards

## Goals

- Facilitate the creation of new standard application via templates (e.g. GitHub Templates, Dotnet Templates)
- Reduce code duplication of standard approach via shared libraries (e.g. logging/metrics standards)
- Bring consistency & avoid re-inventing the wheel for each project
- Provide a central place for application standard description (self-documented if applicable)

## Scope

In scope:
- Repository & Project Structure (e.g. Onion architecture)
- Choosen Framework/Language (Version) - (e.g. you may not want to move to a version until fully stable)
- Latest References to Standard Libraries & to CI pipelines (when applicable)

Out of scope:
- Coding Standards (besides the one covered in templates)
- Quality Gates (covered by [Quality Gates](../quality-gates/README.md))

## Solution Overview

> *TODO: Short description of the techs/tools used. If applicable, mention about its known limitations.*

| Project Type | Template |
|---|---|
| Background Workers | [Link]() |
| REST APIs | [Link]() |
| Scheduled Jobs | [Link]() |
| Serverless Functions | [Link]() |
|...|...|

Best practices:
* These templates are used as reference architecture. They should be kept up-to-date and all engineers should contribute. Cf. [Continuous Improvement](../cimprov/README.md).

## Changes

| ADR | Date | Status |Reasons |
|---|---|---|---|
| - | - | Deprecated | No standard previously defined |
