---
title: external-security-analysis-config
layout: default
parent: Modules configuration
---

The `external-security-analysis-config` module is used in the `com.powsybl.security.distributed.ExternalSecurityAnalysis`
class, an implementation of the `com.powsybl.security.SecurityAnalysis` interface, that submits the execution of a
[security-analysis](../../tools/security-analysis.md) command to the ComputationManager, when it's launched in external
mode.

# Required properties

## itools-command
The `itools-command` property is a required property that defines the iTools command to run. It throws a `ConfigurationException`
if this property is not set.

# Optional property

## debug
The `debug` property is an optional property that defines if the `security-analysis` should run in debug mode of not. The
default value of this property is `false`.

# Examples

## YAML
```yaml
external-security-analysis-config:
    debug: false
    itools-command: itools
```

## XML
```xml
<external-security-analysis-config>
    <debug>false</debug>
    <itools-command>itools</itools-command>
</external-security-analysis-config>
```
