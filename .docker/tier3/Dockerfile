FROM dmoj/runtimes-tier3

ARG TAG=master
RUN mkdir /judge /problems && cd /judge && \
	curl -LJO https://github.com/electroBakuza/judge-server/archive/refs/heads/master.zip && unzip judge-server-master.zip && \
    rm judge-server-master.zip && cd judge-server-master && python3 -m venv --prompt=DMOJ /env && \
	/env/bin/pip3 install cython && \
	/env/bin/pip3 install -e . && \
	/env/bin/python3 setup.py develop && \
	HOME=~judge . ~judge/.profile && \
	runuser -u judge -w PATH -- /env/bin/dmoj-autoconf -V > /judge-runtime-paths.yml && \
	echo '  crt_x86_in_lib32: true' >> /judge-runtime-paths.yml

ENTRYPOINT ["/usr/bin/tini", "--", "/judge/judge-server-master/.docker/entry"]
