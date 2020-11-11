# Detecker - Containerized Black Duck Detect
Detecker (a combination of Detect and Docker) is a way of running Black Duck Detect inside a Docker container, so that it may be executed in a cloud-hosted environment without consuming any client-side resources.

When you build the Docker container, the script will download all of the requisite dependencies for Detect to successfully capture the open source within the codebase to be scanned.

When you run the container, the source will be downloaded and additional components if required (e.g. Python or Nuget). The script will then run Detect against this downloaded source and upload the results to your Black Duck server.

## Usage
### Step 1
Build the Docker container
- To enable scanning with the latest version of Detect,
  - ```docker build -t detecker .```
- To enable scanning with a different version of Detect,
  - ```docker build --build-arg detect_ver=6.3.0 -t detecker .```

### Step 2
Once the container is built, you can then run the Docker container

You can specify the following arguments:
- --source or -s : Git URL from where to obtain the Source Code or the URL where the file to scan is located. Alternatively, you can specify --source=LOCAL to enable local file-system scanning, in which case you must also mount a volume with the parameter -v /path/to/your/code:/source 
- --key or -k : Black Duck API Key. The key needs to have both Read and Write permissions in Black Duck
- --project or -p [optional]: Black Duck Project Name. If not specified, the script will obtain the project name from the Source Code
- --version or -v [optional] : Black Duck Version. If not specified, the script will obtain the project version from the Source Code
- --config or -c [optional] : Optional configuration to invoke prior to running Detect
- --build or -b [optional] : Optionally specify a build command to invoke prior to running Detect
- --extra or -e [optional] : Extra Black Duck Detect options to add when running Black Duck Detect

#### Example 1: To scan a project directly from Github
```sh
docker run --rm --name "detecker" -it detecker -e --source=https://github.com/OWASP/NodeGoat.git \
--project=MJ-NodeGoat --key={redacted}
```

#### Example 2: To scan a project from a URL
```sh
docker run --rm --name "detecker" -it detecker -e \
--source=https://curl.haxx.se/download/curl-7.72.0.zip \
--project=MJ-Curl --version=7.72 --key={redacted}
```

#### Example 3: To scan a local folder
```sh
docker run --rm -v /Users/martin/Development/roller:/source -it detecker -e \
--source=LOCAL \s
--project=MJ-Roller --version=1.23 --key={redacted}
```
