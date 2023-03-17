FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y wget ca-certificates

RUN wget https://github.com/lcgamboa/picsimlab/releases/download/v0.8.12/PICSimLab_0.8.12_230120_Ubuntu_20.04.5_LTS_amd64.deb -O /tmp/PICSimLab_0.8.12_230120_Ubuntu_20.04.5_LTS_amd64.deb && \
    apt install -y /tmp/PICSimLab_0.8.12_230120_Ubuntu_20.04.5_LTS_amd64.deb && \
    rm -rf /tmp/PICSimLab_0.8.12_230120_Ubuntu_20.04.5_LTS_amd64.deb

# Add this line before the ENTRYPOINT in your Dockerfile

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*
COPY launch_picsimlab.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/launch_picsimlab.sh


ENTRYPOINT [ "/usr/local/bin/launch_picsimlab.sh" ]



