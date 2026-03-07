---
title: Self-evaluation
has_children: false
nav_order: 12
---

# Self-evaluation

## Ethar Mohammed Hassan Ali

During this project, I contributed to all major phases, from initial setup and architecture alignment to implementation, testing, CI/CD configuration, release flow, and documentation updates. I worked on structuring the project according to the template requirements and ensuring the software remained functional both locally and in hosted environments.

## Role and contributions

I worked as the main contributor across implementation and integration tasks, with the following responsibilities:

- Designed and maintained the layered structure (`application`, `infrastructure`, `ui`) in line with the course template.
- Implemented and integrated core application features: user authentication, watchlist management, watched-history tracking, movie details retrieval, and recommendation flow.
- Developed and refined the Streamlit user interface, including search interactions, account area, recommendation/trending sections, and user feedback handling.
- Implemented persistence and data handling through SQLite, including account and interaction data storage.
- Improved project quality practices by working on automated tests, fixing CI failures, and aligning workflows for branch checks and releases.
- Worked on release and packaging activities (Poetry, semantic-release/TestPyPI), including version-alignment fixes and deployment troubleshooting.
- Contributed to report/documentation sections (for example concept, deployment, future work updates, and consistency fixes).

## Strengths of the product

- Clear and understandable project organization with separation of responsibilities.
- End-to-end user flow is available: account creation/login, preference handling, watchlist/watched tracking, and recommendations.
- Local setup and execution are straightforward using Poetry and SQLite.
- CI/CD and release workflow are in place and usable.
- Integration with external movie metadata APIs provides useful and rich movie information for users.

## Weaknesses and limitations

- Recommendation logic is currently heuristic and can be improved with more advanced ranking methods.
- The system depends on external APIs (OMDb/TMDb), so missing keys, rate limits, or network issues may reduce functionality.
- Hosted deployment may require extra attention for environment/runtime details (secrets, packaging behavior, persistence constraints).
- Some UI/UX aspects can be further polished for clarity and consistency.
- Testing is solid for core logic, but broader end-to-end UI coverage can still be expanded.

## Personal reflection

This project helped me improve practical software engineering skills beyond coding only: structuring a project, maintaining branch/release discipline, debugging deployment issues, and managing CI/CD and packaging workflows in a realistic team setting. It also highlighted areas where I want to improve further, especially recommendation design quality, deployment robustness, and test depth.
