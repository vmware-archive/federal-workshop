Goals
* Login to PCF environment
* Push applications using CLI prompts
* Access deployed applications
 
Steps

1. Open a terminal window.

2. Clone the spring-mvc project repository

  * `git clone https://github.com/pivotal-cf-workshop/prebuilt-spring-mvc-app`

3. Using the CLI login to PWS using the user name and password for your cloud foundry account
 
  `* cf login -a api.run.pivotal.io`
 
   * Follow prompts to supply user name and password
 
4. Using the CLI push the built application
 
   * `cf push <app-name> -p dist/cf-workshop-spring-mvc-0.1.war`
 
   * Your app-name should be: `<first_initial><last_name>-CFW (e.g “jsmith-CFW”)`
 
5. After application deploys and starts open a browser and navigate to the application.  The path to the application is supplied in the “urls” parameter similar to the following:

  ![Sample Output](images/deploy-output.png)
 
6. Now we will deploy a Ruby on Rails application.  First, we will create a new directory, then change to it:

  * `> mkdir ~/lab2-ruby`
 
  * `> cd ~/lab2-ruby`
 

7. Clone from github

  * `git clone https://github.com/cloudfoundry-samples/rails_sample_app.git`
 
8. Now change to the rails sample application directory

  * `cd rails_sample_app`

9. Create a Postgres Database instance for the Ruby on Rails application.  We are telling the cf CLI that we want to create a service (“cs”).  The type of service is “elephantsql”, a vendor in the PWS marketplace offering a Postgres database as a service.  The service plan is “turtle” – the free tier offered by this vendor.  The name of the service is “rails-postgres.”

  * `cf cs elephantsql turtle rails-postgres`
 
10.  Now push the application to PWS.  In this case, we are creating a “random-route” – asking CF to create a uri with 2 random words used for accessing the application.

  * `cf push rails-sample-app --random-route`

11.  Now view the application in a browser.  The result of the cf push will tell you the URL to use (see the urls parameter).
 
![Output from cf push cmd](images/cf-push-output.png)


