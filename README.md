# Detecker - Containerized Black Duck Detect
Detecker is a way of running Black Duck Detect inside a Docker container, so that it may be executed in a cloud-hosted environment without consuming any client-side resources.

# Usage

Build the Docker container
- To enable scanning with the latest version of Detect,
```-- docker build -t detecker .```
- To enable scanning with a different version of Detect,
```-- docker build --build-arg detect_ver=6.3.0 -t detecker .```

Once the container is built, you can then run the Docker container

You can specify the following arguments:
- --project or -p [optional] : Black Duck Project Name. If not specified, the script will obtain the project name from the Source Code
- --version or -v [optional] : Black Duck Version. If not specified, the script will obtain the project version from the Source Code
- --source or -s : Git URL from where to obtain the Source Code
- --key or -k : Black Duck API Key. Needs to have both Read and Write permissions

Example
```sh
docker run --rm --name "detecker" -it detecker -e --source=https://github.com/OWASP/NodeGoat.git --project=MJ-NodeGoat --key={redacted}
```