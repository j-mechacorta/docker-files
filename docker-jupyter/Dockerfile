FROM fedora-minimal:40

VOLUME [ "/workspace", "/config", "/data" ]
RUN mkdir /opt/kernels

COPY requirements.txt  requirements.txt

COPY jupyter_notebook_config.py /config/jupyter_notebook_config.py

RUN microdnf -y install pip python3 tree cmake gcc g++ git gcc g++ git java-11-openjdk nodejs

ENV JAVA_HOME=/usr/lib/jvm/jre

RUN pip install --upgrade cffi setuptools pip pypandoc && pip install --no-cache-dir -r requirements.txt && jupyter lab build --dev-build=False --mimimize=True

RUN microdnf -y install azure-cli

WORKDIR /workspace

EXPOSE 8888/tcp
EXPOSE 4040/tcp

CMD [ "jupyter", "lab", "--config", "/config/jupyter_notebook_config", "--allow-root" ]
