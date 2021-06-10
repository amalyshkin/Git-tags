[fff](#instance-testgitlab)
---

## Instance "testgitlab"
* Instance name: "testgitlab.bigbrassband.tk"
* AWS instance ID: i-0c5690f3e4b59074c

Gitlab version 12.7.5 (the latest one, supports only API v4)

### Access
* web interface: https://<...>.bigbrassband.tk

### Credentials
* Username: <...>
* Password: <...>
* PAT: <...> (<...name...>; <...scope...>|all; <...exp.date...>|perpetual)



web interface http://testgitlab.bigbrassband.tk/

Admin:
credentials for UI in browser: admin@example.com/BDAhVaRKxXr1jgNOG
credentials for git clone: root/BDAhVaRKxXr1jgNOG

PAT: HvERBGs_hsy1FFZzcJGk

Guest:
login - isvirkina@issart.com
password - bbb4ever!
The user has
a) Guest access to Slap project and
b) Developer access to StageJS project
c) Guest access to BabylonJS project "http://testgitlab.bigbrassband.tk/root/BabylonJS.git",
         because isvirkina is a Guest member of group-with-guests-permissions and BabylonJS is shared with group-with-guests-permissions.
d) Developer access to engine http://testgitlab.bigbrassband.tk/root/engine.git,
         because isvirkina is a Developer member of group-with-developers-permissions and engine is shared with group-with-developers-permissions

Update guide: https://docs.gitlab.com/omnibus/update/README.html
Update steps using *.rpm package (sample):
> curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
> sudo yum install gitlab-ce-9.0.5-ce.0.el6.x86_64


It has NFS server installed which exports Gitlab repository folder "/var/opt/gitlab/git-data/repositories/git-integration-for-jira" (see /etc/exports for more details).
For more details please read "nfs.txt" file.

---------------------

instance name "GitLab API v4 test server" (i-0495a9c744a649dd6)

Gitlab version 9.4.4 (supports both API v3 and v4)

web interface http://testgitlabv4.bigbrassband.tk/

credentials for UI in browser: admin@example.com/BDAhVaRKxXr1jgNOG
credentials for git clone: root/BDAhVaRKxXr1jgNOG

PATs for admin@example.com:
    tcC1-7w2zxzFN6s7jVGC (denis-2017-12-28, api + read_user, never expires)

---------------------

instance name "GitLab API v3 only test server" (i-07ea9a3e1fd1cf166)

Gitlab version 8.16.9 (supports API v3 only)

web interface http://testgitlabv3.bigbrassband.tk/

credentials for UI in browser: root/BDAhVaRKxXr1jgNOG
credentials for git clone: root/BDAhVaRKxXr1jgNOG

if you ssh to that server, you can lookup the name of the container with "docker ps"
Then you can get an ssh session like this:
docker exec -i -t 5de2bc175f92 /bin/bash
(where 5d... is an ID of corresponding docker task)

--------------------

instance name "gitlab-badssl.bigbrassband.tk" (i-0660bef2470ce130d)

Gitlab version 8.12.0 Community Edition

Web interface: https://gitlab-badssl.bigbrassband.tk

credentials for UI in browser: admin@example.com/BDAhVaRKxXr1jgNOG
credentials for git clone: root/BDAhVaRKxXr1jgNOG

git clone https://gitlab-badssl.bigbrassband.tk/root/test-nchernov.git

--------------------

instance name "testgitlabforjenkins.bigbrassband.tk" (i-06342d36d57698d7a)
was cloned from http://testgitlab.bigbrassband.tk

GitLab version  10.8.3 (564c342)

Web interface: http://testgitlabforjenkins.bigbrassband.tk

Admin:
credentials for UI in browser: admin@example.com/BDAhVaRKxXr1jgNOG
credentials for git clone: root/BDAhVaRKxXr1jgNOG

Guest:
login - isvirkina@issart.com
password - bbb4ever!
The user has
a) Guest access to Slap project and
b) Developer access to StageJS project
c) Guest access to BabylonJS project "http://testgitlab.bigbrassband.tk/root/BabylonJS.git",
         because isvirkina is a Guest member of group-with-guests-permissions and BabylonJS is shared with group-with-guests-permissions.
d) Developer access to engine http://testgitlab.bigbrassband.tk/root/engine.git,
         because isvirkina is a Developer member of group-with-developers-permissions and engine is shared with group-with-developers-permissions

User with few repos (do not add more repositories to it. It may break tests!):
login -  autoTestWithFewRepositories 
password - BDAhVaRKxXr1jgNOG
The user has
a) Developer access to Slap project

One more test user (preferred to be used in tests):
login - bbbtesting
password - wRE@39!IxE
PAT - 4yiavtW9cb5XBvELCVxK


Update guide: https://docs.gitlab.com/omnibus/update/README.html
Update steps using *.rpm package (sample):
> curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
> sudo yum install gitlab-ce-9.0.5-ce.0.el6.x86_64


It has NFS server installed which exports Gitlab repository folder "/var/opt/gitlab/git-data/repositories/git-integration-for-jira" (see /etc/exports for more details).
For more details please read "nfs.txt" file.

--------------------

*From Mark Smith:*

Here's how to take a fresh Amazon Linux EC2 instance and have it run a Docker image. For my example, I'll choose an old GitLab instance.

sudo yum update -y
sudo yum install -y docker
sudo service docker start
sudo chkconfig docker on
sudo usermod -a -G docker ec2-user
exit

docker run -d -p 80:80 --restart always gitlab/gitlab-ce:8.16.9-ce.0

You can find more Docker GitLab images here:  https://hub.docker.com/r/gitlab/gitlab-ce/tags/

If you wish to shell to the docker container, you can do this:
docker ps
# Find the instance id -- hex numeric string

docker exec -i -t 5de2bc175f92 /bin/bash
# For GitLab, you may need to update the host name
vim /etc/gitlab/gitlab.rb
gitlab-ctl reconfigure
gitlab-ctl restart

I'd suggest using Docker for any future test Git server if it has an official Docker image.
