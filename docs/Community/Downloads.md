---
layout: doc_page
---
<!--
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.
-->
## Downloads

### Download Source Zip Files and Signatures
Choose the most recent release version from [https://downloads.apache.org/incubator/datasketches/](https://downloads.apache.org/incubator/datasketches/).
* Select the Component directory you are interested in (cpp, hive, java, memory, pig, postgresql).  Note the characterization and vector components do not have formal Apache releases. Go directly to the GitHub sites for those.
* Under your chosen component directory, choose the release of interest. We generally recommend that you choose the latest release. 

### Download Java Jar Files
From [Maven Central](https://search.maven.org/search?q=g:%20org.apache.datasketches).

### Download Shapshot Versions
Clone or fork the current SNAPSHOT directly from the relevant [DataSketches repository](https://github.com/apache?utf8=%E2%9C%93&q=datasketches).

### Version Numbers
Apache DataSketches uses [semantic versioning](https://semver.org/). Version numbers use the form major.minor.incremental and are incremented as follows:

* __major version__ for major new functionality and/or major API changes that may be incompatible with prior versions
* __minor version__ for new functionality and scheduled bug fixes. This should be API compatible with prior versions
* __incremental version__ for unscheduled bug fixes only

The zip files downloaded from [incubator-datasketches-xxx](https://www.apache.org/dyn/closer.cgi?path=/incubator/datasketches)
include a version number in the name, as in _apache-datasketches-java-1.1.0-incubating-src.zip_. 
This same number is also in the top section of the pom.xml file.

If you are developing using Maven and want to use, for example, datasketches-java, add the following dependencies to your pom.xml file:

```
<dependency>
  <groupId>org.apache.datasketches</groupId>
  <artifactId>datasketches-java</artifactId>
  <version>1.2.0-incubating</version>
</dependency>
```


#### Release Philosophy

These are fully tested, production quality releases, and hopefully as bug-free as humanly possible. 
However, the code is continuously evolving and improvements in performance, documentation, additions 
to the API, and bug fixes do occur.  When enough of these build up, especially for bug fixes or 
performance improvements, a new release will be issued and the <b>minor</b> 
digit will be incremented.  The <b>incremental</b> digit will only be used for bug fixes as stated above.

As stated above, the <b>major</b> digit is being reserved for major refactorings of the library where backward API 
compatibility may not be guaranteed. 

For the repositories that depend on java core, such as <i>incubator-datasketches-hive</i>, 
the version number may be incremented just to be in sync with the java core repository, 
and may not reflect any actual code changes other than a change in the pom.xml to reflect the new 
dependency. 

If you just want to run Hive and don't require direct access to the <i>incubator-datasketches-java</i> it is
recommended that you download the "with-shaded-core.jar", which includes the Hive jar as well as 
shaded versions of the core jar and memory jar. The shading avoids conflicts with other possible versions
of core Java and Memory that you might have in your system.


#### SNAPSHOT Jars
If you want the latest and greatest version of the code, it is certainly OK for you to create your 
own snapshot jars from a clone or fork. 
The code is automatically tested using the current test suite, but you might catch the code in
transition to a new future release. Caveat Emptor.

### Version History
Please use GitHub revisions history on the respective component repositories


 
