This repository contains a Postman collection for testing the comment functionality of the social application's API. Below are instructions on how to run the tests, along with insights into the testing approach and potential expansions.


# Instructions to Run Tests

## Prerequisites

### 1. Postman Installation: 

- Make sure you have [Postman](https://www.postman.com/downloads/) installed on your machine.

### 2. JSON Server Setup:

- Firstly, ensure you have __NodeJs__ and __NPM__ installed. Further instructions can be found [here](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm).
- Install [JSON Server](https://github.com/typicode/json-server#getting-started) to simulate the REST API responses.

__Please Note:__ The latest alpha version of the josn-server has issues (further details can be found in the technical challenges section), so in order to avoid that, please install the last stable version. We have installed ```0.17.4```.
We recommend installing all the dependencies in an isolated environment.
``` npm install json-server@0.17.4 ```
Alternatively, you can also install the json-server globally using:
``` npm install -g json-server@0.17.4 ```

### 3. Seeding the Database File 

The database file is already included in the repo. There are multiple ways to generate the db.json file. 

1. Save the response from ```https://jsonplaceholder.typicode.com/db``` as a json file.
2. Download the db.json from their github repo ```https://github.com/typicode/jsonplaceholder/blob/master/data.json```.
3. Use the [seed.js](https://github.com/typicode/jsonplaceholder/blob/master/seed.js) to generate the db.json (This option provides the most customization as you can choose to omit some resources).

__Disclaimer:__ To use seed.js, you need to install extra dependencies, please refer to instructions on jsonplaceholder's [github](https://github.com/typicode/jsonplaceholder/tree/master). 


## Running the Tests

### 1. Clone the Repository:

- Run the following commands in your terminal. 
```git clone https://github.com/ShaistaAbbasi/talonone-takehome-task.git```
```cd talonone-takehome-task```

### 2. Running the Json-Server:

- Run the below command to start the JSON Server with the provided data file.
For local environemnt use:
```npx json-server --watch db.json``` 
For global environment use:
```json-server --watch db.json``` 

### 3. Import Postman Collection:

- Run Postman.
- Being in the Collections tab, click on "Import" and select the SocialAppCollection.json file from the repository.
- Navigate to the Environment tab from left panel, click on "Import" and select the SocialAppEnvironment.json file.

### 4. Set Environment Variables:

- In the imported localhost environment, update the baseUrl variable to the address of your JSON Server (for us it's http://localhost:3000).

### 5. Run the Collection:

- Select the imported environment __Localhost__ in the top right corner. 
- Select the imported collection __Social App Comment Functionality__, click on the ```...``` and select __Run collection__.
- Make sure to provide a delay time before running the collection of atleast ```300 ms```, to avoid 'socket hang up' errors. 

### 6. Failing Cases:

- After the test run finishes, there will be 4 failing tests. All these 4 tests should have passed, it seems that there is no server side logic to handle these cases. I have added ```(Does not work)``` next to the test to indicate the failure is expected. 


# HTML Test Reports

For better visualisation of the test results, I have included an HTML test report using the newman cli tool. This can be replicated by installing [newman](https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman/) and the [htmlextra plugin](https://www.npmjs.com/package/newman-reporter-htmlextra) for HTML reports.

- Navigate to the __HTML_report_and_screenshot__ folder, it contains an HTML report created by the newman cli tool. View that report for the proof of test execution. The following command has been used to generate the newman HTML report.
```newman run SocialAppCollection.json -e SocialAppEnvironment.json --delay-request 300 --reporters cli,htmlextra``` 
- This folder also contains a screenshot for the test run in cli. But the HTML report could give you a better and detailed view for the test execution. 


# Approach to the Assignment

## What I Chose to Test and Why

The tests focus on the comment functionality of the social application's API. The postman collection contains two main folders __Positive__ and __Negative__. Each folder contain subfolders, where each represents a scenarios and is independent, hence can be executed on its own. 

### The positive test cases mainly include:

- Creating, editing, and deleting comments, because we need to make sure the basic comment functionality has been implemented correctly. 
- Integration between posts and comments, as posts and comments have a one-to-many relationship. In order for the app to function properly, the association between posts and comments should be properly handled and tested. 
- Regression checks for the posts, to ensure the new comment functionality does not break the post functionality.

### Negative test cases include:

- Tests for invalid request body or url.
- Some of the tests are failing, because they are not being handled correctly on the server side. These tests are marked with __Does not work__ .


## How Else I Might Have Done Things 

- One alternate approach would be to consider using data-driven testing to cover a wider range of scenarios. For example, create a data file (CSV or JSON) with different combinations of input data and expected outcomes.
- The tests could have been further divided into feature, integration and regression test folders. 
- I found the json-server mock tool to be very limited in terms of replicating a production ready API. I would have preferred having access to an actual production ready API endpoint.  


## Future Test Expansions

In the future, these tests can be expanded to cover:

- Performance Tests.
- Security Tests.
- Exception/error handling for different types of failures.
- Integrating the API tests into CI/CD pipeline to automatically run tests upon code changes.


## Technical Challenges 

## Json-Server Installation

The command to install the json-server ```npm install json-server``` automatically installs the latest alpha version, the resource linking logic is this version is completely broken. Downgrading the json-server version to 0.17.4 fixed the issue.










