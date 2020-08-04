Containerized Black Duck Detect - Detecker

Prerequisites:
Docker

Usage Instructions:
First, build the Docker container. To run with the latest Detect,
docker build -t detecker .

To select a different version of Detect,
docker build --build-arg detect_ver=6.3.0 -t detecker .

Then, run the Docker container,
docker run --rm --name "detecker" -it detecker -e --project <Black Duck Project Name> --version <Black Duck Project Version> --key <Black Duck API Key> --source <Git URL containing source code>
docker run --rm --name "detecker" -it detecker -e -p -v -k --key -s

--project and --version are optional. If not specified, Detect will obtain these values from the source code

E.g.
docker run --rm --name "detecker" -it detecker -e --source=https://github.com/OWASP/NodeGoat.git --project=MJ-NodeGoat --key={redacted}
will run Detect against NodeGoat.git, and scan into MJ-NodeGoat with the project version coming from Github


