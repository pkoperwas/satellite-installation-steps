https://docs.redhat.com/en/documentation/red_hat_satellite/6.15/html/installing_satellite_server_in_a_disconnected_network_environment/index
x86_64 architecture
The latest version of Red Hat Enterprise Linux 8
4-core 2.0 GHz CPU at a minimum
A minimum of 20 GB RAM is required for Satellite Server to function. In addition, a minimum of 4 GB RAM of swap space is also recommended. Satellite running with less RAM than the minimum value might not operate correctly.
A unique host name, which can contain lower-case letters, numbers, dots (.) and hyphens (-)
A current Red Hat Satellite subscription
Administrative user (root) access
Full forward and reverse DNS resolution using a fully-qualified domain name
SELinux mode
SELinux must be enabled, either in enforcing or permissive mode. Installation with disabled SELinux is not supported.
Table 1.1. Storage requirements for a Satellite Server installation
Directory	Installation Size	Runtime Size
/var/log

10 MB

10 GB

/var/lib/pgsql

100 MB

20 GB

/usr

10 GB

Not Applicable

/opt/puppetlabs

500 MB

Not Applicable

/var/lib/pulp

1 MB

300 GB


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
