# GraphCEP

In order to get the appropriate Eclipse version and features to be able to run the projects developed in the context of our paper [1], please follow the following steps.

- Download Scala IDE for Eclipse 4.7.0 from http://scala-ide.org/ and launch it with eclipse.exe (for Windows) or eclipse.app (for Mac).
- Install Maven plugin for Scala on Eclipse:
	* Click on Help-> Install New Software...
	* Select Add...
	* Write a name (for example 'Maven Scala').
	* Paste the following URL in 'Location' space: http://alchim31.free.fr/m2e-scala/update-site/
	* Press 'OK'.
	* Select 'Maven Integration for Eclipse' checkbox and click on Next button every time it appears until the installation finishes. If 'The installation cannot be completed as requested' message appears select 'Show original error and build my own solution' on the radiobutton and choose 'Install different version than originally requested' and 'Update items already installed'.
	* Restart Eclipse.

Please note that the execution of our projects may throw an OutOfMemory error.
In order to prevent this, the Java Heap Space needs to be increased with the parameter -Xmx10G. 
This can be done as follows:

- Right click on the runnable class in the project and select Run As...->Run Configurations.
- Select Java Application and create a new Configuration.
- Go to window 'Arguments' and write the parameter -Xmx10G in the 'VM arguments' field. 

If you have increased this parameter and you still have memory errors, try to increase the parameter as much as your computer permits.

## Maven Dependencies Solutions

Note that our projects use Maven to build dependencies on them. Sometimes, when importing a Maven project and updating dependencies, they can be downloaded wrongly and this can cause errors. To solve this problem it is necessary to follow these steps:
- Right click on the Maven project and select Run as-> Maven clean.
- Right click on the Maven project and select Run as-> Maven install.
- Update the project right clicking on the Maven project and selecting Maven->Update project.

## Watch the Scala version

Our cases 2, 3 and 4 have been built with Scala version 2.11. It is necessary to check if the 'Scala Library Container' contained in the Scala project folder has the proper version when you import the project. If the version of 'Scala Library Container' is different from 2.11, follow these steps:

- Right click on scala project and click on 'Properties'.
- Select 'Scala Compiler' on the left menu.
- Select 'Use Project Settings' checkbox.
- Select 'Latest 2.11 bundle (dynamic)' on 'Scala installation' option.
- Click on 'Apply and Close'.
- Update maven dependencies as we explain above.

## Last remark

Some of our artifacts have two projects: a Scala project and a Java project. The first one contains the source code and the second one is an auxiliary project that allows to export a jar file.


# Case 1 - Motorbike4Esper Project

Motorbike example with Esper technology.

This project sends a particular amount of simple events, selected from a configuration file, to an Esper engine and returns complex events built from simple events and the execution time. 

With this project we have obtained results shown in Table 1 - "Esper" row and Table 2 - "Esper" row of our paper.

## Getting Started

In the following we provide intructions on how to run this project. Please go to 'deployment' below for a description on how to deploy the project on a live system.

### Prerequisites

For running the project you need:

- Internet connection.
- Scala IDE for Eclipse (our tests have been run with the version described at the beginning of this document).
- Java JDK 1.8.

### Project Import and Configuration

To install the project follow these steps:

1. Import project 'motorbikeProject' into workspace.
2. Update maven dependencies right clicking on 'motorbikeProject' project and selecting Maven->Update project. If after this step there are still error dependencies, follow steps mentioned on 'Maven Dependencies Solutions' at the beginning of this document.
3. Open the 'config.properties' file located in 'motorbikeProject' project to set the configuration parameters:
	- NUM_EVENTS -> set the number of events to run a test.
	- DELAY -> set to 'TRUE' if you want to test it with a delay of 1 second between events (results Table 1 - Row 2) and 'FALSE' otherwise (results Table 2 - Row 2). 
Note that selecting DELAY to 'TRUE' will make the execution take the same amount of seconds as value of NUM_EVENTS.

## Running the tests

To run our experiments follow these steps:

- In 'config.properties' set 'NUM_EVENTS' to 5000, 10000, 20000 or 30000.
- Set 'DELAY' to TRUE to test it with a delay and set to FALSE otherwise.
- Right click on Main.java file on 'motorbikeProject' located on src/main/java/com/cor/cep/ project: Run as -> Java Application.

Results will be shown on the console.

## Deployment

In order to export a jar file:
- Right Click on 'motorbikeProject' project and select Run As...->Maven Install.
- When Maven Install finishes the jar file will be created in /motorbikeProject/target/.
- Note that to run the jar file you have to copy 'motorbike.csv' and 'config.properties' (of 'motorbikeProject' project) files in the same folder as the jar.

## Built With

