#### Important commands for unprivilideged containers

LXC containers are great, you can get the flexibility and bootup speed of a docker image, and the flexibility and + networking a VM would have, the only issue is, the permissions!  If you launch in priviledged mode, then it puts your proxmox/hypervisor at a huge security risk if the LXC container is compromised.  However if you can give it the right permissions, you can run it as an unprivilidged container just fine!

Once you create the LXC container, just edit the .conf file and add the permissions I gave you here in the 101.conf file.  This will allow you to mount folders from the 1st host user(in my case "mack"), to the LXC container, and it can read/write only to that folder.  This will allow your LXC containers to actually share folders very easily!


mount folder from the host:

````
sudo pct set 109 -mp0 /home/mack/<folder-name>/,mp=/home/mack/<folder-name>/
````

Note: it is important to set the permissions in order to be able to read/write to the mount folder.  Then you can mount from say, user "mack" to user "mack in the LXC container without having to give it explicit "root" credentials or making it an unpriviledged container.
