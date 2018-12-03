FROM ubuntu:16.04
MAINTAINER Hajime Tazaki <thehajime@gmail.com>

ENV HANDLER 'echo build failed. You can debug this container by running \`docker exec -it THIS_CONTAINER_ID sh\`. \(available for 1 hour\); sleep 3600'

RUN apt-get update
RUN apt-get install -y mercurial libexpat1-dev git-core build-essential bison \
    flex libssl-dev libdb-dev libpcap-dev libc6-dbg libsysfs-dev gawk indent \
    pkg-config autoconf automake sudo ccache libsaxonb-java openjdk-8-jre-headless \
	python3 python3-dev python3-setuptools bc libgoocanvas-2.0-dev wget && \
    rm -rf /var/lib/apt/lists/*

RUN useradd -ms /bin/bash ns3dce && adduser ns3dce sudo && echo -n 'ns3dce:ns3dce' | chpasswd

RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 10 || sh -c "$HANDLER"

# Enable passwordless sudo for users under the "sudo" group
RUN sed -i.bkp -e \
      's/%sudo\s\+ALL=(ALL\(:ALL\)\?)\s\+ALL/%sudo ALL=NOPASSWD:ALL/g' \
      /etc/sudoers

USER ns3dce
WORKDIR /home/ns3dce/

ENV PATH /usr/lib/ccache:${PATH}
