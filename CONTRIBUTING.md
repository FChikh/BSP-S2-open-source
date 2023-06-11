# Contributing to Energy4Life

Thank you for considering contributing to Energy4Life! This document outlines the guidelines for contributing to the project, including how to report bugs, suggest improvements, and submit code changes. 

Please note that by contributing to this project, you are agreeing to the terms set out in the Contributor License Agreement (CLA). Before submitting any contributions, please make sure to sign the CLA. 

## Bug Reports

### Where to Find Known Issues
We are using GitHub Issues for our public bugs. We keep a close eye on this and try to make it clear when we have an internal fix in progress. Before filing a new task, try to make sure your problem doesn’t already exist.

### Reporting New Issues
If you encounter any bugs or issues with the Energy4Life website, please submit a detailed bug report. Your report should include the following information:

- Steps to reproduce the bug
- Expected behavior
- Actual behavior
- Error messages (if any)
- Screenshots (if applicable)

Bug reports should be submitted via the Issues tab on the Energy4Life GitHub repository.

## Feature Requests

If you have an idea for a new feature or improvement to the Energy4Life website, please submit a feature request. Your request should include the following information:

- Description of the new feature or improvement
- Rationale for why the feature or improvement is needed
- Any relevant use cases or examples
- Any potential drawbacks or limitations

Feature requests should be submitted via the Issues tab on the Energy4Life GitHub repository.

## Branch Organization

Submit all changes directly to the main branch. We don’t use separate branches for development or for upcoming releases. We do our best to keep main in good shape, with all tests passing.

Code that lands in main must be compatible with the latest stable release. It may contain additional features, but no breaking changes. We should be able to release a new minor version from the tip of main at any time.

## Contributing Code

If you would like to contribute code to the Energy4Life website, please follow these steps:

1. Fork the Energy4Life repository on GitHub
2. Clone your forked repository to your local machine
3. Make your changes in fork version, directly to the main branch. We don’t use separate branches for development or for upcoming releases. We do our best to keep main in good shape, with all tests passing.
4. Any significant changes should be accompanied by tests. The project already
     has good test coverage, so look at some existing tests if you're unsure
     how to go about it.
5. All contributions must be licensed AGPL v3 and all files must have a
     copy of the boilerplate license comment (can be copied from an existing
     file).
6. Submit a pull request to the main Energy4Life repository

Before submitting a pull request, please make sure to run the code through our Continuous Integration (CI) tools to ensure that all tests pass and the code meets our standards.

## Prerequisites

### Softwares

- `java jdk 8+`
- `Intellij IDEA 11.0.6` 
- `mysql 8.0.21`

## Guidelines
 
### Backend

- For the API server, it is easy to set up, debug, and run in Intellij IDEA. It has inbuilt plugins to build gradle software 

- Then setup your JDK. For example, to set up JDK 1.8, go to File -> Project Structure -> Project -> select 1.8 java version. 
Also, in the same path, File -> Project Structure -> SDKs -> select 1.8

- Before running the application create the database named “e4l” in MySQL and check whether the MySQL server is ON.
  - TODO: create dev-env using either Vagrant or Docker to have same versions than in prod-env.
 
- Specify database location and credentials in config file ([more info](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-connect-to-production-database))
  <!-- - config file ([src/main/java/resources/application.properties](src/main/java/resources/application.properties))  
  ```
  spring.datasource.url= jdbc:mysql://localhost:3306/e4l
  spring.datasource.username= root
  spring.datasource.password= 12345678 
  ```
  Note: Give your username and password if you have a different one
  
  These location configuration of the API server should not be pushed into the remote repository as these are only the local changes. -->

- To run or debug the application just run (or debug) Main.java
  
- To run test cases and build the product, just right click on the project and run the test cases

- Note that for every change in the server-side code, we have to build and run the server again so that the corresponding changes will be updated in the server
  
- .idea files which are created in Intellij should not be pushed into the remote repository as this is not related to the project

- After commit and push your changes, check whether the pipeline run gets passed. If it fails, try to fix it before push anything to the repository

#### Project funtionalities

- From the front-end, the questionnaire is first fetched with the API URI- “/questionnaire” using a GET call

- On selecting the answer for any question, a POST api request is made to “/calculate/energyConsumption” to get the energy consumed for that selected answer

- Once the user finishes the request, a POST request is sent to “/session” along with all selected answers. There, the answers are all stored in the server. It then sends a session ID which is the key to retrieve the same session again

- To retrieve the result for the session, a GET request is made to “/calculate/session/{sessionId}” with proper session ID

- For sending mail in “Contact Us” form, a POST request is made to “/send” along with all the data

#### Configuration parameters
Configuration options are specified in [src/main/java/resources/application.properties](src/main/java/resources/application.properties) file  

