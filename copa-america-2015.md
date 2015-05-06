Copa America 2015 Dev
=====================

Change into **_~/src_** or wherever you want to store the **_ca2015_** repo:

`cd ~/src`

Clone the **_ca2015_** repo from gitlab and **_cd_** to it:

`git clone git@10.12.23.123:webapp/ca2015.git && cd ca2015`

Pull down vagrant box ssh keys (copy/paste):

```
tmpdir=/tmp/sn-vagrant-copa2015; mkdir $tmpdir; cd $tmpdir; \
curl -Lk "https://www.dropbox.com/s/k21kqfwnzss37y7/copa2015-ssh-keys.gz?dl=0" \
    -o v.gz && \
    tar xvzf v.gz && \
    mv -i id_rsa_vagrant_copa2015* ~/.ssh/ && \
    cd -; rm -rf $tmpdir
```

Grab the config file for vagrant:

`curl -L "http://cl.ly/ankO" -o Vagrantfile`

If you have already done the previous steps and simply need to use the most
recent box - before starting it back up, you'll need to destroy the existing vm
and remove the Vagrant box:

```
vagrant destroy
vagrant box remove copa-ubuntu-subzero
```

Start vagrant vm:

`vagrant up`

Login to the guest vm:

`vagrant ssh`

Install the project dependencies on the guest:

```
cd /srv/www/local.ca2015.com
composer install
./repository/create
git clone git@git.performgroup.com:webapp/ca2015-config.git /srv/www/local.ca2015.com/app/config/connections
```

Now, from the host, change the permissions of the _.cache_ dir:

`chmod 777 .cache`

Access the site in your browser:

http://local.ca2015.com
