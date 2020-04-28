FROM gcr.io/wise-cycling-267806/multiqc
USER root
WORKDIR /home/bioinfo/tax
COPY reads_qza/reads_trimmed.qza reads_qza
COPY reads_qza/reads_trimmed_summary.qzv reads_qza
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
