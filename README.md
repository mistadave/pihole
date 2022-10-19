# PI-Hole

This project is for me to test PI-Hole with docker and set it up to block the ads in my local network.

[PI Hole Project](https://pi-hole.net) all documentation and varaints to set it up.

Run the docker compose command, if your using a docker swarm. If only docker is running, the ``mode: host `` isn't required to set in the docker-compose file.

```bash
docker-compose up -d
```

After the PI-Hole is running, follow the Forgot password to login on the admin backend.

## Fix DNS Resolve on Hosted Server

Fix name resolve on hosting server, since it will probably fail.

```bash
sudo nano /etc/resolv.conf

nameserver 127.0.0.1
```

## Fix resolving clients

If possible, set the DNS option 6 in your router, which will advertise the DNS server to  your DHCP clients.
Add here your PI-hole ip and you'll see the single clients instead of only your router as "client".
If the client names aren't resolve, activate under `settings > dns > Conditional forwarding`. 
Set the flag, entry your local net in CIDR notation and the DHCP server, which is usually your router.

Example:

* 192.168.0.0/24 192.168.0.1 homenet.local

If your router doesn't support this option, then you either have to choose your PI-Hole as DHCP server.

## Config for FTL

If you reach the rate limit, set the followign option in etc-pihole/pihole-FTL.conf

```conf
RATE_LIMIT=0/0
REPLY_ADDR4=0.0.0.0
```

## Adding Adlists

Here is a list of sample which are good to use.

Find more list on firebog

* [https://firebog.net](https://firebog.net)
* [https://dbl.oisd.nl](https://dbl.oisd.nl) this page is the list itself

```
https://mirror1.malwaredomains.com/files/justdomains		
Migrated from /etc/pihole/adlists.list
Default

https://adaway.org/hosts.txt		
Adaway List
Default

https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt		
Disconnect Simple AD
Default

https://v.firebog.net/hosts/Easylist.txt		
EasyList
Default

https://v.firebog.net/hosts/Easyprivacy.txt		
EasyPrivacy
Default

https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-blocklist.txt		
notrack Blocklist
Default

https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt		
Simple Tracking
Default

https://dbl.oisd.nl
OISD Blocklist
Default
```