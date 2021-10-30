# Load Balancing Amazon RDS Mysql Simple Way
### A simple wordpress website hosted under a auto-scaled environment with RDS load balancing


![alt text](https://github.com/rony-james/Hosting-website-with-RDS-Load-balancing/blob/main/RDS-LB.jpg?raw=true)

## Used Resources
- EC2
- VPC
- ELB
- Route 53
- RDS
- NFS



In this project a WordPress website hosted on an EC2 instance with auto-scaling enabled. The files of the website are stored in EFS storage that is attached with the EC2. An auto-scaling group is enabled with an application load balancer. The endpoint of the application load balancer is configured as the A record of the domain, which will lead to the connections to the load balancer.
On Route 53, we have two hosted zones available. 
![alt text](https://github.com/rony-james/Hosting-website-with-RDS-Load-balancing/blob/main/R53.png?raw=true)
The first one is the public-hosted zone and the second one is the private-hosted zone. A private hosted zone determines how traffic is routed within an Amazon VPC. Your resources are not accessible outside the VPC. You can use any domain name. The public hosted zone is for the main domain and the private hosted zone is for the RDS load balancing.  RDS master has two read replicas and I am using those replicas for weighted load balancing with the help of a private hosted zone.
![alt text](https://github.com/rony-james/Hosting-website-with-RDS-Load-balancing/blob/main/db-identifier.png?raw=true)

Added two CNAME records to our local domain and set name to read.ddr3.website.local and TTL to 1 second and select routing policy to weighted and fill weight to 50. We should need to provide the database name on the configuration file as "read.ddr3.website.local". 
