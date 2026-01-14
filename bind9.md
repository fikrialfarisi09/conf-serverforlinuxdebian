root@debian:~#cd /etc/bind

root@debian:/etc/bind# vim named.conf 

Fill in the bottom line with this configuration

	zone	“name.com” {	
		type master;
		file “/etc/bind/db.name”;
	};
	zone	“1.168.192.in-addr.arpa” {
		type master;
		file “/etc/bind/db.192”;
	};
	
root@debian:/etc/bind# cp  db.local  db.name

root@debian:/etc/bind# cp  db.127   db.192

root@debian:/etc/bind# vim  db.name

	; BIND data file for local loopback interface
	$TTL		604800
	@		IN		SOA		name.com.  root.name.com.  
					2		; Serial
		    604800			; Refresh
			86400			; Retry
		 2419200			; Expire
			 604800  		; Negative Cache TTL      

	@		 IN		NS		ns.name.com.
	@		 IN		A		  192.168.1.1
	ns		IN		A		  192.168.1.1

root@debian:/etc/bind#  vim  db.192

	$TTL		604800
	@		IN		SOA		namasiswa.com.  root.namasiswa.com.	
						1			; Serial
					604800			; Refresh
				  	86400			; Retry
					2419200			; Expire
			   		604800  		; Negative Cache TTL
	
	@		IN		NS		ns.name.com.
	1		IN		PTR		ns.name.com.     # The number 1 at the beginning is an example of a server IP address


root@debian:/etc/bind#  vim  /etc/resolv.conf

	nameserver  192.168.33.1
