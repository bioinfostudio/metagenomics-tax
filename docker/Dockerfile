FROM qiime2/core
RUN apt-get update --fix-missing
RUN apt-get install -y fontconfig
RUN apt-get clean && apt-get purge && rm -rf /var/lib/apt/lists/* /tmp/*

RUN conda install -c bioconda fastqc
RUN pip install multiqc

# create a non-root user
RUN useradd -ms /bin/bash bioinfo
WORKDIR /home/bioinfo/tax
COPY raw_data raw_data
COPY metadata.txt .
# setup the user directory
RUN chown -R bioinfo:bioinfo /home/bioinfo
RUN echo 'export PS1=" \W\$ "' >> /home/bioinfo/.bashrc
# become the bioinfo
USER bioinfo
ENV HOME /home/bioinfo
WORKDIR /home/bioinfo/tax
ENV NCORES 1
