# Jenkins-CI-CD-Automation-follow below mentioned steps

**pipelineCI-1:**
================
In automation, version numbers are generated automatically using dynamic values like:

Jenkins Build Number
Git Commit Hash
Date/Time
Environment Variable

So no need to manually update version every time.

Lets understand  the environment, VERSION, -Dversion, and build section.

1. environment block

environment {
  VERSION = "1.0.${BUILD_NUMBER}"
}

This defines environment variables used throughout your pipeline.
VERSION is a variable we're creating.
"1.0.${BUILD_NUMBER}" combines static text (1.0.) with Jenkins built-in variable ${BUILD_NUMBER}.
**Example:**
If the current Jenkins build number is 6, then:
VERSION = 1.0.6

2. What is -Dversion=${VERSION} in Maven?
sh 'mvn clean package -Dversion=${VERSION}'
The -Dversion=... is a Maven command-line property. Here's what it means:

-D stands for define a system property.

You're telling Maven:
➤ "Hey, use this value as the version inside the build."

🧠 But here's the catch:

Maven will only respect this -Dversion=... if your pom.xml is written to use it.

For example, in pom.xml, you'd need:
<version>${version}</version>
If not written that way, Maven still uses the version hardcoded in your pom.

3. Artifact Naming stage
sh 'mv target/myapp.jar target/myapp-${VERSION}.jar'

This renames the JAR file after build.
Default Maven output is: target/myapp.jar
This step renames it to something like:
myapp-1.0.6.jar (dynamic version)

So every pipeline run creates a uniquely named artifact.

Note:
If your pom.xml doesn’t use ${version}, the -Dversion won’t change anything internally, but the renamed WAR file will still carry the version info.
Would you like help modifying your pom.xml to support this versioning fully?

Output:
<img width="1140" height="465" alt="image" src="https://github.com/user-attachments/assets/ad0502fe-61a2-4369-b144-08415b25f23e" />

