#Logging and Troubleshooting

Goals

  * Tail logs of running application

  * Download log files

  * View application events

Steps

  1. View the aggregated logs for the application:

    * `cf logs <app-name>`

    * Alternatively, redirect standard out to a file and open in a text viewer for easier reading:

    *  `cf logs <app-name> cf-logs.txt && more cf-logs.txt`

  2. View the failure events for the application:

    * `cf events`

  3. scp the log files to your local filesystem for viewing / archiving:

    * Check to see if ssh is enabled (it is disabled by default in PWS).

      * `cf ssh-enabled cf-workshop-spring-mvc`

    * Enable ssh

      * `cf ssh-enable cf-workshop-spring-mvc`

    * Ssh to the app container via "cf ssh" then exit.

      * `cf ssh cf-workshop-spring-mvc`

    * Get a one-time password for ssh

      * `cf ssh-code cf-workshop-spring-mvc`

    * Get the Global Unique Identifier for your app

      * `cf app cf-workshop-spring-mvc --guid`

    * Scp the remote file `staging_info.yml` to your host.  

      * `scp -p 2222 -o User=cf:<app-guid>/0 ssh.run.pivotal.io:staging_info.yml staging_info.yml`

