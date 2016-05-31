# Ruby on Rails Tutorial: sample application

This is the sample application for [*Ruby on Rails Tutorial: Learn Rails by Example*](http://railstutorial.org/) by [Michael Hartl](http://michaelhartl.com/).

This sample has been modified to run on Cloud Foundry. The `cf-autoconfig` gem was added to enable auto-configuration of database connections as described in the [Cloud Foundry documentation](http://docs.cloudfoundry.com/docs/using/services/ruby-service-bindings.html). The `pg` gem was also added to support connection to PostgreSQL database. 

## Running the application on Cloud Foundry

After installing in the 'cf' [command-line interface for Cloud Foundry](http://docs.cloudfoundry.org/devguide/installcf/),
targeting a Cloud Foundry instance, and logging in, the application can be pushed using these commands:

First, view a list of services and plans available in your Cloud Foundry instance: 

~~~
$ cf marketplace
Getting services from marketplace
OK

service          plans                                                                 description
blazemeter       free-tier, basic1kmr, pro5kmr, pp10kmr, hv40kmr                       The JMeter Load Testing Cloud
cleardb          spark, boost, amp, shock                                              Highly available MySQL for your Apps.
cloudamqp        lemur, tiger, bunny, rabbit, panda                                    Managed HA RabbitMQ servers in the cloud
cloudforge       free, standard, pro                                                   Development Tools In The Cloud
elephantsql      turtle, panda, hippo, elephant                                        PostgreSQL as a Service
ironmq           pro_platinum, pro_gold, large, medium, small, pro_silver              Powerful Durable Message Queueing Service
ironworker       large, pro_gold, pro_platinum, pro_silver, small, medium              Scalable Background and Async Processing
loadimpact       lifree, li100, li500, li1000                                          Automated and on-demand performance testing
memcachedcloud   25mb, 100mb, 250mb, 500mb, 1gb, 2-5gb, 5gb                            Enterprise-Class Memcached for Developers
mongolab         sandbox                                                               Fully-managed MongoDB-as-a-Service
newrelic         standard                                                              Manage and monitor your apps
rediscloud       25mb, 100mb, 250mb, 500mb, 1gb, 2-5gb, 5gb, 10gb, 50gb                Enterprise-Class Redis for Developers
searchify        small, plus, pro                                                      Custom search you control
searchly         small, micro, professional, advanced, starter, business, enterprise   Search Made Simple. Powered-by ElasticSearch
sendgrid         free, bronze, silver, gold, platinum                                  Email Delivery. Simplified.
~~~

Choose a PostgreSQL service from the list and create a service instance named `rails-postgres` using a PostgreSQL service and plan: 

~~~
$ cf create-service SERVICE PLAN rails-postgres
Creating service rails-postgres
OK
~~~

Now push the application: 

~~~
$ cf push APP-NAME --random-route
Using manifest file manifest.yml

Updating app rails-sample
OK

Creating route rails-sample-desiccative-acetylizer.cfapps.io...
OK

Binding rails-sample-desiccative-acetylizer.cfapps.io to rails-sample...
OK

Uploading rails-sample...
Uploading app files from: rails_sample_app
Uploading 41.1M, 6349 files
OK
Binding service rails-postgres to app rails-sample
OK

Starting app rails-sample
OK
...

0 of 1 instances running, 1 starting
0 of 1 instances running, 1 starting
0 of 1 instances running, 1 starting
1 of 1 instances running

App started

Showing health and status for app rails-sample
OK

requested state: started
instances: 1/1
usage: 256M x 1 instances
urls: rails-sample-desiccative-acetylizer.cfapps.io

     state     since                    cpu    memory          disk
#0   running   2014-05-29 03:34:22 PM   0.0%   50.3M of 256M   80.2M of 1G
~~~

The application will be pushed using settings in the provided `manifest.yml` file. The `--random-route` option adds random
words in the host to make sure the URL for the app is unique in the Cloud Foundry environment. The output of the
`cf push` command shows the URL that was assigned. Using the provided URL you can browse to the running application.
