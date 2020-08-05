# openliberty-s2i-starter
Cirrus uses a modified version of Red Hat's Node.js Universal Base Image(s) as the foundation for this s2i container runtime. The following README is composed of fragments from the [OpenLiberty's Repository](https://github.com/OpenLiberty/open-liberty-s2i)
and Red Hat's [Guide on Universal Base Images](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/building_running_and_managing_containers/using_red_hat_universal_base_images_standard_minimal_and_runtimes).

Usage
-----

When creating a Cirrus build, select the **OpenLiberty S2I** for the container runtime.
By default, this image will do the following:

1. If a pom.xml file is found in the root of the source tree, it will be built using maven. 

2. If the environment variable `LIBERTY_RUNNABLE_JAR` is set, the build will attempt to copy that file to `/opt/ol/ol-runnable.jar`. At runtime, S2I will run that jar file instead of running the normal Liberty instance.

3. If a `server.xml` file exists in the directory `src/main/liberty/config` it will be copied to the config directory of the Liberty instance. 

4. If the directory `src/wlp/usr` exists, it will be copied to the `wlp` directory to the Liberty instance. 

5. All `WAR`, `JAR`, `EAR`, and `RAR` files from the build will be copied to either the `apps` or `dropins` directory the Liberty instance depending on the value of the `DEPLOY_TO_APPS` environment variable. 


Build variables
---------------

The variables below affect the build process of your application, and can be added via _Build Environment Vars_ in the build form.

**`DEPLOY_TO_APPS`**
  * Description: When true, applicaton binaries will be copied to `apps` instead of `dropins`