- `spring.jpa.hibernate.ddl-auto`  
Specifies DB initialisation strategy: update (tries to update the existing schema), create (on each launch drops the existing schema and creates a new one)  
[more information](https://docs.spring.io/spring-boot/docs/current/reference/html/howto-database-initialization.html)

- `jwt.secret`  
Secret key to sign jwtokens.  
Note: If the application runs with multiple instances (vertical scaling), each instance should have the same key to avoid authorization issues.  

- `jwt.expiration-time`  
Validity time of a jwtoken in ms (1000 ms = 1 second).

- `signature.key`  
Secret key to sign objects (id of a result).  
Note: If the application runs with multiple instances (vertical scaling), each instance should have the same key.  

- `admin.email` and `admin.password`
The admin user credentials. The only way to create an admin user.  

- `resources.static.url`
The public URL of a static resources (images, pdfs)  

[more info on spring config](https://docs.spring.io/spring-boot/docs/current/reference/html/howto-properties-and-configuration.html)

### Frontend

- The server is written in React with Redux design pattern. Axios is mainly used to make the API calls

- A simple example for action, reducer and container can be understood in the following commit [Example commit](https://minsky.uni.lu/gitlab/e4l/lu.uni.e4l.platform.frontend.dev/-/commit/74a2a5e538254a4b1628cda687aba26fe21701a6)

- The following change should be done in .env file to have it working on localhost
    ```
       API_URL=http://localhost:8080/e4lapi
    ```
    This change should not be pushed into the repository as these are only the local changes.

- Run the following command in the `app` folder. 
    ```
       npm i && npm start
    ```
- To see the Redux states in the browser you can install a handy extension named “Redux dev tools” in chrome web browser. To configure that plugin in our code, uncomment the following line in store.js

    ```
    export const store = createStore(
      reducer,
      compose(
        applyMiddleware(changeLang, promise(), createLogger())
        window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
      )
    );
    ```
    This change should not be pushed into the remote repo.
    
- Once uncommented and the server is started again, the action dispatched and the states can be viewed by right clicking the browser > Inspect > Redux tab > state

- This tool is very useful for debugging our react-redux code. Every action dispatched and its corresponding state change and the response received in the action could be viewed in this tool
  
- If any new dependencies installed using npm, it will be stored in package.json and package-lock.json. So, these files should also be committed and pushed into the remote repo

- .idea file should not be pushed into the remote repo as this is not related to our project

- After commit and push your modifications, check whether the pipeline run gets passed. If not, try to fix it before push anything into remote repo


 Note: For every questions in the survey, you may find `info` button which shows the information related to the corresponding question as a popup.
 As of now, it is given as a pdf file. Below is a simple example to make it as a HTML page. Do the changes as below for all the questions in question.js.
 ```
- Get the question name by iterating calculationResult.breakdown using 'for' loop
- By using if-else condition, give the html content for the corresponding question as below.

Example:

if(calculationResult.breakdown[i].question == "question name")
return(
.........
.........
<Modal.Body>
    <h4 style={{textAlign: "center"}}>Electricity and heating consumption: Where do you live?</h4>
    <p><b>Electricity consumption at home: </b></p>
    <p style={{textAlign: "left", fontSize: 14}}>The energy needed for electricity was computed from real data of 44 luxembourgish households. The data are anonymous and were divided into three categories depending on the habitable surface:
    households with 100 m<sup>2</sup> or less were considered as apartments, households with 100-200 m<sup>2</sup> surface were considered row houses and households with above 200 m<sup>2</sup> surface were considered free-standing houses. Thus we get: </p>
</Modal.Body>
.........
)
 ```


## Code Style

The Energy4Life website is built on Java Spring and ReactJS. We follow the coding standards set out by the Java and ReactJS communities, respectively. 

- Java code should be formatted using the Google Java Style Guide
- ReactJS code should be formatted using the Prettier code formatter

## License
By contributing to Energy4Life (e4l), you agree that your contributions will be licensed under its [AGPL v3 license][].

[AGPL v3 license]: https://www.gnu.org/licenses/agpl-3.0.en.html

## Contributor License Agreement

Contributions to Energy4Life project must be accompanied by a Contributor
License Agreement. This is not a copyright _assignment_; it simply gives
us permission to use and redistribute your contributions as part of the
project.

You generally only need to submit a CLA once, so if you've already submitted
one (even if it was for a different project), you probably don't need to do it
again.

## Conclusion

Thank you for your interest in contributing to Energy4Life! We value all contributions, big and small. If you have any questions or concerns, please don't hesitate to reach out to us via the Issues tab on the Energy4Life GitHub repository.


## Your First Pull Request
Working on your first Pull Request? You can learn how from this free video series:

[How to Contribute to an Open Source Project on GitHub][]

[How to Contribute to an Open Source Project on GitHub]: https://egghead.io/courses/how-to-contribute-to-an-open-source-project-on-github


