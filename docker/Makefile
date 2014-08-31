DOCKER_CMD=docker run -p 2222:22 -p 80:80 -v /Users/***REMOVED***/dev/dailyimpactfact/web:/usr/share/nginx/html:ro
DOCKER_IMG=dailyimpactfact_v1

build:
	docker build --no-cache=false -t ${DOCKER_IMG} .

run:
	${DOCKER_CMD} -d ${DOCKER_IMG}

interactive:
	${DOCKER_CMD} -t -i ${DOCKER_IMG}

bash:
	${DOCKER_CMD} ${DOCKER_IMG} /bin/bash

clean:
	docker rm $(docker ps -aq)
