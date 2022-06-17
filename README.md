<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/Suracki/Mediscreen">
    <img src="/logomin.png" alt="Logo">
  </a>

<h3 align="center">Mediscreen Application</h3>

  <p align="center">
    Mediscreen Patient Demographics application.
    <br>
    Application provides functionality to store Patient Demographic data, Patient History (Notes), and generate Diabetes Risk Assessments.

  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li><a href="#getting-started">Getting Started</a>
		<ul>
        <li><a href="#installation">Installation</a></li>
		</ul>
	</li>
    <li><a href="#usage">Usage</a>
		<ul>
        <li><a href="#front-end">Front End</a></li>
		<li><a href="#api">API</a></li>
		</ul>
	</li>
	<li><a href="#architechture-diagram">Architechture Diagram</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

This is the completed Mediscreen application, consisting of 3 microservices and 2 databases.
<br><br>
This repository contains all of the completed applications, along with their Dockerfiles, and a docker-compose.yml which will create a container with the microservices and their databases.
<br><br>
For additional details on the development process for each microservice, please refer to their individual repositories which contain a full commit and pull request history.
<br>
[Patient Demographics Microservice](https://github.com/Suracki/Mediscreen)
[Patient History Microservice](https://github.com/Suracki/MediscreenPatientHistory)
[Patient Assessment Microservice](https://github.com/Suracki/MediscreenPatientAssessment)
<br><br>

In addition to the font end pages, the application also provides REST API endpoints.
<p align="right">(<a href="#top">back to top</a>)</p>



### Built With

* [Java 11](https://www.oracle.com/java/technologies/javase/jdk11-archive-downloads.html)
* [Spring Boot](https://spring.io/projects/spring-boot)
* [Maven](https://maven.apache.org/)
* [Gson](https://github.com/google/gson)
* [RetroFit](https://square.github.io/retrofit/)
* [Thymeleaf](https://www.thymeleaf.org/)
* [Bootstrap](https://getbootstrap.com)


<p align="right">(<a href="#top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

### Installation
1. Clone the repo
   ```sh
   git clone https://github.com/suracki/mediscreenapplication.git
   ```
2. Set configuration variables in each microservice's `application.properties` as desired
	Some properties of note:
	/Mediscreen/ -> Patient Demographic Service
	```
   spring.datasource.url -> url of the MySQL database; examples included for IDE or Docker use, defaulted to Docker.
   docker.assessment.url -> url of the Patient Assessment microservice. Default is localhost:8282
   docker.history.url -> url of the Patient History Microservice. Default is localhost:8181
   ```
   /PatientHistory/ -> Patient History Service
	```
   spring.data.mongodb.host -> location of the Mongo database; examples included for IDE or Docker use, defaulted to Docker.
   docker.patient.ip -> ip of the Patient Demographic microservice. Default is mediscreenapp
   docker.patient.port -> port for Patient Demographic microservice. Default is 8080
   docker.patient.url -> url of the Patient Demographic Microservice. Default is localhost:8080
   ```
   /PatientAssessment/ -> Patient History Service
	```
   docker.patient.ip -> ip of the Patient Demographic microservice. Default is mediscreenapp
   docker.patient.port -> port for Patient Demographic microservice. Default is 8080
   docker.patient.url -> location of the Patient Demographic Microservice. Default is localhost:8080
   docker.history.ip -> ip of the Patient History microservice. Default is patienthistoryapp
   docker.history.port -> port for Patient History microservice. Default is 8181
   docker.history.url -> url of the Patient History Microservice. Default is localhost:8181
   trigger.terms.array -> terms used for determining risk
   ```
3. Start the application running in Docker
	Ensure that Docker is installed and running
	```
	https://docs.docker.com/get-docker/
	```
	Use the provided docker-compose.yml to build and start the application
	```
	docker-compose up -d
	```
3. Access the application via web browser
	Once the application is running it can be accessed via web browser
	```
	Default:
	https://localhost:8080
	```
	In addition, Adminer and MongoExpress are provided for additional database administration
	```
	Adminer:
	https://localhost:9000
	MongoExpress:
	https://localhost:9001
	```

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

### Front End

The application serves a Front End UI using Thymeleaf and Bootstrap, which can be accessed via the following URLs:

Navigation starting point:<br>
/ -> Home Page, welcome page with links to guide user through interface<br><br>
Patient Demographics:<br>
/patient/list -> List of all Patients currently stored in the system<br>
/patient/add -> UI for adding a new Patient to the system<br>
/patient/view/{id} -> UI to view details of a Patient in the system<br>
/patient/update/{id} -> UI to update details of a Patient in the system<br><br>
Patient History:<br>
/patient/note/list -> List of all PatientNotes currently stored in the system<br>
/patient/note/add -> UI for adding a new PatientNote to the system<br>
/patient/note/view/{id} -> UI to view details of a PatientNote in the system<br>
/patient/note/viewall/{id} -> UI to view all PatientNotes for a specific Patient<br>
/patient/note/update/{id} -> UI to update details of a PatientNote in the system<br><br>
Patient Assessment:<br>
/assessment/view/{id} -> Generate & View assessment for a specific patient<br>

### API

The application provides a REST API with the following endpoints<br><br>
Patient Demographics:<br>
/patient/api/add -> add a Patient to the system<br>
/patient/api/get/{id} -> get a Patient from the system<br>
/patient/api/update -> update a Patient in the system<br><br>
Patient History:<br>
/patient/note/api/add -> add a PatientNote to the system<br>
/patient/note/api/get/{id} -> get a PatientNote from the system<br>
/patient/note/api/getbypatient/{id} -> get all PatientNotes for one Patient<br>
/patient/note/api/update -> update a PatientNote in the system<br><br>
Patient Assessment:<br>
/assessment/api/get/{id} -> Generate & Get Assessment for a specific patient<br>

_For full details of API usage, please refer to the [API specification document](/REST%20API%20Specification.pdf)_

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- DESIGN -->
## Architechture Diagram

The services created by running the provided script will be set up like this:<br><br>

![Architechture Diagram](/architechture.png)


<p align="right">(<a href="#top">back to top</a>)</p>


<!-- CONTACT -->
## Contact

Simon Linford - simon.linford@gmail.com

Project Link: [https://github.com/Suracki/MediscreenApplication](https://github.com/Suracki/MediscreenApplication)

<p align="right">(<a href="#top">back to top</a>)</p>
