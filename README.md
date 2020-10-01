# Example for containers
Show:
- Networking
- Logging
- Config

## Starts with Docker
Build an image that embeds a script.  Script uses ENV Var to ping endpoint, outputs to `stdout`

## Moves to compose
Does all the Docker fun magically.

# Commands
- Build the project
  - `docker build -t foo:1 .`
- Run on localhost
  - `docker run --rm -e PING_COUNT=5 foo:1`
- Run as daemon
  - `docker run -d --rm --name bar -e PING_COUNT=1000 foo:1`
- Run second container to validate
  - `docker run --rm -e PING_COUNT=5 -e PING_HOST=bar foo:1`
  - (this should fail - not in addressable network)
- Inspect
  - `docker inspect bar`
  - (see network info)
- Stop
  - `docker stop bar`
- Create network
  - `docker network create foobar`
- Run in network
  - `docker run -d --rm --name bar -e PING_COUNT=1000 --network=foobar foo:1`
- Check addressable with second container
  - `docker run --rm -e PING_COUNT=5 -e PING_HOST=bar --network=foobar foo:1`
- Confirm this is network
  - `docker run --rm -e PING_COUNT=5 -e PING_HOST=bar foo:1`
  - (should still fail)
- See logs
  - `docker logs bar`

# License
This project is licensed under the Apache-2.0.