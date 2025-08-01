FROM quay.io/centos/centos:stream9

VOLUME [ "/workspace", "/config", "/data" ]

# 
RUN rpm --import https://packages.microsoft.com/keys/microsoft.asc && dnf install -y https://packages.microsoft.com/config/rhel/9.0/packages-microsoft-prod.rpm && dnf install -y azure-cli && dnf clean all

# Install utilities
RUN dnf install -y which zsh python3.12 tree cmake gcc g++ git gcc g++ git nodejs && dnf clean all

# Install Java
RUN dnf install -y java-21-openjdk java-21-openjdk-devel && dnf clean all
RUN dnf module -y reset nodejs && dnf module -y enable nodejs:22 && dnf module -y install nodejs:22/common && dnf clean all
RUN useradd -ms /bin/zsh jupyter
USER jupyter

WORKDIR /home/jupyter
RUN mkdir .jupyter
COPY jupyter_notebook_config.py /home/jupyter/.jupyter/jupyter_notebook_config.py

RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

RUN python3.12 -m venv .pyenv && source .pyenv/bin/activate
ENV SHELL=/usr/bin/zsh
ENV VIRTUAL_ENV=/home/jupyter/.pyenv
ENV PATH=/home/jupyter/.pyenv/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

COPY requirements.txt  requirements.txt
RUN pip install --upgrade cffi setuptools pip pypandoc && pip install --no-cache-dir -r requirements.txt
RUN jupyter lab build --dev-build=False --minimize=True

WORKDIR /workspace

EXPOSE 8888/tcp
EXPOSE 4040/tcp

ENV JAVA_HOME=/usr/lib/jvm/jre

CMD [ "jupyter", "lab", "--config", "/home/jupyter/.jupyter/jupyter_notebook_config.py"]
