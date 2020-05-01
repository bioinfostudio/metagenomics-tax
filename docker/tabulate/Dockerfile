FROM gcr.io/wise-cycling-267806/classification
USER root
COPY representative_sequences.qzv deblur_output
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
