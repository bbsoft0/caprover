### CapRover - Full Steps to install Sample Apps
Only the sample apps were updated. All the other caprover files were untouched.


### Version 1.0     Ruby_complex deployed
- Deploy and run a complex rails application in minutes. This includes configurations, sending code to server, builds, getting an SSL certificate, install it, update nginx, running caprover definition file.
- Generic Caprover definition file which covers most rails apps
- Detailed explanations of every action on caporover UI and bash
- Example was taken from Active Admin with full data
https://github.com/activeadmin/demo.activeadmin.info

## Learn More!

For more details and documentation, please visit https://CapRover.com/



___




### Deploy admin app - FULL STEPS :

Create a new droplet (could be DigitalOcean or other host)

Install caprover on it, go to UI and upgrade Caprover, then add the domain (as instructed in docs)

Add first postgres as a single click app. Full name : postgres-db

Create a new app : Full name : admin

Inside the app admin, go to App Configs and add these 2 Environmental Variables:

SECRET_KEY_BASE							anything

RAILS_SERVE_STATIC_FILES				true

DOMAIN									admin.[domain]

Inside the app admin, go to Deployment and with method 2 deploy the ruby_complex.tar file

SSH to the server and run this 2 bash commands:

- `sudo docker exec -ti $(docker container ls --filter name=srv-captain--run | awk 'FNR == 2 {print $1}') rake db:migrate`

- `sudo docker exec -ti $(docker container ls --filter name=srv-captain--run | awk 'FNR == 2 {print $1}') rails db:seed`




___



### Deploy pghero - FULL STEPS :

In caprover, create a new app - pghero, make sure persistent checkbox is selected

In container HTTP Port, set 3005

In AppConfigs, Environment Variables set the following:

DATABASE_URL	postgres://demo_aa:demo_aa@srv-captain--postgres-db:5432/demo_aa_development

PORT			3005

RAILS_LOG_TO_STDOUT		disabled

You should ssh to droplet and set the ufw to allow port

- `sudo ufw allow 3005`

Inside the app pghero, go to Deployment and with method 5 deploy this captain-definition file :

- `{
 "schemaVersion" :2 ,
   "imageName" : "ankane/pghero"
}
`

After instalation, postgres.conf can be found and edited at 
/var/lib/docker/volumes/captain--postgres-db-data/_data
