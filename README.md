# aqcu-tss-report


[![Build Status](https://travis-ci.org/USGS-CIDA/aqcu-tss-report.svg?branch=master)](https://travis-ci.org/USGS-CIDA/aqcu-tss-report) [![Coverage Status](https://coveralls.io/repos/github/USGS-CIDA/aqcu-tss-report/badge.svg?branch=master)](https://coveralls.io/github/USGS-CIDA/aqcu-tss-report?branch=master)

## Aquarius Customization - Time Series Summary Report

This report provides a tabular and interactive summary of all actions applied to a selected time series. 

It is built as a Docker container.

Configured functionality includes:

- **Swagger API Documentation** https://localhost:7501/swagger-ui.html

## Running the Application

This application can be run locally using the docker container built during the build process or by directly building and running the application JAR. The included `docker-compose` file has 3 profiles to choose from when running the application locally:

1. aqcu-tss-report: This is the default profile which runs the application as it would be in our cloud environment. This is not recommended for local development as it makes configuring connections to other services running locally on your machine more difficult.
2. aqcu-tss-report-local-dev: This is the profile which runs the application as it would be in the aqcu-local-dev project, and is configured to make it easy to replace the aqcu-tss-report instance in the local-dev project with this instance. It is run the same as the `aqcu-tss-report` profile, except it uses the docker host network driver.
3. aqcu-tss-report-debug: This is the profile which runs the application exactly the same as `aqcu-tss-report-local-dev` but also enables remote debugging for the application and opens up port 8000 into the container for that purpose.

Before any of these options are able to be run you must also generate certificates for this application to serve using the `create_certificates` script in the `docker/certificates` directory. Additionally, this service must be able to connect to a running instance of Water Auth when starting, and it is recommended that you use the Water Auth instance from the `aqcu-local-dev` project to accomplish this. In order for this application to communicate with any downstream services that it must call, including Water Auth, you must also place the certificates that are being served by those services into the `docker/certificates/import_certs` directory to be imported into the Java TrustStore of the running container.

To build and run the application after completing the above steps you can run: `docker-compose up --build {profile}`, replacing `{profile}` with one of the options listed above.
