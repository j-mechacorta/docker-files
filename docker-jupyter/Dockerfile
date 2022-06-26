FROM fedora-minimal:36

VOLUME [ "/workspace", "/config", "/data" ]
RUN mkdir /opt/kernels

COPY requirements.txt  requirements.txt
COPY reqpyspark330.txt  reqpyspark330.txt
COPY reqpyspark321.txt  reqpyspark321.txt

COPY jupyter_notebook_config.py /config/jupyter_notebook_config.py

RUN microdnf -y install pip python tree python3.10 gcc g++ git gcc g++ git java-11-openjdk && microdnf -y install nodejs

ENV JAVA_HOME=/usr/lib/jvm/jre

RUN pip install --upgrade cffi setuptools pip pypandoc && pip install --no-cache-dir -r requirements.txt && jupyter lab build --dev-build=False --mimimize=True

RUN python3.10 -m venv /opt/kernels/spark330 && /opt/kernels/spark330/bin/pip install --upgrade pip && /opt/kernels/spark330/bin/pip install ipykernel && /opt/kernels/spark330/bin/python -m ipykernel install --name "spark330" --display-name "pyspark3.3.0" && /opt/kernels/spark330/bin/pip install -r reqpyspark330.txt
RUN python3.10 -m venv /opt/kernels/spark321 && /opt/kernels/spark321/bin/pip install --upgrade pip && /opt/kernels/spark321/bin/pip install ipykernel && /opt/kernels/spark321/bin/python -m ipykernel install --name "spark321" --display-name "pyspark3.2.1" && /opt/kernels/spark321/bin/pip install -r reqpyspark321.txt


WORKDIR /workspace

EXPOSE 8082/tcp

CMD [ "jupyter", "lab", "--config", "/config/jupyter_notebook_config", "--allow-root" ]
