#pcf-ers-demo on concourse

![](images/pipeline.png)

* [Concourse](http://councourse.ci)
* Build only once and deploy anywhere
* Every build is a release candidate
* Every build step runs inside a docker container mounting to garden linux cells

## Resources

Resources in concourse are implemented as docker images which contain implementations corresponding their types

* git-repo ([git-resource](https://github.com/concourse/git-resource)): A Github repo. E.g. pcf-ers-demo Github resource

* version ([semver-resource](https://github.com/concourse/semver-resource)): A file to track the version stored in Github. E.g. 1.0.1 in a file named as current-version

* release-candidate (([github-resource](https://github.com/concourse/github-release-resource))) Store pcf-ers-demo artifact E.g. pcf-ers-demo-1.0.1-rc1.jar

* production-release (([github-resource](https://github.com/concourse/github-release-resource))) Store pcf-ers-demo artifact E.g. pcf-ers-demo-1.0.1.jar

## Pipeline Progress

### Check out from the git-repo

### Unit testing pcf-ers-demo

This step runs on a container with maven and java installed.
Basically it just runs "./mvnw test" against the git-repo

### build-artifact

* git-repo - Check out the same source version of git-repo as unit step
* version - Checkout the version file from Github
* "./mvnw install" generates the jar artifact
* Push the artifact to the Github resource as music-resource
* Git tag on the git-repo
* Bump the version resource for the next usage

### integration-tests

* Pull the binary from release-candidate
* Deploy to cloudfoundry acceptance tests space
* Run Automation Acceptance Tests suite

### promote-to-uat

* Pull the binary from release-candidate
* Deploy to cloudfoundry uat space
* Waiting for user acceptance tests

### manual-deploy-to-prod

* Manually trigger the build when the operators are ready
* Pull the binary from release-candidate and rename
* Deploy to prod
* Copy to Github release as production-release

### How to replicate this pipeline in your env

* If you don't already have a Concourse environment, you can quickly spin one up locally with [Vagrant](https://concourse.ci/vagrant.html])

* Download the `fly` CLI by visiting `http://192.168.100.4:8080` and selecting your OS then install

* Fork this github repo to your own github account, [ generate the key pair and add the public key to github ](https://help.github.com/articles/generating-ssh-keys/), and save the private key for future usage.


* Install PCF Dev ([Vagrant VM](http://pivotal.io/pcf-dev))
 * Setup spaces for development, test, uat and production
  * `cf create-space development`
  * `cf create-space test`
  * `cf create-space uat`
  * `cf create-space production`


* Set your fly endpoint (assuming you are taking the easy way and using vagrant)

  * `fly -t lite login -c http://192.168.100.4:8080`

  * Configure your environment details in pcf-ers-demo-credentials.yml

  * `fly -t lite set-pipeline -p pcf-ers-demo -c ci/pipeline.yml -l pcf-ers-demo-credentials.yml`
  * `fly -t lite unpause-pipeline -p pcf-ers-demo`
  * Open `http://192.168.100.4:8080` in your browser and enjoy!

###  __FYI DO NOT COMMIT `pcf-ers-demo-credentials.yml` as it has all your secrets__
