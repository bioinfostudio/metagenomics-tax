FROM gcr.io/wise-cycling-267806/diversity
USER root
COPY ancom_output ancom_output
RUN chown -R bioinfo:bioinfo /home/bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
ENV METADATA "/home/bioinfo/tax/metadata.txt"
