This is a fork of the Spring Batch Admin code for Kit Digital UK, project Orion.

The parent pom has been modified to deploy the generated artifacts into Artifactory on our in house server.

# Building

mvn clean install <-P strict>

Strict will cause the build to halt on error, otherwise it will complete with success status in the presence of test failures.

# Deploying

mvn -Dmaven.test.skip=true deploy -P orion

# Authentication

In order to authenticate with artifactory you will require a settings.xml file in $M2_HOME containing the following, username + password our obtained
internally.

<?xml version="1.0" encoding="UTF-8"?>
<settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd" xmlns="http://maven.apache.org/SETTINGS/1.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <servers>
    <server>
		<username>TBD</username>
		<password>TBD</password>
		<id>orion</id>
	</server>
  </servers>
</settings>

# Hudson

As this is not a SNAPSHOT build, Hudson/maven will not pull updated artifacts unless there is a version number change.
Therefore old versions of the artifacts must be manually removed from the Hudson M2 repo.

e.g.

login to the relevant server as the Hudson user.

rm -rf .m2/repository/org/springframework/batch/spring-batch-admin-manager
rm -rf .m2/repository/org/springframework/batch/spring-batch-admin-resources
rm -rf .m2/repository/org/springframework/batch/spring-batch-admin-parent
rm -rf .m2/repository/org/springframework/batch/spring-batch-integration


