# Gradle Executable Container

This docker image includes OpenJDK 8 and Gradle 2.12 configured with Gradle as the entrypoint.

## Usage

By defaut, running this image without any command will run `gradle -version` in the /usr/bin/app directory. 

### Doing Something Actually Useful
To run something more interesting, say `gradle clean war`, you should mount your project root in /app. For example, you can run the following to create a deployable web archive.

```bash
docker run --rm -v /path/to/your/project:/usr/src/app -v /root/.gradle/caches:/root/.gradle/caches asiazhang/gradle build
```

### Plugins
Of course, you can use any command here, including those dependent on plugins. For example, if you project inlcudes the Jetty plugin (by including `apply plugin: 'jetty'` in its build.gradle) you can run the following command to start an instance of Jetty running a WAR of your application on port 8080 on the host.

```bash
docker run --rm -p 8080:8080 -v /path/to/your/project:/usr/src/app -v /root/.gradle/caches:/root/.gradle/caches asiazhang/gradle jettyRunWar
```
