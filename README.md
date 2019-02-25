# exe-sm


Application Engineer - Technical evaluation assignment
======================================================

## Requirements
For this assignment, the following will be provided for you:
  * 3 hosts with Ubuntu Linux 18.04 LTS
  * SSH private key
  * Public network on all 3 of the hosts
  * Private network on all 3 of the hosts

> ## Solution for setup of the hosts: Ansible
> 
>  * First look at the hosts reveals `python` is not installed on any of them, which is a prerequisite for Ansible to work, so we install it manually with ssh
>  * We achieve this rather ingeniously with  
>  `ssh ubuntu@52.29.209.228 "sudo apt-get -y install python"`  
>  `ssh ubuntu@52.58.152.245 "sudo apt-get -y install python"`  
>  `ssh ubuntu@54.93.249.52 "sudo apt-get -y install python"`  
> 
> In order to preserve good practices from the start, repeatability is key to sucess in a DevOps driven environment. 
> To guarantee this, Ansible is used to achieve the desired state of the servers.  
> 
> *Of course, another valid alternative would be puppet, but due to the higher
> infrastucture footprint (server, agent ...) and the one-off nature of the exercise, I´ve chosen Ansible*
> 
> All required data (inventory, playbooks...) for Ansible can be found in the "ansible" folder




## Techniques
During this assignment, you will be using the following techniques/knowledge:
  * Linux (https://www.ubuntu.com)
  * Apache/nginx (http://httpd.apache.org or https://nginx.org)
  * Load balancing
  * MySQL (https://www.mysql.com)
  * PHP (http://php.net)
  * Gearman (http://gearman.org)

## Assignment
Create a small webcluster of 3 hosts. One host will be installed as HTTP
loadbalancer. The other two webservers will run the HTTP webservers. One of the
backend servers will run a MySQL server and the other will run a Gearman job
server. Both backend servers will run a gearman worker with 2 gearman functions.

The gearman workers are identical and implement 2 functions; one function
is used to write data to the database, and one function is used to read data
from the database.

All HTTP requests should be balanced equally over the 2 webservers. The two
webservers should contain a PHP script which does 2 things. First it calls the
gearman function to write data to the database, and writes the hostname of
the server which is handling the web request, the date & time, and the IP
address of the client. Secondly, it calls the other gearman function to retrieve
the 20 last records from the database and displays it on the website.

The MySQL database contains 1 database with 1 table which can store the
information in a logical way.

Make sure the entire environment is as safe and production ready as you can.
Because of limited time and resources, we accept that the loadbalancer, MySQL
database and gearman job server are not redundant, but everything else should
be configured in such a way as you would any production-grade platform.
