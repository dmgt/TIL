Setting up multiple user logins to RStudio running in a Docker container on Jetstream
================
Dana
March 28, 2019

-   [One way of setting up Rstudio and R](#one-way-of-setting-up-rstudio-and-r)
-   [Adding multiple users and configuring their permissions](#adding-multiple-users-and-configuring-their-permissions)
    -   [1. Add more users to an existing instance](#add-more-users-to-an-existing-instance)
    -   [2. Launch a separate R Studio instance bound to a different port](#launch-a-separate-r-studio-instance-bound-to-a-different-port)
-   [Reference docs](#reference-docs)

*With thanks to the [Rocker Project](https://www.rocker-project.org/) for R on Docker, Indiana University and the National Science Foundation for cloud compute resources through [Jetstream](https://jetstream-cloud.org/), [DIBSCI](http://ivory.idyll.org/dibsi/2018/WHO.html) at UC Davis for documentation, and Carl Boettiger at UC Berkeley for reproducible research inspiration and troubleshooting*

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

If you get an error about permission denied and docker daemon, try adding yourself to root privileges with `sudo usermod -aG docker example_username`, where `example_username` is your username

-   Start a new Docker container that has R, R Studio, and the `tidyverse` preinstalled (you could also install these and all the required dependencies without Docker but it takes a long time and is potentially error-prone)

    ``` bash
    docker run -d -p 8787:8787 -rm -e PASSWORD=example_password rocker/tidyverse
    ```

    -   *What do all those flags mean?*

        -   "-d" for *detach* means the container will run 'in the background' , and return a command prompt (without this flag your container will be running but you won't be able to run anything else at the command prompt until the container is stopped)
        -   "-p" for *port* is a port and also the suffix for the url your RStudio session will be accesible at
        -   "-e" for *environment* is passing the `PASSWORD` variable to the created computational environment
        -   "-rm" for *remove* , which will automatically delete this container after it exits (note it does not delete the underlying image the container was based on)
        -   `rocker/tidyverse` - this specifies the exact Docker image (already created by the Rocker project) to use. Using the same image, you can set up the exact same computational environment many differnet times, or many different people can all use it to set up the same environment - More details about this image at <https://www.rocker-project.org/images/>

-   To find the URL you can use to log into the new R Studio session, run

    ``` bash
    echo My RStudio Web server is running at: http://$(hostname):8787/
    ```

Note the URL above is *http* not *https*, the latter is also possible to set up but requires a custom domain name Note to copy and paste text from the Jetstream web shell, you have you highlight it and then press Ctrl + Alt + Shift

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

-   With your Jetstream istnance active, launch the web shell
-   See the ids of your running Docker container with RStudio by running `docker ps`. You will need to write down or remember the first 5 digits of your CONTAINER ID (a long string of numbers and letters)

-   To run commands inside that container, run

``` bash

    docker exec -ti CONTAINER_ID bash
```

Where CONTAINER\_ID is eg "904b2", the first 5 digits

-   Now you can use regular UNIX commands to create a new user (this is not Docker-specific)

``` bash
 adduser example_user
```

Enter a password, press 'Enter' to leave the other questions blank, they are not required, and press Y for "Yes"

-   At this point, someone could go to the same URL you set up above, and login with this new username and password but they wouldn't be able to install packages (no root access)

-   To give the new user the right to download packages, add them to the `staff` group

``` bash
 usermod -aG staff example_user
```

#### 2. Launch a separate R Studio instance bound to a different port

Alternatively, start an additional Docker container on the same Jetstream instance with a different port number

`bash  docker run -d -p 8888:8787 -rm -e PASSWORD=newpassword rocker/tidyverse`

The default username will still be "rstudio", and the password will be whatever you just specified, but the login URL will be different (note the port number is changed above and accordingly also changed below)

``` bash
echo My RStudio Web server is running at: http://$(hostname):8888/
```

### Reference docs

-   DIBSCI docs on [setting up a Jetstream instance](https://angus.readthedocs.io/en/2018/jetstream/boot.html) and [installing and running RStudio on Jetstream](https://angus.readthedocs.io/en/2018/visualizing-blast-scores-with-RStudio.html#installing-and-running-rstudio-on-jetstream) - note some of the instructions are specific to their workshop
-   See more details from the Rocker Project on managing user authentication [here](https://www.rocker-project.org/use/managing_users/)
-   [Docker docs](https://docs.docker.com/)
