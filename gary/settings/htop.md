## install htop on centos6
wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
rpm -ihv epel-release-6-8.noarch.rpm
yum groupinstall "Development Tools"
yum install ncurses ncurses-devel
wget http://hisham.hm/htop/releases/2.0.2/htop-2.0.2.tar.gz
tar xvfvz htop-2.0.2.tar.gz
cd htop-2.0.2
./configure
make
make install
