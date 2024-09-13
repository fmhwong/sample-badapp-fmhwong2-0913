# Liberty Test Application - BadApp

## Build
1. `git clone` 
2. Please create `settings.xml` file under this path`${user.home}/.m2/`.Please replace TaaS artifactory server credentials for both `central` and `snapshots` entries.
```
<?xml version="1.0" encoding="UTF-8"?>
<settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd" xmlns="http://maven.apache.org/SETTINGS/1.1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	
  <servers>
    <server>
      <username>YOUR_EMAIL_ADDRESS</username>
      <password>YOUR_ARTIFACTORY_W3_ENCRYPTED_PASSWORD</password>
      <id>central</id>
    </server>
    <server>
      <username>YOUR_EMAIL_ADDRESS</username>
      <password>YOUR_ARTIFACTORY_W3_ENCRYPTED_PASSWORD</password>
      <id>snapshots</id>
    </server>
  </servers>
  <profiles>
    <profile>
      <repositories>
        <repository>
          <snapshots>
            <enabled>false</enabled>
          </snapshots>
          <id>central</id>
          <name>hyc-wassvt-team-maven-virtual</name>
          <url>https://na.artifactory.swg-devops.com/artifactory/hyc-wassvt-team-maven-virtual</url>
        </repository>
        <repository>
          <snapshots />
          <id>snapshots</id>
          <name>hyc-wassvt-team-maven-virtual</name>
          <url>https://na.artifactory.swg-devops.com/artifactory/hyc-wassvt-team-maven-virtual</url>
        </repository>
      </repositories>
      <pluginRepositories>
        <pluginRepository>
          <snapshots>
            <enabled>false</enabled>
          </snapshots>
          <id>central</id>
          <name>hyc-wassvt-team-maven-virtual</name>
          <url>https://na.artifactory.swg-devops.com/artifactory/hyc-wassvt-team-maven-virtual</url>
        </pluginRepository>
        <pluginRepository>
          <snapshots />
          <id>snapshots</id>
          <name>hyc-wassvt-team-maven-virtual</name>
          <url>https://na.artifactory.swg-devops.com/artifactory/hyc-wassvt-team-maven-virtual</url>
        </pluginRepository>
      </pluginRepositories>
      <id>artifactory</id>
    </profile>
  </profiles>
  <activeProfiles>
    <activeProfile>artifactory</activeProfile>
  </activeProfiles>
</settings>

```
3. `mvn install`

4. Follow this doc if you want to publish new [release](https://github.ibm.com/was-svt/svtMessageApp/wiki/How-to-publish-a-release-using-maven-release-plugin%3F)

## Run

`mvn liberty:run`

Or, drop the `target/badapp.war` into Liberty's `dropins` folder

- Write a random message to messages.log: http://localhost:9080/badapp/Angry
- Write a random JSON message to SystemOut/SystemErr: http://localhost:9080/badapp/AngryJson
- Write 5 trace messages: http://localhost:9080/badapp/Chatty
- Write 20 trace messages: http://localhost:9080/badapp/Chatty?numTraces=20
- Leak 1k bytes: http://localhost:9080/badapp/Leaky
- Leak 1M bytes: http://localhost:9080/badapp/Leaky?numBytes=1000000
- Sleep for a random amount of time up to 5s: http://localhost:9080/badapp/Pokey
- Sleep for a random amount of time up to 60s: http://localhost:9080/badapp/Pokey?delay=60000
- Sleep for 125 +/- 25 ms: http://localhost:9080/badapp/Steady
- Request a system GC: http://localhost:9080/badapp/Impatient
- Start a thread every 10 seconds until we reach the 8th thread, then allow all threads to run together for 30 seconds: http://localhost:9080/badapp/Spinny
- Start a thread every 5 seconds until we reach the 16th thread, then allow all threads to run together for 8 seconds: http://localhost:9080/badapp/Spinny?threads=16&delay=5&finalDelay=8
- Start a thread every 3 seconds until we reach the 10th thread, then allow all threads to run together for 5 seconds: http://localhost:9080/badapp/Spinny?threads=10&delay=3&finalDelay=5
