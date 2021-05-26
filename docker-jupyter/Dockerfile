FROM fedora-minimal:33

VOLUME [ "/workspace", "/config", "/config" ]
RUN mkdir /opt/kernels

COPY requirements.txt  requirements.txt
COPY reqpyspark244.txt  reqpyspark244.txt
COPY reqpyspark311.txt  reqpyspark311.txt

COPY jupyter_notebook_config.py /config/jupyter_notebook_config.py
# COPY nodejs.module /etc/dnf/modules.d/nodejs.module

RUN microdnf -y install pip python tree python3.7 gcc g++ git java-1.8.0-openjdk gcc g++ git java-1.8.0-openjdk && microdnf -y install nodejs

ENV JAVA_HOME=/usr/lib/jvm/jre

RUN pip install --upgrade cffi setuptools pip pypandoc && pip install --no-cache-dir -r requirements.txt && jupyter lab build --dev-build=False --mimimize=False


RUN python3.7 -m venv /opt/kernels/py244 && /opt/kernels/py244/bin/pip install --upgrade pip && /opt/kernels/py244/bin/pip install ipykernel && /opt/kernels/py244/bin/python -m ipykernel install --name "py244" --display-name "pyspark2.4.4" && /opt/kernels/py244/bin/pip install pypandoc && /opt/kernels/py244/bin/pip install pyspark==2.4.4
RUN python3.7 -m venv /opt/kernels/py311 && /opt/kernels/py311/bin/pip install --upgrade pip && /opt/kernels/py311/bin/pip install ipykernel && /opt/kernels/py311/bin/python -m ipykernel install --name "py311" --display-name "pyspark3.1.1" && /opt/kernels/py311/bin/pip install pyspark==3.1.1

WORKDIR /workspace

EXPOSE 8082/tcp

CMD [ "jupyter", "lab", "--config", "/config/jupyter_notebook_config", "--allow-root" ]
