
# Self-Evaluation – Kosar

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
