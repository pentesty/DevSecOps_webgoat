# DevSecOps - Pipeline

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Information](#information)
  - [Secure Development Process](#secure-development-processes)
  - [Awareness of Security Risks](#awareness-of-security-risks)

- [Tools and Resources](#tools-and-resources)
  - [Pre-commit or Pre-push hooks](#pre-commit-or-pre-push-hooks)
  - [Secret Scanning](#secret-scanning)
  - [SCA (Source composition analysis)](#sca-source-composition-analysis)
  - [SAST (Static Application Security Testing)](#sast-static-application-security-testing)
  - [DAST (Dynamic Application Security Testing)](#dast-dynamic-application-security-testing)
  - [Security monitoring and infrastructure misconfigurations](#security-monitoring-and-infrastructure-misconfigurations)

  - [Integration of security tools](#integration-of-security-tools)
  
<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Information


## Secure Development Processes

* [DevSecOps Guidlines](https://owasp.org/www-project-devsecops-guideline/)
* [OWASP secure coding practices](https://www.owasp.org/images/0/08/OWASP_SCP_Quick_Reference_Guide_v2.pdf)
* [Java-SE](https://www.oracle.com/java/technologies/javase/seccodeguide.html) - Secure Coding Guidelines for Java SE

## Awareness of Security Risks

* [OWASP Top 10](https://owasp.org/www-project-top-ten/) - Top 10 security risks from OWASP 

# Tools and Resources

## Pre-commit or Pre-push hooks

This tool is ued for

* [Tailsman](https://github.com/thoughtworks/talisman)

## Secret Scanning

This tool is used for 

* [TruffelHog](https://github.com/trufflesecurity/truffleHog)

## SCA (Source composition analysis)

Software Composition Analysis (SCA) tools find common open source libraries and components used in application, Compare findings to a list of known vulnerabilities (e.g., Common Vulnerabilities and Exposures, or CVEs) and determine whether components have known and documented vulnerabilities, are out of date, and have patches available

* [OWASP Dependancy Check](https://github.com/jeremylong/DependencyCheck)

## SAST (Static Application Security Testing)

SAST tools analyse source code to look for security issues in an application during non-running state, and are supported by a large number of languages. They usually have quite a high false positive rate, due to the fact they cannot track data through an app, instead using a bit of guesswork to determine if flaws exist.

* [SonarQube](https://www.sonarqube.org/) 

## DAST (Dynamic Application Security Testing)

DAST tools run automated penetration testing scans against a running service as a blackbox. It tries to hack into the service using well known vulnerabilities, however scans can take a while due to the vast number, as well as crawling services to find all the endpoints.

* [OWASP ZAP](https://github.com/zaproxy/zaproxy)

## Security monitoring and infrastructure misconfigurations

This is used for security monitoring

* [AWS Security Hub](https://aws.amazon.com/security-hub/?aws-security-hub-blogs.sort-by=item.additionalFields.createdDate&aws-security-hub-blogs.sort-order=desc)

## Integration of security tools
