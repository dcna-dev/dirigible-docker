# dirigible-docker
This repository contains the necessary files to deploy an Eclipse Dirigible instance with Postgresql using Docker Compose.

From the official website, Eclipse Dirigible is:

Eclipse Dirigible provides capabilities for end-to-end development process from database modeling and management, through RESTful services authoring using various dynamic languages, to pattern-based user interface generation, role based security, external services integration, testing, debugging, operations, and monitoring.

This configuration follows the official documentation to deploy with Tomcat (https://www.dirigible.io/help/setup_tomcat.html) and Postgres (https://www.dirigible.io/help/setup_tomcat_postgresql.html). A custom pom.xml is used to generate only the target server-all and build a smaller image. Despite that, the resulted image is almost 670MB size. To achieve an even smaller image, the Docker Multistage Build is used to generate a final image with 165MB and only what is necessary to deploy the system.

To deploy Dirigible with Postgres as database using docker-compose, follow these instructions:

- Clone this repo:
- git clone https://github.com/dcna-io/dirigible-docker.git
- Modify the environment file (.env) to configure the database access.
- Modify the dirigible/tomcat_users.xml to configure users and passwords.
- Run docker-compose up
- Access https://localhost:8080

# To deploy the Eclipse Dirigible in Google Kubernetes Engine

- Clone this repo:
- git clone https://github.com/dcna-io/dirigible-docker.git
- Export an env variable with the path to your GCP credentials:
- export GOOGLE_APPLICATION_CREDENTIALS=/path/to/your/credentials.json
- Export an env variable with GCP project ID:
- export PROJECT_ID="$(gcloud config get-value project -q)"
- Build the docker image:
- docker build -t gcr.io/${PROJECT_ID}/dirigible ./dirigible
- Push the created image to GCP registry:
- docker push gcr.io/${PROJECT_ID}/dirigible
- Go to cloud/dev/ and edit the variables in all .tfvars files
- Execute terragrunt apply-all
- Access the Dirigible app using the IP address shown  at the end of execution
