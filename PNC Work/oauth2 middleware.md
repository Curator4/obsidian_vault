tags: [[oauth2 middleware]], [[OAuth 2.0]], [[Reverse Proxy NSBV]], [[nginx_oath2.png]]

nsbv server is `10.181.10.200`, dns `rmgroup.nsbvteknik.dk`, has both [[nsbv_nginx]] and [[oauth2 middleware]] running on it
login: Administrator, Rudersdal7913

### OAuth 2 middleware
Currently nginx forwards incoming ``port 443`` requests with the ``/GIS`` suffix towards `http://localhost:3000`
the express server then gets token and forwards to target `https://ac.hbr.dk/wfs/lokationer_stationer?SERVICE=WFS&REQUEST=GetCapabilities&ACCEPTVERSIONS=2.0.0,1.1.0,1.0.0`
with appended token


test with calls in postman to `https://10.181.10.200/GIS`

https://10.181.10.200/GIS/wfs/lokationer_stationer?SERVICE=WFS&REQUEST=GetCapabilities&ACCEPTVERSIONS=2.0.0,1.1.0,1.0.0

https://rmgroup.nsbvteknik.dk/GIS/wfs/lokationer_stationer?SERVICE=WFS&REQUEST=GetCapabilities&ACCEPTVERSIONS=2.0.0,1.1.0,1.0.0


i guess can either
	1. add custom routes for each of the paths he wants
	2. add a wildcard route and pass the uri

i do the "wildcard" like i did with the normal /location route, and just pass along the uri variable,

for now i will 
	1. pass the URI on the `/GIS` path [x]
	2.  then remove the "/GIS" in an extra middleware function [x]
	3.  add logging middleware [x]
	4.  then forward to arbitrary url in the proxy middleware [x]
	5. add service functionality, run in background and on startup

Okay, i added these things, the service is installed/started with the service.js script, and removed with the uninstall script

