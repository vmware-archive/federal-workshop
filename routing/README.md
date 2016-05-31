Goals

* Deploy application
* Map a new URL Subdomain to the application

Steps

1. Get information about deployed app using CLI command

* `cf apps`

* Note the deployed application name.

2. Map a new URL to the application 

* `cf map-route <app_name> cfapps.io –n <app_name>-new`
* Where <app_name> is the app name recorded in step 1.  
	
![Mapping an app route in PCF](images/cf-map-route.png)

3. Verify the new URL route was created in the space.  You should see the new host domain combination listed

* `cf routes`

![Listing Routes in PCF](images/cf-routes.png)

4. Open a browser and navigate to the application using the new URL route.

5. Unmap the new URL to the application 

* `cf unmap-route <app_name> cfapps.io –n <app_name>-new`
* Where `<app_name>` is the app name recorded in step 1.  

![Un-mapping an app route in PCF](images/cf-unmap-route.png)
 
6.List the routes for the space

* `cf routes`
 
* The route still exists because we have unmapped the route, but not deleted the route, so it is reserved for our future use.

![Listing Routes in PCF](images/cf-routes-2.png)

7.Attempt to map a route to a reserved URL 

`cf map-route <app_name> cfapps.io –n cfworkshop-reserved`

* You will see this fails as this has already been reserved.
 
![Reserved Routes in PCF](images/cf-route-reserved.png)

8. Delete the route (this will also unmap the route)

`cf delete-route cfapps.io –n <app_name>-new`

* When prompted confirm you want to delete the route.  

![Delete Routes in PCF](images/cf-delete-route.png)
 
9. Verify the route has been deleted

* `cf routes`

