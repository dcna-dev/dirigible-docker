# dirigible-docker
This repository contains the necessary files to deploy an Eclipse Dirigible instance with Postgresql using Docker Compose.

From the official website, Eclipse Dirigible is:

Eclipse Dirigible provides capabilities for end-to-end development process from database modeling and management, through RESTful services authoring using various dynamic languages, to pattern-based user interface generation, role based security, external services integration, testing, debugging, operations, and monitoring.

This configuration follows the official documentation to deploy with Tomcat (https://www.dirigible.io/help/setup_tomcat.html) and Postgres (https://www.dirigible.io/help/setup_tomcat_postgresql.html). A custom pom.xml is used to generate only the target server-all and build a smaller image. Despite that, the resulted image is almost 670MB size. To achieve an even smaller image, the Docker Multistage Build is used to generate a final image with 165MB and only what is necessary to deploy the system.

To deploy Dirigible with Postgres as database using docker-compose, follow these instructions:

- Clone this repo: git clone https://github.com/dcna-io/dirigible-docker.git
- Switch to docker branch: git checkout docker
- Modify the environment file (.env) to configure the database access.
- Modify the dirigible/tomcat_users.xml to configure users and passwords.
- Run docker-compose up
- Access https://localhost:8080
