# Kinde Java generator

The generator for the [Kinde Java SDK](<[link-to-sdk-repo](https://github.com/kinde-oss/kinde-java-sdk)>).

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](https://makeapullrequest.com) [![Kinde Docs](https://img.shields.io/badge/Kinde-Docs-eee?style=flat-square)](https://kinde.com/docs/developer-tools) [![Kinde Community](https://img.shields.io/badge/Kinde-Community-eee?style=flat-square)](https://thekindecommunity.slack.com)

## Overview

This generator creates an SDK in Java that can authenticate to Kinde using the Authorization Code grant or the Authorization Code with PKCE grant via the [OAuth 2.0 protocol](https://oauth.net/2/). It can also access the [Kinde Management API](https://kinde.com/api/docs/#kinde-management-api) using the client credentials grant.

Also, see the SDKs section in Kinde’s [contributing guidelines](https://github.com/kinde-oss/.github/blob/main/.github/CONTRIBUTING.md).

## Usage

[comment]: <> (### Requirements)

[comment]: <> (You will need the following tools to be able to generate the SDK.)

[comment]: <> (**`<todo>`**)

[comment]: <> (- [ ] Include details here on any tools required to use this generator, e.g. Docker. If none exist, remove the section altogether. **Note:** This is different to developing on the generator - see the Development section.)

[comment]: <> (**`</todo>`**)

### Initial set up

1. Clone the repository to your machine:

   ```bash
   git clone https://github.com/kinde-oss/kinde-java-generator
   ```

2. Go into the project:

   ```bash
   cd kinde-java-generator
   ```

3. Install the OpenAPI Generator tool:

   https://openapi-generator.tech/docs/installation

### SDK generation

Run the following command to generate the SDK:

```bash
openapi-generator-cli generate -i kinde.yml -g spring -c kinde-config.yml -o kinde-java-sdk --skip-validate-spec
```
OR
```bash
openapi-generator generate -i kinde.yml -g spring -c kinde-config.yml -o kinde-java-sdk --skip-validate-spec
```

**Note:** The API specifications should always point to Kinde's hosted version: https://kinde.com/api/kinde-mgmt-api-specs.yaml. This is set via the ` -i` option in the [OpenAPI Generator CLI](https://openapi-generator.tech/docs/usage/), for example:

```bash
openapi-generator-cli generate -i https://kinde.com/api/kinde-mgmt-api-specs.yaml
```

The SDK gets outputted to: kinde-java-sdk, which you can enter via:

```bash
cd kinde-java-sdk
```

## SDK documentation

[Java SDK](<[link-to-kinde-doc](https://kinde.com/docs/developer-tools/)>)

## Development


Add the following dependency in pom.xml after generation:

```spring
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
</dependency>
```

Afterwards make following changes in pom.xml

```
1. Locate the <build> section within the pom.xml file.
2. Replace the <build> with following

<build>
    <sourceDirectory>src/main/java</sourceDirectory>
    <plugins>
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
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <classifier>exec</classifier>
            </configuration>
        </plugin>
    </plugins>
</build>
```

## Contributing

Please refer to Kinde’s [contributing guidelines](https://github.com/kinde-oss/.github/blob/489e2ca9c3307c2b2e098a885e22f2239116394a/CONTRIBUTING.md).

## License

By contributing to Kinde, you agree that your contributions will be licensed under its MIT License.