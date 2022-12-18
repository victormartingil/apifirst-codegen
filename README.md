# FirstApi approach with OpenAPI generator plugin and SpringDoc OpenAPI UI to your Spring Boot Project

*Tested with Java 17 and SpringBoot 2.7.7*

## STEP 1

**Add the following dependencies:** </br>

```
<!--OPENAPI GENERATOR MAVEN PLUGIN-->
<dependency>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <version>6.2.1</version>
    <scope>provided</scope>
</dependency>

<!--SPRINGDOC OPENAPI-->
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-ui</artifactId>
    <version>1.6.13</version>
</dependency>

<!--DEPENDENCIES NEEDED FOR THE GENERATED SOURCES WITH OPENAPI TOOLS GENERATOR PLUGIN-->
<!--JAVAX WS RS-->
<dependency>
    <groupId>javax.ws.rs</groupId>
    <artifactId>javax.ws.rs-api</artifactId>
    <version>2.1.1</version>
</dependency>

<!-- GOOGLE GSON -->
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10</version>
</dependency>

<!--OKHTTP3-->
<dependency>
    <groupId>com.squareup.okhttp3</groupId>
    <artifactId>okhttp</artifactId>
    <version>4.10.0</version>
</dependency>

<!--OKHTTP3 LOGGING-->
<dependency>
    <groupId>com.squareup.okhttp3</groupId>
    <artifactId>logging-interceptor</artifactId>
    <version>4.10.0</version>
</dependency>

<!--APACHE OLTU-->
<dependency>
    <groupId>org.apache.oltu.oauth2</groupId>
    <artifactId>org.apache.oltu.oauth2.client</artifactId>
    <version>1.0.1</version>
</dependency>

<!--GSON FIRE-->
<dependency>
    <groupId>io.gsonfire</groupId>
    <artifactId>gson-fire</artifactId>
    <version>1.8.5</version>
</dependency>
```

## STEP 2

**Generate your api.yaml file**</br>
You can use https://editor.swagger.io/ </br>
Generate a file called api.yaml and place it in src/main/resources

## STEP 3

**Add the following plugging in your pom.xml file** </br>

```
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <!-- RELEASE_VERSION -->
    <version>6.0.0</version>
    <!-- /RELEASE_VERSION -->
    <executions>
        <execution>
            <goals>
                <goal>generate</goal>
            </goals>
            <configuration>
                <inputSpec>${project.basedir}/src/main/resources/api.yaml</inputSpec>
                <generatorName>java</generatorName>
                <generateApiTests>false</generateApiTests>
                <generateModelTests>false</generateModelTests>
                <configOptions>
                    <sourceFolder>src/gen/java/main</sourceFolder>
                    <oas3>true</oas3>
                    <useSpringController>true</useSpringController>
                    <useSpringfox>false</useSpringfox>
                </configOptions>
            </configuration>
        </execution>
    </executions>
</plugin>
```

## STEP 4

**Add the following property in application.properties file** </br>
_This is optional but could avoid few future problems_

```

spring.mvc.pathmatch.matching-strategy=ant-path-matcher

```

## STEP 5

**Implement the generated methods**</br>
To complete your API, you can implement the generated methods by the codegen plugging on the default path:</br>
_target/generated_sources/openapi/src/gen/java_

## STEP 6

**Check Swagger UI website**</br>
Run your application and access the following url to check your API documentation:

```

host:port/swagger-ui/index.html
http://localhost:8080/swagger-ui/index.html

```

http://localhost:8080/swagger-ui/index.html
