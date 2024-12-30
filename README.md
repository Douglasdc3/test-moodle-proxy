# Moodle test with reverse proxy

A test repository to experiment with a Moodle deploy behind a reverse proxy

## Issue

When deploying Moodle behind a reverse proxy it detects the wrong URL and shows a error that the site is behind a reverse proxy but access directly.
This issue is caused by a detection in the config which checks the current `Host` header and compares it against the configured application URL, this causes the app stop processing the request.

## Solution

The nginx configuration needs to be changed not set the `Host` header which lets Moodle detect that it's accessed from a behind a proxy and thus let the request through.

## Example setup.

Moodle is running on port 80 accessible via `http://moodle` from inside the same docker network.

The reverse proxy is running a nginx image on port 8888 and is accessible from traefik network. 

Traefik is my main reverse proxy which performs SSL termination and forwards the request to the nginx reverse proxy.


