
## VMWARE exporter for later

### Table of Content
1. [Install Openssl](#install-openssl)
2. [Install Python](#install-python)
3. [References](#references)

### Install openssl
Requirements: >=Python 3.6, newest openssl
1. Download python3 source from [offical website](https://www.python.org/downloads/source/)
2. Download openssl source from [offical website](https://www.openssl.org/source/)
``` bash
sudo yum install zlib-devel perl-Test-Simple 
tar zxvf openssl-*.tar.gz
cd cd openssl-*
./config --prefix=/opt/openssl --openssldir=/opt/openssl no-ssl2
make
make test
```

If Failed test 'running ssl_test 12-ct.cnf' occured, ignore it (fix in next patch)
``` bash
sudo make install
```

### Add to PATH environment
1.Find out the name of openssl lib directory (lib64/lib)
``` bash
export PATH=/opt/openssl/bin:$PATH
export LD_LIBRARY_PATH=/opt/openssl/lib64
export LC_ALL="en_US.UTF-8"
export LDFLAGS="-L /opt/openssl/lib64 -Wl,-rpath,/opt/openssl/lib64"
. ~/.bash_profile
``` 

### Confirm openssl installation
``` bash
which openssl
/opt/openssl/bin/openssl
[leele3@] openssl version
OpenSSL 3.0.3 3 May 2022 (Library: OpenSSL 3.0.3 3 May 2022)
```

## Install Python

### Step1. Extract tarball
``` bash
tar -zxvf Python-3.?.?.tar.xz
```

### Step2. Enable SSL by default
``` bash
vi ./Python-3*/Modules/Setup.dist
```

### Step3. Search for “SSL” and uncomment the code as shown below
``` bash
_socket socketmodule.c
# Socket module helper for SSL support; you must comment out the other
# socket line above, and possibly edit the SSL variable:
SSL=/opt/openssl
_ssl _ssl.c \
 -DUSE_SSL -I$(SSL)/include -I$(SSL)/include/openssl \
 -L$(SSL)/lib -lssl -lcrypto
```

### Step4. Configure python installation script
``` bash
cd {Python script path}
./configure
make
sudo make altinstall or install
```

### Step5. Check for ssl support
``` bash
python3.6
import ssl
```

### Step6. If ssl import error still existing (Optional)
This normally happened when multiple openssl version installed
Need to customize Python3 setup script
1. Modify python3 setup.py following this [link](https://gist.github.com/eddy-geek/9604982)
2. Configure Python3 installation script again
``` bash
cd {python script directory}
./configure --with-openssl=/opt/ (no need openssl directory)
make 
sudo make altinstall or install
```

### Step7. Install vmware exporter
1.download release from [github page](https://github.com/pryorda/vmware_exporter) \
2.extract tarball
``` bash
sudo env "PATH=$PATH" python3.6 setup.py install
```

### References
1. [Openssl Requirement](https://mta.openssl.org/pipermail/openssl-dev/2016-January/003936.html)
2. [Install Python3 on Redhat](https://programmer.group/install-python3-in-centos7.html)
3. [VMware exporter](https://github.com/pryorda/vmware_exporter)
4. [Setup.py modify](https://gist.github.com/eddy-geek/9604982)
5. [Coredump when compiling python with a custom openssl version](https://stackoverflow.com/questions/22409092/coredump-when-compiling-python-with-a-custom-openssl-version)

