FROM openjdk:8-alpine

RUN set -x && \
  apk --no-cache add --update git maven
RUN git clone https://github.com/eclipse/dirigible.git /opt/dirigible
WORKDIR /opt/dirigible
COPY pom.xml .
RUN mvn clean install -DskipTests

FROM tomcat:alpine

RUN rm -rf  $CATALINA_HOME/webapps/ROOT
COPY --from=0 /opt/dirigible/releng/server-all/target/ROOT.war $CATALINA_HOME/webapps/
COPY tomcat_users.xml $CATALINA_HOME/conf/tomcat-users.xml
RUN wget https://jdbc.postgresql.org/download/postgresql-42.2.5.jar -P $CATALINA_HOME/lib/
EXPOSE 8080

