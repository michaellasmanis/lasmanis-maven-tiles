# Maven Tiles

| Branch | Status |
| ------ | ------ |
|Master|[![Build Status](https://img.shields.io/circleci/project/github/michaellasmanis/lasmanis-maven-tiles/master.svg?style=flat)](https://circleci.com/gh/michaellasmanis/lasmanis-maven-tiles/tree/master) [![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.lasmanis.maven.tiles/core-set-ossrh/badge.svg?style=flat)](https://maven-badges.herokuapp.com/maven-central/com.lasmanis.maven.tiles/core-set-ossrh)|

This project sets up the basic maven infrastructure for projects.

It configures the following basic items for your maven projects:

* Properties
    * project.build.sourceEncoding
    * project.reporting.outputEncoding
    * maven.compiler.source
    * maven.compiler.target
* POM elements
    * developers
    * distributionManagement
    * issueManagement
    * license
    * organization
    * scm urls
    * url
* Plugins
    * clirr-maven-plugin
    * exec-maven-plugin
    * flatten-maven-plugin
    * jacovo-maven-plugin
    * license-maven-plugin
    * maven-antrun-plugin
    * maven-assembly-plugin
    * maven-changes-plugin
    * maven-checkstyle-plugin
    * maven-clean-plugin
    * maven-dependency-plugin
    * maven-deploy-plugin
    * maven-enforcer-plugin
    * maven-gpg-plugin
    * maven-install-plugin
    * maven-jar-plugin
    * maven-javadoc-plugin
    * maven-jxr-plugin
    * maven-pmd-plugin
    * maven-project-info-reports-plugin
    * maven-release-plugin
    * maven-resources-plugin
    * maven-scm-plugin
    * maven-scm-plublish-plugin
    * maven-shade-plugin
    * maven-site-plugin
    * maven-source-plugin
    * maven-surefire-plugin
    * nexus-staging-maven-plugin
    * swagger-maven-plugin
    * templating-maven-plugin
    * versions-maven-plugin

The tile expects the following properties to be set:

* project.name : the name of the project
* project.version : the version of the project
* project.inceptionYear : year the project was starts
* repository.name : the name of the VCS repository
* gpg.keyname : key to be used for signing

Tiles can be used individually.  Several pre-defined sets are available:
* core-set-ossrh: Basic POM support with deployment to Maven Central.
* core-set-nodistribution: Basic POM support without deployment.
* java-set: Typical JDK8 setup.  You should also include a core-set set.

## Usage

Below is the basic usage pattern for inclusion in a pom:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.lasmanis</groupId>
    <artifactId>myartifact</artifactId>
    <version>${revision}.${changelist}</version>

    <packaging>jar</packaging>

    <name>My Project Name</name>
    <description>My Project Description</description>
    <inceptionYear>2020</inceptionYear>

    <properties>
        <revision>0.1</revision>
        <changelist>0-SNAPSHOT</changelist>
        <repository.name>myproject</repository.name>
        <tiles-maven.version>2.19</tiles-maven.version>
        <lasmanis-maven-tiles.version>0.0.0</lasmanis-maven-tiles.version>
    </properties>

    <url>${baseurl}</url>

    <scm>
        <connection>${scmBase.connection}</connection>
        <url>${scmBase.url}</url>
        <developerConnection>${scmBase.developerConnection}</developerConnection>
        <tag>${scmBase.tag}</tag>
    </scm>

    <distributionManagement>
        <site>
           <id>scm-publish</id>
           <url>${scmBase.connection}</url>
       </site>
    </distributionManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>io.repaint.maven</groupId>
                <artifactId>tiles-maven-plugin</artifactId>
                <version>${tiles-maven.version}</version>
                <extensions>true</extensions>
                <configuration>
                    <tiles>
                      <tile>com.lasmanis.maven.tiles:core-set-ossrh:${lasmanis-maven-tiles.version}</tile>
                      <tile>com.lasmanis.maven.tiles:java-set:${lasmanis-maven-tiles.version}</tile>
                    </tiles>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```
At a minimum, you should update project.artifactId, project.name, repository.name and lasmanis-maven-tiles.version.

gpg.keyname is typically set via a maven settings.xml file or the maven command line (-Dgpg.keyname=GPG_KEY_EMAIL).
