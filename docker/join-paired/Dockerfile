FROM gcr.io/wise-cycling-267806/trim-paired
USER root
COPY reads_joined.qza reads_qza
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
