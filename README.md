# FirstApi approach with OpenAPI generator plugin and SpringDoc OpenAPI UI to your Spring Boot Project

*Tested with Java 17 and SpringBoot 2.7.7*

## STEP 1

**Add the following property version for openapitools in pom.xml:** </br>

```
<properties>
    <openapitools.generator.version>6.4.0</openapitools.generator.version>
</properties>
```

**Add the following dependencies:** </br>

```
    <!--OPENAPI GENERATOR MAVEN PLUGIN-->
    <dependency>
        <groupId>org.openapitools</groupId>
        <artifactId>openapi-generator-maven-plugin</artifactId>
        <version>${openapitools.generator.version}</version>
        <scope>provided</scope>
    </dependency>
    
    <dependency>
        <groupId>org.openapitools</groupId>
        <artifactId>jackson-databind-nullable</artifactId>
        <version>0.2.4</version>
    </dependency>
    
    <!--SPRINGDOC OPENAPI-->
    <dependency>
        <groupId>org.springdoc</groupId>
        <artifactId>springdoc-openapi-ui</artifactId>
        <version>1.6.13</version>
    </dependency>
```

## STEP 2

**Generate your api.yaml file**</br>
You can use https://editor.swagger.io/ </br>
Generate a file called api.yaml and place it in src/main/resources

## STEP 3

**Add the following plugging in your pom.xml file** </br>

```
    <!--OpenApi Codegen-->
    <plugin>
        <groupId>org.openapitools</groupId>
        <artifactId>openapi-generator-maven-plugin</artifactId>
        <version>${openapitools.generator.version}</version>
        <executions>
            <execution>
                <goals>
                    <goal>generate</goal>
                </goals>
                <configuration>
                    <inputSpec>${project.basedir}/src/main/resources/api.yaml</inputSpec>
                    <generatorName>spring</generatorName>
                    <generateApiTests>false</generateApiTests>
                    <generateModelTests>false</generateModelTests>
                    <modelNameSuffix>Dto</modelNameSuffix>
                    <configOptions>
                        <sourceFolder>src/gen/java/main</sourceFolder>
                        <oas3>true</oas3>
                        <useSpringController>true</useSpringController>
                        <useSpringfox>false</useSpringfox>
                        <interfaceOnly>true</interfaceOnly>
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
