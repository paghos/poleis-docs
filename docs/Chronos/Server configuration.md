We'll host Chronos using a server based on Ubuntu, we strongly suggest to use the latest LTS Server version.
### Step 1 - updates and software installation

Open a shell and execute the following commands that will update and upgrade the system.

```shell
sudo apt-get update && sudo apt-get upgrade
```

After you completed the update process, install the following packages.

```shell
sudo apt-get install -y python3 python3-pip python3-venv unzip
```

We assume you were running the previous commands as root, please create a new user called '*chronos*' as running Flask web apps as root is not recommended.
To do that run the following command and follow the instructions

``` shell
adduser chronos
```

Then add the previously created user to the 'sudo' group,

``` shell
usermod -aG sudo chronos
```

Now log out and proceed with the user chronos.

We'll use [Waitress](https://pypi.org/project/waitress/) as web server.

### Step 2 - Creating the Chronos environment

First we need to create the directory for Chronos:

``` shell
mkdir /mnt/chronos && cd /mnt/chronos
```

Then we download the latest version of it from GitHub (you need to update the URL according to the current version)

```shell
wget https://github.com/paghos/poleis-chronos/latest.zip
```

And we unzip it

```shell
unzip latest.zip
```

Before proceeding, remove the downloaded zip

```shell
rm -rf latest.zip
```

Check if the files were extracted

```shell
ls 
```

If everything looks like this, you're good to go!

```shell
app.py  assets  chronosconf.py  ClientOperatore.py  flask_session  instance requirements.txt  static  templates
```

#### Configure Chronos as described in [this guide](/Chronos/Environment setup/)

Create the virtual environment

```shell
python3 -m venv venv
```

And activate it

```shell
source venv/bin/activate
```

Install all the necessaries libraries for Chronos

```shell
pip install /mnt/chronos/requirements.txt
```


### Step 3 - Test the functionality

Before continuing we want to check if what we have done so far works.
To do that we'll run Chronos to check if everything works.

```shell 
waitress-serve --host 0.0.0.0 app:app
```

Then, using a web browser open the following IP: machineip:8080.

If you see Chronos home everything works as expected.

After you've done that, desconnect from the virtual environment by giving the following command.

```shell
deactivate
```


### Step 4 - Configure autostart

Download the latest version of the execution script [from here](http://downloads.poleis.cloud/chronos/exec.sh) and put it in /opt

```shell 
cd /opt
```

And download the execution script

```shell 
sudo wget https://downloads.poleis.cloud/chronos/exec.sh
```

After you've done this, set it to be executed at every boot.

Edit the crontab file by giving the following command:

```shell 
crontab -e
```

Select 'nano' as text editor, and add the following line at the bottom of the file:

``` 
@reboot bash /opt/exec.sh
```

Save by giving 'Control + X' and confirm with Y.

Done! 

Reboot the system and everything should work as expected.

Your Ubuntu Server is now configured to work with Chronos. 

Chronos should be available at MACHINE_IP:8080, if not please do some troubleshooting and do these steps again or, [send us an email](mailto:hello@poleis.cloud).
