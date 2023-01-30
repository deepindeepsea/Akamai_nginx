# Akamai_nginx
Akamai Scripts and NGNIX conf

     Here are the scripts I used for my Nginx test.
 
 
 
LG is the load generating server
DUT is device under test
OS is Origin simulator (fake origin)
 
Eth0 interfaces and Eth1 interfaces should be different subnet. We need 100Gbps on all interfaces.
 
akamai@akamai:~$ cat /etc/os-release 
PRETTY_NAME="Ubuntu 22.04 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04 (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
akamai@akamai:~$ uname -a
Linux akamai 5.15.0-48-generic #54-Ubuntu SMP Fri Aug 26 13:26:29 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
 
We use Ubuntu for all our tests. Please use Ubuntu LTS.
 
Test setup
 
Please install Nginx on DUT machine
sudo apt-get install nginx
sudo apt install sysstat
sudo cp ./nginx.conf /etc/nginx/nginx.conf 
sudo rm /etc/nginx/sites-enabled/default
sudo mkdir -p /data/nginx/cache
sudo systemctl restart nginx
 
Please install wrk2 on LG machine 
Clone wrk2 from its git repo and compile it
 
Please install apache on OS machine 
sudo apt install apache2
cd /var/www/html/hello/
sudo dd if=/dev/urandom of=./4M bs=4000000 count=1
sudo dd if=/dev/urandom of=./2M bs=2000000 count=1
sudo dd if=/dev/urandom of=./1M bs=1000000 count=1
sudo dd if=/dev/urandom of=./512K bs=512000 count=1
sudo dd if=/dev/urandom of=./256K bs=256000 count=1
sudo dd if=/dev/urandom of=./128K bs=128000 count=1
sudo dd if=/dev/urandom of=./64K bs=64000 count=1
sudo dd if=/dev/urandom of=./1K bs=1000 count=1
sudo systemctl restart apache2.service
sudo systemctl status apache2.service
 
 
Verify the network connections with iperf, verify if you can curl the Nginx and see if you are able to get Apache HTTP servers webpage through Nginx on your LG machine. 
 
It’s a crude setup but gives me my numbers.
Please let me know if you have any questions.
 
 
Note: I have also attached my 1LG and 2LG (2 load generator) test numbers.
