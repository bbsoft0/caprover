### CapRover - Full Steps to install Sample Apps


### Rails complex deploy
- Deploy and run a complex rails application in minutes. This includes configurations, sending code to server, builds, getting an SSL certificate, install it, update nginx, running caprover definition file.
- Generic Caprover definition file which covers most rails apps
- Detailed explanations of every action on caporover UI and bash
- Example was taken from Active Admin with full data
https://github.com/activeadmin/demo.activeadmin.info

## Learn More!

For more details and documentation, please visit https://CapRover.com/

## Open Source

Only the sample apps were updated. All the other caprover files were untouched.



### Rails complex deploy Steps :

Create a new droplet (could be DigitalOcean or other host)

Install caprover on it and add the domain (as instructed in docs)

Add first postgres as a single click app. Full name : postgres-db

Create a new app : Full name : run

Inside the app run, go to App Configs and add these 2 Environmental Variables:

SECRET_KEY_BASE			anything

SECRET_KEY_BASE			true

Inside the app run, go to Deployment and with method 2 deploy the ruby_complex.tar file

SSH to the server and run this 2 bash commands:

- `sudo docker exec -ti $(docker container ls --filter name=srv-captain--run | awk 'FNR == 2 {print $1}') rake db:migrate`

- `sudo docker exec -ti $(docker container ls --filter name=srv-captain--run | awk 'FNR == 2 {print $1}') rails db:seed`
