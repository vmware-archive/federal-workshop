Goals

  * Configure Oracle as a User-Defined Service

  * Bind the Oracle service

  * Start application and use service

*Pre-requisite*

  1.	Stop all of your running applications in PWS

  2.	Obtain information about Oracle service from your instructor.  This will take the form of

    * `oracle://<uid>:<pwd>@<host>:<port>/<db>`

Steps

  1. Create the Oracle service.  Note that "cups" is short for "create user provided service."  The '-p "uri"' tells the cf CLI that we will be passing a parameter called uri as input

    * `cf cups oracle-db –p 'uri'`

    * `uri>oracle://<username>:<password>@<host>:<port>/<db>`

  2. Using a text editor, update the manifest file – change “${random-word}” to your first initial + lastname (i.e. the “host” line in the manifest file should read:”host: spring-music-jsmith” if your name is John Smith)

  3. Push the app to Cloud Foundry

    *  `cf push spring-music`

  4. Bind the Oracle service to the deployed application

    * `cf bind-service spring-music oracle-db`

  5. Restart the application to utilize the service.

    * `cf restart spring-music`

  6. After application restarts open a browser and navigate to the application.  The path to the application is supplied in a message similar to the following: `urls: spring-music-mdolan.cfapps.io`

  7. Mouse over the “i" in the header to confirm your service configuration
 
    * Mousing over will show the connected services (in this case oracle-db)

    * [Confirm Spring Music Datasource](images/header-confirm.png)
 
  8. Stop your spring music application

    * `cf stop spring-music`

