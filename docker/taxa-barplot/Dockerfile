FROM gcr.io/wise-cycling-267806/rarefaction
USER root
COPY taxa_barplot.qzv taxa
RUN chown -R bioinfo:bioinfo /home/bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
ENV METADATA "/home/bioinfo/tax/metadata.txt"
