# WebApplication13

This is an example of Dockerfile with NuGet.config file with configured private feed. `NuGet.config` file in the solution folder contains the feed URL and uses credentials from `HANGFIRE_LOGIN` and `HANGFIRE_PASSWORD` environment variables. Dockerfile contains instructions to copy the `NuGet.config` file into the root folder of a container image, defines `HANGFIRE_PASSWORD` and `HANGFIRE_LOGIN` build arguments (via the `ARG` command) and adds the required environment variables (via the `ENV` command) based on build arguments. Build arguments are defined because of the limitations that "docker build" command can't use environment variables when building the image. And we are using the same names for build arguments and environment variables because in this case build arguments can be resolved automatically from environment variables of a working machine:

docker build -f Dockerfile .. --build-arg HANGFIRE_LOGIN --build-arg HANGFIRE_PASSWORD

But as an alternative we can pass them directly:

docker build -f Dockerfile .. --build-arg HANGFIRE_LOGIN=SomeLogin --build-arg HANGFIRE_PASSWORD=SomePassword