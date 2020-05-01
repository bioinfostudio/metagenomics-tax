FROM gcr.io/wise-cycling-267806/taxa-barplot
USER root
COPY diversity diversity
RUN chown -R bioinfo:bioinfo /home/bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
ENV METADATA "/home/bioinfo/tax/metadata.txt"
