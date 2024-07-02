## LLM Retrieval Augmented Generation

(note: code coming soon)

Wouldn't it be great if there was a cost-effective way to interact with your documents as if you were conversing with a cutting-edge AI? Now you can, using Retrieval Augmented Generation (RAG)!

RAG combines vector search and advanced language models to deliver accurate, context-aware responses. What makes RAG truly cost-effective is that it doesn't require retraining the model. By retrieving relevant information from disparate sources like chat history and pdf documents, RAG enhances the language model's output, ensuring answers are relevant. Retrieval Augmented Generation offers a powerful, efficient way to interact with your documents, making the future of AI-driven document interaction a reality today.

Below I outline the process and architectural decisions around developing this project. Also included are a couple of videos recorded during our daily meetings. They are very raw but they showcase my ability to not only develop software, but also my ability to collaborate and explain complex topics.

### Process

[Video of me implementing the v0 Flask app](https://youtu.be/hov4eGjnOQ4?si=UgQR710oAuLiDPik)

To develop our Retrieval Augmented Generation (RAG) system, we adopted a lean agile approach, ensuring we delivered user value at every stage and quickly established an end-to-end Minimum Viable Product (MVP).

Initial Implementation in Jupyter Notebook:
We began with a Jupyter notebook where we implemented a basic RAG system based on a tutorial. This allowed us to experiment, iterate quickly, and validate the core concept in an interactive environment. This was already done when I took over the project.

Transition to Python Scripts:
Once the basic functionality was validated, we transitioned the notebook code into Python scripts. This step was crucial for modularizing the code, improving maintainability, and preparing it for integration into a larger system and deployment.

Development of a Flask App:
To create a user-friendly interface and make the RAG system accessible, we developed a Flask app. This web application provided an easy way for users to interact with the system, submit queries, and receive responses, showcasing the practical utility of RAG in real-world scenarios.

Throughout this process, our focus was on delivering user value by continuously iterating on user feedback and refining the system's functionality. By prioritizing a lean MVP approach, we ensured that the core features were up and running as quickly as possible, providing immediate benefits while allowing room for future enhancements.

### Architecture decisions

In developing our Retrieval Augmented Generation (RAG) system, we made several key architectural decisions to ensure robustness, scalability, and cost-effectiveness. This is just a small sample of the many decisions that went into developing this project.

_Monolithic Codebase with Modular Design:_

[Video of me whiteboarding this for the team](https://youtu.be/RKnX4UapHcQ)

Initially, we considered using two separate applications with a shared SDK to modularize the system, aiming to facilitate independent development and deployment. However, after coding both versions, we opted for a single monolithic codebase. This approach aligns with industry best practices for early-stage projects where simplicity and speed of development are crucial. A monolithic architecture allows for easier deployment, development, and debugging since all components are integrated into a single codebase, reducing the complexity of managing multiple codebases​ (Atlassian)​​ (CWS Technology Pvt. Ltd.)​.

Despite the monolithic codebase, we maintained a modular design. These could be separate applications but needed to access the database similarly. To facilitate this, the vector store and LLM are in a shared library folder, while the ETL has its own folder. This service-oriented approach ensures clear separation of concerns and easier management, though the source code is shared. The primary difference in the architecture lies in the organization of the source code, which resides in one repository instead of three separate ones for the client API, ETL, and SDK.

_Flask vs. AWS Chalice:_
We evaluated AWS Chalice for its seamless support of serverless architectures. While Chalice offers excellent integration with AWS services, it is limited to serverless environments. We chose Flask because it provides broader deployment options, allowing us to support both serverless and traditional server-based architectures. Flask’s flexibility and ease of use made it a more suitable choice for our needs, enabling us to maintain control over our infrastructure and accommodate future scaling requirements​ (Java Code Geeks)​.

_ETL Pattern vs. LangChain Patterns:_
Our data processing approach evolved significantly. Initially, we employed an explicit Extract, Transform, Load (ETL) pattern with separate endpoints for each stage, managing raw data, processed data, and embedded data in distinct tables. This setup used Alembic for version control and migration. As we progressed, we transitioned to LangChain-inspired patterns, integrating extraction, transformation, and embedding into a single process. We adopted PGVector as our vector store, leveraging PostgreSQL for cost-effective local development. This shift allowed us to streamline our data processing pipeline, improve efficiency, and reduce costs. We now manage raw data with Alembic, while processed data is handled by PGVector and SQLRecordStore from LangChain, providing a more integrated and efficient system​ (Atlassian)​​ (Java Code Geeks)​.

These architectural decisions were driven by our commitment to creating a robust, scalable, and cost-effective RAG system. By continuously evaluating and refining our approach, we ensured that our system meets real-world demands while remaining flexible and easy to maintain."
