# 1. Vytvoreni Docker image pomoci Dockerfile

    mvn clean package
    docker build --tag hello-spring-boot .
    docker run --rm -it -p 8080:8080 --name hello-spring-boot hello-spring-boot

# 2. Vytvoreni Docker image BEZ Dockerfile POZOR!!! OMEZENE!!!

    mvn spring-boot:build-image
    docker run --rm -it -p 8080:8080 --name spring-boot-app spring-boot-app:0.0.1-SNAPSHOT

# 3. Vytvoreni Docker image BEZ Dockerfile

- JIB plugin
- mvn clean compile com.google.cloud.tools:jib-maven-plugin:2.4.0:build -B -Djib.to.auth.username=USERNAME -Djib.to.auth.password=$GITLAB_PASS

            <plugin>
                <groupId>com.google.cloud.tools</groupId>
                <artifactId>jib-maven-plugin</artifactId>
                <version>2.4.0</version>
                <configuration>
                    <from>
                        <image>adoptopenjdk/openjdk11-openj9:alpine-jre</image>
                    </from>
                    <to>
                        <image>registry.gitlab.com/USERNAME/NAZEV_PROJEKTU</image>
                    </to>
                    <container>
                        <jvmFlags>
                            <jvmFlag>-Djava.security.egd=file:/dev/./urandom</jvmFlag>
                            <jvmFlag>-Duser.timezone=Europe/Prague</jvmFlag>
                            <jvmFlag>-Xtune:virtualized</jvmFlag>
                        </jvmFlags>
                        <args>
                            <arg>--spring.profiles.active=prod</arg>
                        </args>
                    </container>
                </configuration>
            </plugin>
