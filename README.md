## RPM for JBoss Application Server

The missing RPM and init script for JBoss AS and EAP version 5.

This project creates an RPM file for JBoss RPM and adds init scripts for stopping and starting jboss in the RPM. 

Version 1.0 is available in https://github.com/henrik242/jboss-rpm/releases/tag/v1_0

To communicate or ask questions to project members - feel free to use our issue management system.

### Getting started

To build the project you will need to install RPM build tools

* On Fedora this is done by installing some packages. Run as root:
```
  $ yum groupinstall "Development Tools"
  $ yum install rpmdevtools maven2
```
* On Centos/RHEL install the following packages as root:
```
  $ yum install rpm-build
```
* On Centos/RHEL maven2 can be installed from here http://maven.apache.org/download.html

* On Ubuntu install the following packages as root:
```
  $ apt-get install rpm maven2
```

### RPM build instructions:  3 options

#### Prerequisites

Ensure that you have a .rpmmacros file in your $HOME directory.
A sample of this file is provided in rpmmacros.sample.

##### Option 1: Regular build

Run `mvn clean install`.  This will download and build the source, and create the RPM.

##### Option 2: Build manually from SVN
```
  $ mkdir jboss-eap-5.0-src; cd jboss-eap-5.0-src
  $ svn co http://anonsvn.jboss.org/repos/jbossas/tags/JBPAPP_5_0_0_GA jboss-as
  $ cd jboss-as/build
  $ ant
  $ cd ../../..
  $ mvn clean install -Djboss.skip.download -Djboss.skip.unzip -Djboss.skip.build
```
##### Option 3: Download the binary

Download the binary (login required): https://support.redhat.com/jbossnetwork/restricted/listSoftware.html?product=appplatform
```
  $ mkdir -p jboss-eap-5.0-src/jboss-as/build/output/jboss-5.0.0.GA
  $ unzip <zipfile> -d jboss-eap-5.0-src/jboss-as/build/output/jboss-5.0.0.GA
  $ mvn clean install -Djboss.skip.download -Djboss.skip.unzip -Djboss.skip.build  
```
#### Successful build: The RPM

The resulting RPM is located in `target/rpm/jboss-eap/RPMS/`

### Why we don't distribute RPM binaries

The legal terms stated in the JBoss EULA states that it is not allowed to redistribute JBoss without removing its images and trademarks. For that reason we are not going to redistribute JBoss but instead describe how to dowload the distribution and create the RPM file yourself using a simple maven2 script.

See also https://jira.jboss.org/jira/secure/attachment/12312677/JBossEULA.txt
