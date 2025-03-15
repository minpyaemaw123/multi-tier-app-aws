# ElasticCache Setup

1. Create Subnet Group
	The Same procedure with RDS Setup, we will create subnet Group first and then parameter group to be used in ElasticCache setup.
	
	Name: **memcached-sub-grp**
	
	VPC: Default VPC
	
	![](imgs/memcached-sub-grp.png)
2. Create Parameter Group

	Name: memcached-para-grp  

	![](imgs/memcahced-para-grp.png)
3. Create Memcached

	Choose "Design your own cahce" for our own configuration.

	![](imgs/create-memcached-1.png)
	
	Cluster Name: demo-cluster
	
	Default Port: **11211** is used for Memcached.
	
	Please select the created **memcached-para-grp**
	
	![](imgs/create-memcached-2.png)
	
	Please select the created **memcached-sub-grp**
	
	![](imgs/create-memcached-3.png)
	
	Please review and create ElasticCache.
	
	![](imgs/create-memcached-4.png)
	

