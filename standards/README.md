# Standard Guidelines

## Goals

- Gather guidelines on common engineering concerns
- Defines current recommended standards for new projects

## Guidelines

- [Application Lifecycle Management Shared Ownership](./guidelines/alm/README.md)
- [Version Control](./guidelines/vc/README.md)
    - [Branching Model](./guidelines/vc/br/README.md)
- [Application Standards](./guidelines/app-std/README.md)
- [Continuous Integration](./guidelines/ci/README.md)
- [Quality Gates](./guidelines/quality-gates/README.md)
    - [QA & Automated Test Suite](./guidelines/quality-gates/qa/README.md)
    - [Code Quality](./guidelines/quality-gates/code-quality/README.md)
    - [Test Coverage](./guidelines/quality-gates/test-coverage/README.md)
    - [Vulnerability Detection](./guidelines/quality-gates/vuln/README.md)
- [Continuous Delivery](./guidelines/cdelivery/README.md) 
    - [Approval process](./guidelines/cdelivery/approval/README.md)
    - [Blue/Green](./guidelines/cdelivery/bg/README.md)
    - [Canary](./guidelines/cdelivery/canary/README.md)
- [Pipeline As Code](./guidelines/pac/README.md)
- [Infrastructure As Code](./guidelines/iac/README.md)
- [Observability Standards](./guidelines/obs/README.md)
    - [Logging](./guidelines/obs/logging/README.md)
    - [Metrics](./guidelines/obs/metrics/README.md)
    - [Tracing](./guidelines/obs/tracing/README.md)
- [Access Control Strategies](./guidelines/ac/README.md)
- [Encryption](./guidelines/enc/README.md)
    - [Sensitive configurations](./guidelines/enc/sensitive-config/README.md)
    - [At rest](./guidelines/enc/at-rest/README.md)
    - [In transit](./guidelines/enc/in-transit/README.md)
- [Documentation](./guidelines/doc/README.md)

## Continuous Improvements 

Everything which falls into the above guidelines will need regular review and system will have to upgrade over time. 

Continous improvement is about:
- removing technical debt by upgrading the existing systems regularly, without waiting for business changes
- avoiding massive migration/standard alignment efforts for a single person at a bad time
- maintaining an updated list of adopted standards (in line with what the tech market/support offers) 
- keeping templates/shared components up-to-date for new services
- planning/prioritising the work for aligning to standards and technical debt for existing applications in an progressive manner
- encouraging contributions from all engineers (e.g. presentations, mentoring)

To contribute to this repository, follow the [guidelines](./CONTRIBUTING.md).

## System Design Considerations

*TODO: Serverless computing, containerisation, cloud provider, storage type, etc.*

## Doc Templates

- [Standard Definition](./templates/standard-group/README.md)
- [ADR Template](./templates/standard-group/adrs/ADR-000.md.md)


