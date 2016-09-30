# OpenResty Reverse Proxy

This playbook was written to provide a quick proxy to a downstream service using OpenResty. The proxy had to hide the downstream headers by 
rewriting or removing headers and also provide multiple HTTP Basic Auth credentials to clients whilst sharing one set of credentials
when calling the other service.

It provides examples of;
* Installing OpenResty by building from source on the remote machines
* Setting up HTTP basic auth
* Removing headers with OpenResty

# Run
~~~
$  ansible-playbook -i <your inventory file> playbooks/openresty.yml
~~~

# Adding additional credentials
Add a new element to the list in playbooks/openresty.yml


# Testing
The following two commands should be equivalent;
~~~
$ curl -i https://yourdomain.com/test \
	-X PUT \
	-u XXXXXXXXXX:YYYYYYYYY \
	-H 'Content-Type:application/json' \
	-d '{"key": "value"}'
~~~

~~~
$ curl -i 'https://otherservice.com/test' \
	-X PUT \
	-u username:password  
	-H "Content-Type: application/json"
	-d '{"key": "value"}'	
~~~

