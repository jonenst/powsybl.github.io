---
title: itools-packager
layout: default
---

The `itools-packager` Maven plugin provides a way to assemble distribution bundles based on [iTools](../tools/index.md).

The layout of such distribution is the following:
```
<package-name>
├── bin
│   ├── itools
│   ├── itools.bat
│   ├── powsyblsh
│   └── tools-mpi-task.sh
├── etc
│   ├── itools.conf
│   └── logback-itools.xml
├── lib
└── share
    └── java
        ├── <jars>
```

# Goals overview
The `itools-packager` only has one goal.
- The `package` goal creates a compressed package based on `iTools` with three types of output compression format:
zip, tar.gz, tar.bz2.

# Configuration

## Properties

### archiveName
The `archiveName` property defines the basename of the archive. If this property is not set, `itools-packager` uses the
packageName. The iTools-packager supports three types of output compression format: zip, tar.gz, tar.bz2.

### packageName
The `packageName` property defines the name of the root folder of the distribution. If this property is not set,
`itools-packager` uses the finalName of the maven project.

### configName
The `configName` property defines the the basename of the configuration file. The default value is `config`

### javaXmx
The `javaXmx` property defines the amout of the Java Heap memory. The default value is 8 Gb. This property is used to
initialize the `java_xmx` property of the `itools.conf` file.

### mpiHosts
The `mpiHosts` property defines the list of hosts of the MPI cluster. The default value is `localhost`. This property is used to
initialize the `mpi_hosts` property of the `itools.conf` file.

### mpiTasks
The `mpiTasks` property defines the maximum number of parallel tasks. The default value is 2. This property is used to
initialize the `mpi_tasks` property of the `itools.conf` file.

### copyToBin
The `copyToBin` property defines the list of files to copy in the `bin` directory of the distribution.

### copyToLib
The `copyToLib` property defines the list of files to copy in the `etc` directory of the distribution.

### copyToEtc
The `copyToEtc` property defines the list of files to copy in the `etc` directory of the distribution.

## Example
```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.powsybl</groupId>
            <artifactId>powsybl-itools-packager-maven-plugin</artifactId>
            <version>${powsybl.core.version}</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>package</goal>
                    </goals>
                </execution>
            </executions>
            <configuration>
                <packageName>powsybl</packageName>
                <archiveName>powsybl-V${project.version}</archiveName>
                <javaXmx>512M</javaXmx>
            </configuration>
        </plugin>
    </plugins>
</build>
```

# Usage
The `itools-packager` plugin copies all the maven dependencies to the `share/java` folder of the distribution. To enable
a feature, add a runtime dependency to the `pom.xml` file. Refer to the [iTools](../tools/index.md) documentation to
learn more about existing `iTools` commands.

The `itools-packager` demo gives the minimal configuration of an `iTools` based distribution.
```shell
$> git clone https://github.com/powsybl/powsybl-tutorials.git
$> cd powsybl-tutorials/itools-packager
$> mvn package
$> cd target/powsybl/bin
$> ./itools --help
usage: itools [OPTIONS] COMMAND [ARGS]

Available options are:
    --config-name <CONFIG_NAME>   Override configuration file name
    --parallel                    Run command in parallel mode

Available commands are:

```
