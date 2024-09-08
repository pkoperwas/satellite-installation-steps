# Red Hat Satellite 6 - "disconnected network" installation steps 


Official documentation:
https://docs.redhat.com/en/documentation/red_hat_satellite/6.15/html/installing_satellite_server_in_a_disconnected_network_environment/index 

- OS: Red Hat Enterprise Linux 8.10 (RHEL9 is still not supported)
- 4-core CPU (you can reduce to 2-core after installation in case of LAB envorinment)
- 20 GB RAM (you can reduce to 6GB after installation in case of LAB envorinment)
- 6 GB SWAP
- A unique host name, which can contain lower-case letters, numbers, dots (.) and hyphens (-)
- A current Red Hat Satellite subscription
- Full forward and reverse DNS resolution using a fully-qualified domain name
- SELinux must be enabled, either in enforcing or permissive mode. Installation with disabled SELinux is not supported.
- /var/lib/pgsql installation size 100MB, up to 20GB
- /opt/puppetlabs installation size 500MB
- /var/lib/pulp installation size 1MB up to 300GB
- /var/log  installation size 10MB up to 10GB
- /usr installation size 10GB    
- If /tmp is a separate file system, you must use the exec mount option in the /etc/fstab file.

**Download ISO Files from Red Hat Customer portal**
- rhel-8.10-x86_64-dvd.iso
- Satellite-6.15.3-rhel-8-x86_64.dvd.iso

**Mount ISO files**
```
mount -o loop rhel-8.10-x86_64-dvd.iso /mnt/rhel8
mount -o loop Satellite-6.15.3-rhel-8-x86_64.dvd.iso /mnt/satellite6
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```

**Create RHEL8 Repo from ISO file**
/etc/yum.repos.d/rhel8.repo
```
[RHEL8-BaseOS]
name=Red Hat Enterprise Linux BaseOS
mediaid=None
metadata_expire=-1
gpgcheck=0
cost=500
baseurl=file:///mnt/rhel8/BaseOS/

[RHEL8-AppStream]
name=Red Hat Enterprise Linux Appstream
mediaid=None
metadata_expire=-1
gpgcheck=0
cost=500
baseurl=file:///mnt/rhel8/AppStream/
```


**Install Satellite packages**
```
 cd /mnt/satellite6
 ./install_packages
```

**Enabling connections from clients to Satellite**
```
firewall-cmd --add-port="5647/tcp" --add-port="8000/tcp" --add-port="9090/tcp"
firewall-cmd --add-service=dns --add-service=dhcp --add-service=tftp --add-service=http --add-service=https --add-service=puppetmaster
firewall-cmd --runtime-to-permanent
```

**Install/Configure Satellite**
```
satellite-installer --scenario satellite --foreman-initial-organization "koperwas.local" --foreman-initial-location "Poland" --foreman-initial-admin-username admin --foreman-initial-admin-password changeme
```
