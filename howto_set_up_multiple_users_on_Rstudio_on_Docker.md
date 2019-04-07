Setting up multiple user logins to RStudio running in a Docker container on Jetstream
================
Dana
March 28, 2019

- [One way of setting up Rstudio and R](#one-way-of-setting-up-rstudio-and-r)
- [Adding multiple users and configuring their permissions](#adding-multiple-users-and-configuring-their-permissions)
    - [1. Add more users to an existing instance](#1-add-more-users-to-an-existing-instance)
       - [Create new users](#create-new-users)
       - [Enable downloading RStudio packages](#enable-downloading-rstudio-packages)
       - [Enable `sudo` in terminal](#enable-sudo-in-terminal)
    - [2. Launch a separate R Studio instance bound to a different port](#2-launch-a-separate-r-studio-instance-bound-to-a-different-port)
- [Installing `curl`, `pip3` and `aws cli` on a fresh `verse` image](#installing-curl-pip3-and-aws-cli-on-a-fresh-verse-image)  
- [Reference docs](#reference-docs)

*With thanks to the [Rocker Project](https://www.rocker-project.org/) for R on Docker, Indiana University and the National Science Foundation for cloud compute resources through [Jetstream](https://jetstream-cloud.org/), [DIBSCI](http://ivory.idyll.org/dibsi/2018/WHO.html) at UC Davis for documentation, and Carl Boettiger at UC Berkeley for reproducible research inspiration and an initial version of these instructions. All remaining errors are mine, and suggestions to improve these notes are welcome* 

[Jetstream](https://jetstream-cloud.org/) is an NSF-supported cloud compute resource that runs on the open-source software Atmosphere and OpenStack.

### One way of setting up Rstudio and R

If you already have a Jetstream login and allocation, to run R Studio on Jetstream:

-   Log in and go to 'Create a new project'
-   Enter project name and description
-   Select the size and *image* you would like to use (images have various software preinstalled): select [this](https://use.jetstream-cloud.org/application/images/107) Ubuntu image that includes Docker and GUI support
-   Once the new instance for your project is active (green dot), click the "Open web shell" link on the right hand side
-   See if you are able to run docker commands:

    ``` bash
    docker run hello-world
    ```

If configured correctly, this will say `Hello from Docker!...`

If you get an error about permission denied and docker daemon, try adding yourself to root privileges with `sudo usermod -aG docker example_username`, where `example_username` is your username, and then close and re-open the web shell so your new permissions take effect. Alternatively, you can run all the `docker ...` commands prefaced with `sudo`.  See specific Docker on Linux docs [here](https://docs.docker.com/install/linux/linux-postinstall/) for more background. 

-   Start a new Docker container that has R, R Studio, and the `tidyverse` preinstalled (you could also install these and all the required dependencies without Docker but it takes a long time and is potentially error-prone)

``` bash
    docker run -d -p 8787:8787 --rm -e PASSWORD=example_password rocker/tidyverse
```

or, if in addition you also want TeX installed and tools for publishing, use the larger `verse` image:

``` bash
    docker run -d -p 8787:8787 --rm -e PASSWORD=example_password rocker/verse
```

-   *What do all those flags mean?*

    -   "-d" for *detach* means the container will run 'in the background' , and return a command prompt (without this flag your container will be running but you won't be able to run anything else at the command prompt until the container is stopped)
    -   "-p" for *port* is a port and also the suffix for the url your RStudio session will be accesible at
    -   "-e" for *environment* is passing the `PASSWORD` variable to the created computational environment
    -   "--rm" for *remove* , which will automatically delete this container after it exits (note it does not delete the underlying image the container was based on)
    -   `rocker/tidyverse` - this specifies the exact Docker image (already created by the Rocker project) to use. Using the same image, you can set up the exact same computational environment many differnet times, or many different people can all use it to set up the same environment - More details about this image at <https://www.rocker-project.org/images/>
    - If you also need to allow a user to install tools using `apt get` at the command time inside the RStudio session (eg to have `sudo` access), you will additionally need to add `-e ROOT=true` in the `docker run` command above - see Rocker docs [here](https://www.rocker-project.org/use/managing_users/) and more details in the section on `sudo` below 
    
``` bash
    docker run -d -p 8787:8787 --rm -e PASSWORD=example_password -e ROOT=true rocker/verse
```  

-   To find the URL you can use to log into the new R Studio session, run

    ``` bash
    echo My RStudio Web server is running at: http://$(hostname):8787/
    ```

Note the URL above is *http* not *https*, the latter is also possible to set up but requires a custom domain name

Note to copy and paste text from the Jetstream web shell, you have you highlight it and then press Ctrl + Alt + Shift

-   Paste the URL above into your web browser, and to login:

    -   The default username is "rstudio"
    -   The password is whatever you chose in the `docker run...` command above for `example_password`

    Congrats, you are now running RStudio on Jetstream!

    The `rstudio` user has permission to install packages.

Optional UNIX configuration notes:

-   `whoami` in at the command line is *not* the same as the user for logging in to the R Studio browser prompt
-   Specifying a username with `docker run -u...` also doesn't work for the R Studio login prompt

### Adding multiple users and configuring their permissions

There are two ways to do this:

1.  Add users to your existing instance, or
2.  Launch a separate R Studio instance bound to a different port

#### 1. Add more users to an existing instance

##### Create new users
-   With your Jetstream instance active, launch the web shell
-   See the ids of your running Docker container with RStudio by running `docker ps`. You will need to write down or remember the first 5 digits of your CONTAINER ID (a long string of numbers and letters)

-   To run commands inside that container, run

``` bash

    docker exec -ti CONTAINER_ID bash
```

Where CONTAINER\_ID is eg "904b2", the first 5 digits. Notice your prompt will change now that you are inside the container.

-   Now you can use regular UNIX commands to create a new user (this is not Docker-specific)

``` bash
 adduser example_user
```

Enter a password, press 'Enter' to leave the other questions blank (eg Name, Work Phone...), they are not required, and press Y for "Yes"

- At this point, someone could go to the same URL you set up above, and login with this new username and password but they wouldn't be able to install packages (no root access)

##### Enable downloading RStudio packages
-   To give the new user the right to download packages, add them to the `staff` group

``` bash
 usermod -aG staff example_user
```

To see a list of all the users (this includes some other system info) as well

``` bash
cat /etc/passwd
```

To change a password (note `passwd` below is not a typo)

``` bash
sudo passwd example_username
```
##### Enable `sudo` in terminal

- Only if acess to install command line programs is required
- Requires `docker run` command to have already been run with `-e ROOT=true` (see above), then you additionally have to add the user to `sudoers`

```bash
adduser example_username sudo
```

``` bash
exit
```
to return to the command line outside of that container.

And the login url for the new users same as above, at:

``` bash
echo My RStudio Web server is running at: http://$(hostname):8787/
```

- Related Rocker Github issue [here](https://github.com/rocker-org/rocker/issues/206)
- For more help, see instructions online eg 'Ubuntu add new user to sudo', eg [here](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart) are instructiosn for how to test this from the terminal with `su`

#### 2. Launch a separate R Studio instance bound to a different port

Alternatively, start an additional Docker container on the same Jetstream instance with a different port number

`bash  docker run -d -p 8888:8787 -rm -e PASSWORD=newpassword rocker/tidyverse`

The default username will still be "rstudio", and the password will be whatever you just specified, but the login URL will be different (note the port number is changed above and accordingly also changed below)

``` bash
echo My RStudio Web server is running at: http://$(hostname):8888/
```

### Installing `curl`, `pip3` and `aws cli` on a fresh `verse` image

1. Install curl, eg following instructions [here](https://www.luminanetworks.com/docs-lsc-610/Topics/SDN_Controller_Software_Installation_Guide/Appendix/Installing_cURL_for_Ubuntu_1.html)

```{bash}
sudo apt-get update
```
```{bash}
sudo apt-get install curl
```
```bash
curl --version
```

2. Install pip - use python 3

- See "Install pip" instructions [here](https://docs.aws.amazon.com/cli/latest/userguide/install-linux.html#install-linux-pip)
    - `verse` image has python three, so use the python3 variants, eg `python3 get-pip.py --user`, not `python get-pip.py --user`
    - For the step about editing your bash profile, it will probably be called `.profile` (even though that is not listed as one of the options in Amazon's docs). 
    - You can use `vim` to edit the file (type `vim .profile` to open the file: 
    
        - `i` to go into "insert" (editing) mode
        - add `export PATH=~/.local/bin:$PATH` to the file below anything in it already (you can start a line with `#` as a comment to explain why it's there)
        - press `:` to exit editing mode and `wq` to save (write) and quit to go back to the terminal
    - Per the AWS docs, make sure you source the file after editing it! ` source ~/.bash_profile`
        
3. Install `aws cli`

Continue to follow instructions [here](https://docs.aws.amazon.com/cli/latest/userguide/install-linux.html#install-linux-awscli)
    

### Reference docs

-   DIBSCI docs on [setting up a Jetstream instance](https://angus.readthedocs.io/en/2018/jetstream/boot.html) and [installing and running RStudio on Jetstream](https://angus.readthedocs.io/en/2018/visualizing-blast-scores-with-RStudio.html#installing-and-running-rstudio-on-jetstream) - note some of the instructions are specific to their workshop
-   See more details from the Rocker Project on managing user authentication [here](https://www.rocker-project.org/use/managing_users/)
-   [Docker docs](https://docs.docker.com/)
