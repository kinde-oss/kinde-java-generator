# Kinde Java SDK Generator

## Update config file

`kinde-config.yml` is the config file which will generate the SDK files. We'll need to update the config file with SDK file paths.

Change the first part of file list to the path of the SDK files. In case the SDK is located at the previous directory, no changes are needed to be made.

For example, yml file will become for each file from:
```yml
../international-kinde-java/src/main/java/org/openapitools/sdk/KindeClientSDK.java:
  destinationFilename: src/main/java/org/openapitools/sdk/KindeClientSDK.java
```
to:
```yml
/path/to/sdk/KindeClientSDK.java
  destinationFilename: src/main/java/org/openapitools/sdk/KindeClientSDK.java
```

## Generate

Run the following command to generate the code files with OpenAPI code generator:
```ssh
openapi-generator-cli generate -i kinde.yml -g spring -c kinde-config.yml -o kinde-java-sdk --skip-validate-spec
```
OR 
```ssh
openapi-generator generate -i kinde.yml -g spring -c kinde-config.yml -o kinde-java-sdk --skip-validate-spec
```

`kinde.yml` is the YML spec file here that will be used for code generation.

## Usage

Add the following dependency in pom.xml after generation:

```spring
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
</dependency>
```

Add the following plugins in pom.xml

```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <configuration>
        <includes>
            <include>**/*.java</include>
        </includes>
    </configuration>
</plugin>
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-jar-plugin</artifactId>
    <version>3.2.0</version>
    <executions>
        <execution>
            <goals>
                <goal>test-jar</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <finalName>kindejava</finalName>
    </configuration>
</plugin>
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
        <source>15</source>
        <target>15</target>
    </configuration>
</plugin>
```