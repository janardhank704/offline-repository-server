# offline-repository-server
This is my first git Repositroy.
<br>
Author - janardhan k
***FIRST STEP***
# To install the appache server
dnf install httpd -y 
# This is the default directory for the Apache HTTP Server
cd /var/www/html/
# To the move into the corrent working directory
mv /rocky9 / ./
# Let me know if the files were moved
ls 
# To the restore SELinux security contexts recursively on the directory
restorecon -R /rocky9
# To open and edit the main Apache HTTP Server configuration file using the vim text editor
vim /etc/httpd/conf/httpd.conf
:set nu
# we have to go to line no 134 
<Directory "/var/www/html/rocky">
add and add your directory name
# Then save and quit
:wq!
# The restart the appche server
systemctl restart httpd
# We have enabled Apache server
systemctl enabled httpd -now
# We have enabled firewalld service
systemctl enable firewalld.service --now
# To check  list all the network services currently allowed of the firewallfirewall-cmd --list-services
firewall-cmd --list-services
# Next let's add a firewall server
firewall-cmd --add-service={http,https} --permanent
firewall-cmd --reload
# To check that the services were added successfully or not 
firewall-cmd --list-services
# Let's install CreatorRepo now
dnf install createrepo -y 

***SENCOND STEP***

# Now, let's configure the /etc/yum.repos.d directory on the next client machine.
# We navigate to this directory /etc/yum.repos.d
cd /etc/yum.repos.d
# Let's create a file and configure it now
vim local_env.repo
[AppStream_env_repo]
name= AppSteam
baseurl=http://192.168.149.133/rocky9/Packages/AppStream/
enabled=1
gpgcheck=0

[BaseOS_env_repo]
name= BaseOS
baseurl= httpd://192.168.149.133/rocky9/Packages/BaseOS
enabled=1
gpgcheck=0

# Then save and quit
:wq!
# Now we need to generate the .repodata or metadata
 createrepo /var/www/html/repos/myrepo
 Eg :  createrepo /var/www/html/rocky9/Packages/AppSteam
 Eg :  createrepo /var/www/html/rocky9/Packages/BaseOS
 
 # To Clean dnf caches and update the repository list
     dnf clean all
     dnf makecache
     dnf update
     
    