* [Maven](https://maven.apache.org/) - Dependency Management.
* [Spring](https://spring.io/) - Architecture framework.


# Case 2 - Motorbike4Graphx Project

Motorbike example with Spark technology. 

This project sends a particular amount of simple events, selected from a configuration file, to a graph and returns complex events built from simple events and the execution time. 

With this project we have obtained results shown in Table 1 - "Spark" row and Table 2 - "Spark" row of our paper.

For this artifact we have two projects:

- motorbike4Graphx: scala project with the source code.
- MotorbikeGraph: java project to export a jar file of the project.

## Getting Started

In the following we provide intructions on how to run this project. Please go to 'deployment' below for a description on how to deploy the project on a live system.

### Prerequisites

For running the project you will need:

- Internet connection.
- Scala IDE for Eclipse (our tests have been run with the version described at the beginning of this document).
- Java JDK 1.8.
- Scala version 2.11 - if your version is not this one, follow the instructions described in section 'Watch the Scala version' at the beginning of this document.


### Project Import and Configuration

To import the projects follow these steps:

1. Import project 'MotorbikeGraph' into workspace right clicking on Package Explorer of Eclipse and selecting Import->General->Existing Projects into Workspace.
2. Import project 'motorbike4Graphx' into workspace right clicking on Package Explorer of Eclipse and selecting Import->Maven->Existing Maven Projects.
3. Update maven dependencies right clicking on 'motorbike4Graphx' project and selecting Maven->Update project. If after this step there are still error dependencies, follow steps mentioned on 'Maven Dependencies Solutions' at the beginning of this document.
4. Open 'config.properties' located in 'MotorbikeGraph' project to set the configuration parameters:
	- NUM_EVENTS -> set the number of events to run a test.
	- DELAY -> set to 'TRUE' if you want to test with a delay of 1 second between events (results Table 1 - Row 3) and 'FALSE' otherwise (results Table 2 - Row 3). 
Note that selecting DELAY to 'TRUE' will make the execution take the same amount of seconds as value of NUM_EVENTS.

## Running the tests

To run our experiments follow these steps:

- In 'config.properties' set 'NUM_EVENTS' to 5000, 10000, 20000 or 30000.
- Set 'DELAY' to TRUE to test it with a delay and set to FALSE otherwise.
- Right click on Main.java file on 'MotorbikeGraph' project and located on src/main/java/com/cor/graphx: Run as -> Java Application.

Results will be shown on the console. The two last log messages of 'MotorbikeEventGenerator' class will show the execution time of sending all simple events selected in the configuration file and the start timestamp. 
Note that at the time the last simple event has been sent, not all complex events have been processed. To calculate the exact execution time of processing complex events, it is necessary to substract the start timestamp to the timestamp of the last complex event produced (first value in the tuple of the last log message in the console).

Note that this project will never stop the execution in Eclipse because our queries run in an infinite loop, but the console will stop showing results when the last complex event has been produced.

## Deployment

To export a jar file:

- Right Click on 'MotorbikeGraph' project and select Export->Runnable JAR File->Next->Finish.
- Note that to run the jar file you have to copy 'motorbike.csv' and 'config.properties' (of 'MotorbikeGraph' project) files in the same folder as the jar.

## Built With

* [Apache Spark - Graphx tool](https://spark.apache.org/docs/latest/graphx-programming-guide.html) - The technology used.
* [Maven](https://maven.apache.org/) - Dependency Management.
* [Scala](https://www.scala-lang.org/) - Coding Language.


# Case 3 - TwitterFlickrStatic Project

TwitterFlickr example with Spark technology. 

This project creates a graph with synthetic data from a configuration file, runs our queries five times and shows their execution times on the console to calculate the mean execution time of each query.

With this project we have obtained results shown in Table 3 of our paper.

For this artifact we have two projects:

- TwitterUserStatic: scala project with the source code.
- TwitterFlickr: java project to export a jar file of the project.

## Getting Started

In the following we provide intructions on how to run this project. Please go to 'deployment' below for a description on how to deploy the project on a live system.

### Prerequisites

For running the project you need:

- Internet connection.
- Scala IDE for Eclipse (our tests have been run with the version described at the beginning of this document).
- Java JDK 1.8.
- Scala version 2.11 - if your version is not this one, follow the instructions described in section 'Watch the Scala version' at the beginning of this document.


### Project Import and Configuration

To import the projects follow these steps:

1. Import project 'TwitterFlickr' into workspace right clicking on Package Explorer of Eclipse and selecting Import->General->Existing Projects into Workspace.
2. Import project 'TwitterUserStatic' into workspace right clicking on Package Explorer of Eclipse and selecting Import->Maven->Existing Maven Projects.
3. Update maven dependencies right clicking on 'TwitterUserStatic' project and selecting Maven->Update project. If after this step there are still error dependencies, follow steps mentioned on 'Maven Dependencies Solutions' at the beginning of this document.
4. Open 'config.properties' located in 'TwitterFlickr' project to set the configuration parameters:
	- numInactiveTwitterUsers: number of Inactive Twitter Users.
	- numInfluencerTwitterUsers: number of Influencer Twitter Users.
	- numActiveTwitterUsers: number of Active Twitter Users.
	- numFlickrUsers: number of Flickr Users.
	- numHashtags: number of Hashtags.

## Running the tests

To run our experiments follow these steps:

- In 'config.properties' set:
	* numInactiveTwitterUsers: 10000, 21000 or 44000.
	* numInfluencerTwitterUsers: 5.
	* numActiveTwitterUsers: 1000, 2100 or 4400.
	* numFlickrUsers: 10000, 21000 or 44000.
	* numHashtags: 100.
- Right click on Main.java file on 'TwitterFlickr' project located on src: Run as -> Java Application.

It is necessary to wait some minutes until the graph is created. Once the graph creation is completed, 5 execution time results will be shown on the console for each query. To obtain results from Table 3 we have calculated the mean with the last 3 results for each query.

Note that in cases where configuration has 21000 and 44000 TwitterUsers it is possible that machines with specifications lower than 64GB RAM and 16 cores receive an OutOfMemoryError exception.

## Deployment

To export a jar file:

- Right Click on 'TwitterFlickr' project and select Export->Runnable JAR File->Next->Finish.
- Note that to run the jar file you have to copy 'config.properties' (of 'TwitterFlickr' project) file in the same folder as the jar.

## Built With

* [Apache Spark - Graphx tool](https://spark.apache.org/docs/latest/graphx-programming-guide.html) - The technology used.
* [Maven](https://maven.apache.org/) - Dependency Management.
* [Scala](https://www.scala-lang.org/) - Coding Language.


# Case 4 - TwitterFlickrStreamingDEMO Project

This is simply a DEMO of TwitterFlickr example CEP with Spark technology. 
First, this project creates an initial graph. Then, it starts a simulation of how our CEP architecture works, handling new edges and nodes and running the queries in an infinite loop.

For this artifact we have two projects:

- TwitterFlickr4Graphx: scala project with the source code.
- TwitterFlickr2: java project to export a jar file of the project.

## Getting Started

In the following we provide intructions on how to run this project. Please go to 'deployment' below for a description on how to deploy the project on a live system.

### Prerequisites

For running the project you will need:

- Internet connection.
- Scala IDE for Eclipse (our tests have been run with the version described at the beginning of this document).
- Java JDK 1.8.
- Scala version 2.11 - if your version is not this one, follow the instructions described in section 'Watch the Scala version' at the beginning of this document.


### Project Import and Configuration

To import the projects follow these steps:

1. Import project 'TwitterFlickr2' into workspace right clicking on Package Explorer of Eclipse and selecting Import->General->Existing Projects into Workspace.
2. Import project 'TwitterFlickr4Graphx' into workspace right clicking on Package Explorer of Eclipse and selecting Import->Maven->Existing Maven Projects.
3. Update maven dependencies right clicking on 'TwitterFlickr4Graphx' project and selecting Maven->Update project. If after this step there are still error dependencies, follow steps mentioned on 'Maven Dependencies Solutions' at the beginning of this document.

## Running the tests

To run the DEMO: right click on Main.java file on 'TwitterFlickr2' project located on src: Run as -> Java Application.

Results will be shown on the console. Once the initial graph creation is completed, execution times of queries, node handling and edge handling will be shown.

## Deployment

To export a jar file:

- Right Click on 'TwitterFlickr' project and select Export->Runnable JAR File->Next->Finish.
- Note that to run the jar file you have to copy 'config.properties' (of 'TwitterFlickr' project) file in the same folder as the jar.

## Built With

* [Apache Spark - Graphx tool](https://spark.apache.org/docs/latest/graphx-programming-guide.html) - The technology used.
* [Maven](https://maven.apache.org/) - Dependency Management.
* [Scala](https://www.scala-lang.org/) - Coding Language.

# Authors

Gala Barquero, Loli Burgueño, Javier Troya and Antonio Vallecillo.

# References

[1] Gala Barquero, Loli Burgueño, Javier Troya, Antonio Vallecillo: Extending Complex Event Processing to Graph-structured Information. In Proc. of the ACM/IEEE 21th International Conference on Model Driven Engineering Languages and Systems 2018 (MODELS 2018). Copenhagen, Denmark, October 2015. 
