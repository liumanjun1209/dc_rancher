# KatrinaBI（SpagoBI商业定制版）


### Info:

 This template will install KatrinaBI（SpagoBI商业定制版）.
 
### Using

The only one environment property used by SpagoBI is:

* PUBLIC_ADDRESS : optional - define the IP Host of SpagoBI visible from outside the container (eg. http://$PUBLIC_ADDRESS:8080/SpagoBI), the url's host part of SpagoBI url. If not present (like the above examples) the default value is the IP of container. You can use the IP of virtual machine (in OSX or Windows environment) or localhost if you map the container's port.
* Get the IP of container :$ docker inspect --format '{{ .NetworkSettings.IPAddress }}' spagobi
* Open SpagoBI on your browser at url (use your container-ip):container-ip:8080/SpagoBI
* If you run the host with a Virtual Machine (for example in a Mac environment) then you can route the traffic directly to the container from you localhost using route command:
$ sudo route -n add 172.17.0.0/16 ip-of-host-Virtual-Machine





