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
