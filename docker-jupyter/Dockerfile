FROM fedora-minimal:39

VOLUME [ "/workspace", "/config", "/data" ]
RUN mkdir /opt/kernels

COPY requirements.txt  requirements.txt
COPY reqpyspark330.txt  reqpyspark330.txt

COPY jupyter_notebook_config.py /config/jupyter_notebook_config.py

RUN microdnf -y install pip python tree cmake gcc g++ git gcc g++ git java-11-openjdk nodejs

ENV JAVA_HOME=/usr/lib/jvm/jre

RUN pip install --upgrade cffi setuptools pip pypandoc && pip install --no-cache-dir -r requirements.txt && jupyter lab build --dev-build=False --mimimize=True

RUN python3 -m venv /opt/kernels/spark330 && /opt/kernels/spark330/bin/pip install --upgrade pip && /opt/kernels/spark330/bin/pip install ipykernel && /opt/kernels/spark330/bin/python -m ipykernel install --name "spark330" --display-name "pyspark3.3.0" && /opt/kernels/spark330/bin/pip install -r reqpyspark330.txt

RUN microdnf -y install azure-cli

WORKDIR /workspace

EXPOSE 8888/tcp
EXPOSE 4040/tcp

CMD [ "jupyter", "lab", "--config", "/config/jupyter_notebook_config", "--allow-root" ]
