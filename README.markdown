# Maven Tiles

This project sets up the basic maven infrastructure for projects.

It configures the following basic items for your maven projects:

* Properties
    * project.build.sourceEncoding
    * project.reporting.outputEncoding
* POM elements
    * organization
    * developers
    * issueManagement
    * scm urls
* Plugins
    * flatten-maven-plugin
    * license-maven-plugin
    * maven-antrun-plugin
    * maven-assembly-plugin
    * maven-changes-plugin
    * maven-clean-plugin
    * maven-dependency-plugin
    * maven-deploy-plugin
    * maven-enforcer-plugin
    * maven-gpg-plugin
    * maven-install-plugin
    * maven-project-info-reports-plugin
    * maven-release-plugin
    * maven-resources-plugin
    * maven-scm-plugin
    * maven-site-plugin
    * nexus-staging-maven-plugin
    * versions-maven-plugin

The tile expects the following properties to be set:

* project.name : the name of the project
* project.version : the version of the project
* project.inceptionYear : year the project was starts
* repository.name : the name of the VCS repository
* gpg.keyname : key to be used for signing

## Usage

Below is the basic usage pattern for inclusion in a pom:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.lasmanis</groupId>
    <artifactId>myartifact</artifactId>
    <version>${revision}.${changelist}</version>
    <name>My Project Name</name>
    <inceptionYear>2018</inceptionYear>
    <properties>
        <revision>0.1</revision>
        <changelist>0-SNAPSHOT</changelist>
        <repository.name>myrepo</repository.name>
        <tiles-maven.version>2.16</tiles-maven.version>
        <maven-tiles-core.version>0.0.0</maven-tiles-core.version>
    </properties>
    <url>${baseurl}</url>
    <scm>
        <connection>${scm.connection}</connection>
        <url>${scm.url}</url>
        <developerConnection>${scm.developerConnection}</developerConnection>
        <tag>${scm.tag}</tag>
    </scm>
    <build>
        <plugins>
            <plugin>
                <groupId>io.repaint.maven</groupId>
                <artifactId>tiles-maven-plugin</artifactId>
                <version>${tiles-maven.version}</version>
                <extensions>true</extensions>
                <configuration>
                    <tiles>
                        <tile>com.lasmanis.maven.tiles:core-set-ossrh:${maven-tiles-core.version}</tile>
                    </tiles>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```
At a minimum, you should update project.artifactId, project.name, repository.name and maven-tiles-core.version.

gpg.keyname is typically set via a maven settings.xml file or the maven command line (-Dgpg.keyname=GPG_KEY_EMAIL).
