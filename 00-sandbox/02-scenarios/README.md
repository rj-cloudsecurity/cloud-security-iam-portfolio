# Scenarios

Preparation for work and job applications. A scenario is a realistic work situation, as you meet it in an IAM role: a request from a department, an incident, an audit or something that needs to be automated.

This is separate from the [SC-300 exercises](/00-sandbox/01-oceanic-airlines/). There I try things out; here I work through a situation from start to finish.

## How it works
1. The assignment is drafted with the help of AI, as a situation that matches what happens in a real workplace
2. I carry it out myself in Microsoft Entra ID, and write scripts where needed
3. I record what I did, what the result was and what I would do differently next time
4. What is not possible in my tenant, I describe as a limitation

## Structure of a scenario
- **Situation:** what is going on and who is asking
- **Assignment:** what needs to happen and which requirements it must meet
- **Approach:** what I chose and why
- **Result:** what was built, with evidence (screenshot, log or script)
- **Retrospective:** what went well, what did not, what I would do differently

## Types
- **Request:** a department asks for something, for example access for contractors
- **Incident:** something goes wrong, for example an account that is being misused
- **Audit:** proving that something is correct, for example who has administrator rights
- **Automation:** a recurring task with a script or workflow

## Overview

| # | Scenario | Type | Status |
|---|----------|------|--------|
| S01 | No standing Global Administrators (PIM) | Audit | Planned |
| S02 | Conditional Access baseline | Request | Planned |
| S03 | Finding inactive users with a script | Automation | Planned |
| S04 | Joiner, mover, leaver | Automation | Planned |
| S05 | Contractors: temporary access | Request | Planned |
| S06 | Managing guests | Request | Planned |
| S07 | PIM for Groups | Request | Planned |

The list grows: new scenarios are added as I complete or receive them.
