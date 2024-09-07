# Red Hat Satellite 6 - "disconnected network method" installation steps 

#


More info you can find here: https://docs.redhat.com/en/documentation/red_hat_satellite/6.15/html/installing_satellite_server_in_a_disconnected_network_environment/index 

* OS: Red Hat Enterprise Linux 8 (RHEL9 is still not supported)
* 4-core CPU
* 20 GB RAM 
* 4 GB RAM 
* A unique host name, which can contain lower-case letters, numbers, dots (.) and hyphens (-)
* A current Red Hat Satellite subscription
* Full forward and reverse DNS resolution using a fully-qualified domain name
* SELinux must be enabled, either in enforcing or permissive mode. Installation with disabled SELinux is not supported.
* Storage requirements for a Satellite Server installation
 * /var/lib/pgsql installation size 100MB, up to 20GB
 * /opt/puppetlabs installation size 500MB
 * /var/lib/pulp installation size 1MB up to 300GB
 * /var/log  installation size 10MB up to 10GB
 * /usr installation size 10GB    

If you mount the /tmp directory as a separate file system, you must use the exec mount option in the /etc/fstab file. If /tmp is already mounted with the noexec option, you must change the option to exec and re-mount the file system. This is a requirement for the puppetserver service to work.


 mount -o loop rhel8-DVD.iso /media/rhel8
 # cp /media/rhel8/media.repo /etc/yum.repos.d/rhel8.repo
# chmod u+w /etc/yum.repos.d/rhel8.repo
[RHEL8-BaseOS]
name=Red Hat Enterprise Linux BaseOS
mediaid=None
metadata_expire=-1
gpgcheck=0
cost=500
baseurl=file:///media/rhel8/BaseOS/

[RHEL8-AppStream]
name=Red Hat Enterprise Linux Appstream
mediaid=None
metadata_expire=-1
gpgcheck=0
cost=500
baseurl=file:///media/rhel8/AppStream/

# mkdir /media/sat6
# mount -o loop sat6-DVD.iso /media/sat6
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
 cd /media/sat6/
 # ./install_packages



 root@satellite [ /media/sat6 ]# ./install_packages 
This script will install the satellite packages on the current machine.
   - Ensuring we are in an expected directory.
   - Copying installation files.
   - Creating Satellite Repository File
   - Creating Maintenance Repository File
   - Checking to see if Satellite is already installed.
   - Importing the gpg key.
Error: Problems in request:
Modular dependency problems:

 Problem: conflicting requests
  - nothing provides module(pki-core) needed by module satellite:el8:61520240814200641:0975698b.x86_64 from Satellite-local
  - nothing provides module(platform:el8) needed by module satellite:el8:61520240814200641:0975698b.x86_64 from Satellite-local
  - nothing provides module(postgresql:12) needed by module satellite:el8:61520240814200641:0975698b.x86_64 from Satellite-local
  - nothing provides module(ruby:2.7) needed by module satellite:el8:61520240814200641:0975698b.x86_64 from Satellite-local
Error while executing command: 'dnf module enable -y satellite:el8'
root@satellite [ /media/sat6 ]# dnf module reset postgresql
Updating Subscription Management repositories.
Last metadata expiration check: 0:06:20 ago on Sat 31 Aug 2024 01:11:42 AM CEST.
Dependencies resolved.
Nothing to do.
Complete!
root@satellite [ /media/sat6 ]# dnf module reset pki-core
Updating Subscription Management repositories.
Last metadata expiration check: 0:06:29 ago on Sat 31 Aug 2024 01:11:42 AM CEST.
Unable to resolve argument pki-core
Error: Problems in request:
missing groups or modules: pki-core
root@satellite [ /media/sat6 ]# dnf module reset postgresql
Updating Subscription Management repositories.
Last metadata expiration check: 0:06:42 ago on Sat 31 Aug 2024 01:11:42 AM CEST.
Dependencies resolved.
Nothing to do.
Complete!
root@satellite [ /media/sat6 ]# dnf module reset ruby
Updating Subscription Management repositories.
Last metadata expiration check: 0:06:51 ago on Sat 31 Aug 2024 01:11:42 AM CEST.
Dependencies resolved.
Nothing to do.
Complete!
root@satellite [ /media/sat6 ]# dnf module reset platform
Updating Subscription Management repositories.
Last metadata expiration check: 0:06:58 ago on Sat 31 Aug 2024 01:11:42 AM CEST.
Unable to resolve argument platform
Error: Problems in request:
missing groups or modules: platform
