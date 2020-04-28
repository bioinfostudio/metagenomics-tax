FROM gcr.io/wise-cycling-267806/join-paired
USER root
COPY reads_qza/reads_trimmed_joined_filt.qza reads_qza
COPY reads_qza/reads_trimmed_joined_filt_summary.qzv reads_qza
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
