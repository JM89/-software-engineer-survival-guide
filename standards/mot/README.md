# Application MOT

A MOT Check, but for Applications. 

> *MOT stands for the Ministry of Transport, the government department that introduced the test in 1960 as a means of testing vehicle safety, exhaust emissions, and roadworthiness.*

An application without addition of business features, may not be released often anymore and technical debt will accumulate progressively and silently. 

Similarly to your car that needs regular revision and pass basic checks yearly, this proposition is defining a checklist to review the state of your live applications.

The outcome "badge" will give an immediate feedback when looking at adding feature in an application.

## "Rules"

- The label "pass|fail" should be on top of the page of the service documentation. 
- In case of MOT failure, the action items must be prioritised ASAP and the MOT re-passed before x months.
- In case of MOT success but failing minor items, the action items must be prioritised before the next MOT, else, they will accumulate with other items on the next test.
- Add the "MOT" certificate history to the service documentation.

## Test

Max 10 points if in the critical path. 15 points otherwise. 

Since the last MOT:
- +1 for every incidents caused by this application
- +1 for every rollbacks to older system versions
- +1 for each security standards not applied (e.g. encryption)
- +1 for each observability standards not applied (e.g. logging, metrics)
- +1 for each infrastructure standards not applied (e.g. serverless, containers, release process)
- +1 for each pipeline standards not applied (e.g. ci pipeline up to date, automatic deployment)
- +1 for missing test coverage on critical features
- +1 for every major versions between current and latest frameworks (e.g. between dotnet 2.1 and 6: +4 points)
- +1 if service documentation is outdated/incomplete.
- +1 if feature flag was configured but never cleaned.

## Outcomes

[![Pass](https://img.shields.io/badge/MOT_01/01/2022-Passed-g.svg)](https://shields.io/)

[![Failed](https://img.shields.io/badge/MOT_01/01/2022-Failed-red.svg)](https://shields.io/)

