Goals
* Create a managed service instance 
* Push application using CLI prompts
* Access deployed applications
 
Steps

1. Create a Postgres Database instance for the Ruby on Rails application.  

  * We are telling the cf CLI that we want to create a service (“cs”).  The type of service is “elephantsql”, a vendor in the PWS marketplace offering a Postgres database as a service.  The service plan is “turtle” – the free tier offered by this vendor.  The name of the service is “rails-postgres.”

  * `cf cs elephantsql turtle rails-postgres`
 
2.  Now push the application to PWS.  

  * In this case, we are creating a “random-route” – asking CF to create a uri with 2 random words used for accessing the application.

  * `cf push rails-sample-app --random-route`

3.  Now view the application in a browser.  The result of the cf push will tell you the URL to use (see the urls parameter).
 
  ![Output from cf push cmd](images/cf-push.png)


