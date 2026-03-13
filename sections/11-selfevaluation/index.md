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

----------

## Kosar Mazaheri

## My Role in the Project

In this project, I mainly focused on the backend logic and quality assurance aspects of the system. My primary contributions were:

-   Implementing the OMDb API integration
    
-   Writing and structuring the unit tests
    
-   Understanding and managing the CI/CD workflow
    
-   Contributing significantly to the technical sections of the report
    

I also spent a considerable amount of time resolving integration issues between branches and stabilizing the system before the first release.

I would describe my role as someone who focused on making the system reliable, structured, and professionally organized.

----------

## What I Contributed

### OMDb Integration

I was responsible for integrating the OMDb external API into the application. This required:

-   Designing a separate OmdbClient to respect the layered architecture
    
-   Making sure the UI did not directly call the API
    
-   Handling errors properly (e.g., missing API key, movie not found)
    
-   Managing environment configuration for the API key
    

This part was challenging because it introduced external dependencies and required careful architectural consistency.

----------

### Testing

I developed the unit tests for the application layer. My goal was to ensure that:

-   Business logic was properly validated
    
-   Delegation between layers worked correctly
    
-   Future changes would not silently break functionality
    

Writing tests forced me to deeply understand the system structure and exposed several inconsistencies that I later fixed.

----------

### CI/CD and Workflow

I reviewed and worked with the GitHub Actions workflows to understand how:

-   Static checks and type validation were performed
    
-   Tests were executed across multiple operating systems and Python versions
    
-   Releases were automated
    

Although I did not design the entire pipeline from scratch, I ensured it remained functional after structural changes and during integration.

----------

## Strengths of the Product

-   The architecture is clean and well separated into layers.
    
-   The system is testable and includes automated validation.
    
-   The integration with an external API makes the application realistic.
    
-   The CI pipeline enforces a professional development process.
    

I believe the product reflects a good balance between simplicity and engineering discipline.

----------

## Weaknesses of the Product

-   The system is not designed for scalability; it would need architectural redesign for production-level use.
    
-   Password handling is simplified for academic purposes and not secure enough for real-world deployment.
    
-   UI testing is minimal.
    
-   The system relies directly on the external API without caching or fallback strategies.
    

These are limitations we accepted due to time and scope constraints.

----------

## My Strengths During the Project

-   I was persistent when debugging difficult integration and configuration issues.
    
-   I paid close attention to architectural consistency.
    
-   I tried to maintain professional standards in testing and documentation.
    
-   I connected implementation decisions with report explanations.
    

----------

## Areas Where I Could Improve

-   I could have synchronized earlier with teammates to reduce merge conflicts.
    
-   I could have planned database schema evolution more proactively.
    
-   I could have introduced integration tests earlier in development.
    

This project showed me how important early coordination and planning are in collaborative development.

----------

## Final Reflection

This project helped me better understand:

-   Practical layered architecture
    
-   API integration in real applications
    
-   The importance of automated testing
    
-   How CI/CD supports team collaboration
    

More importantly, it helped me experience what it means to work on a structured software project rather than just writing isolated code. I learned not only technical skills, but also workflow discipline and collaboration awareness.

----------

## Personal reflection

This project helped me improve practical software engineering skills beyond coding only: structuring a project, maintaining branch/release discipline, debugging deployment issues, and managing CI/CD and packaging workflows in a realistic team setting. It also highlighted areas where I want to improve further, especially recommendation design quality, deployment robustness, and test depth.
