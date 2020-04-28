FROM gcr.io/wise-cycling-267806/tax
USER root
WORKDIR /home/bioinfo/tax
COPY fastqc_out fastqc_out
COPY reads_qza reads_qza
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
