# azure-pipelines-docker-agent
[![Build Status](https://dev.azure.com/ofcoursedude/ofcoursedude/_apis/build/status/ofcoursedude.azure-pipelines-docker-agent?branchName=master)](https://dev.azure.com/ofcoursedude/ofcoursedude/_build/latest?definitionId=100&branchName=master)

A bunch of dev tools packed in an azure pipelines agent for docker:
- Ubuntu 20.04 LTS
- .Net Core 3.1 LTS
- NodeJS 12 LTS
- Golang 1.15
- [build-essential apt package](https://packages.ubuntu.com/focal/devel/build-essential)
- Docker CLI for Docker in Docker builds

### In a nutshell
To start standard agent, run:

`docker run -e AZP_URL=https://dev.azure.com/YOUR_AZURE -e AZP_TOKEN=YOUR_ACCESS_TOKEN -d ofcoursedude/azure-pipelines-docker-agent `

To start an agent that can build also run docker builds:

`docker run -v /var/run/docker.sock:/var/run/docker.sock -e AZP_URL=https://dev.azure.com/YOUR_AZURE -e AZP_TOKEN=YOUR_ACCESS_TOKEN -d ofcoursedude/azure-pipelines-docker-agent `

With a little bit of extra sugar:

`docker run -v /var/run/docker.sock:/var/run/docker.sock --restart=unless-stopped -h docker-1 -e AZP_URL=https://dev.azure.com/YOUR_AZURE -e AZP_TOKEN=YOUR_ACCESS_TOKEN -d --name buildagent ofcoursedude/azure-pipelines-docker-agent `

For additional documentation on image configuration, head to https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops
