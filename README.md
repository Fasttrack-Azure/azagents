# azagents

docker run -e AZP_URL="https://dev.azure.com/fasttrack-azure/" -e AZP_TOKEN="13trbgdjf9xJoJduj6rHacEXYweCUA13WAku4XVGTdDrAodywzrjJQQJ99BAACAAAAAJhA4EAAASAZDO5AxQ" -e AZP_POOL="fasttrack-sh-agent" -e AZP_AGENT_NAME="Docker Agent - Linux" --name "azp-agent-linux" azdevopsagent:latest