FROM gcr.io/wise-cycling-267806/table-final
USER root
COPY asvs-tree.qza .
COPY insertion-placements.qza .
RUN chown -R bioinfo:bioinfo /home/bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
ENV METADATA "/home/bioinfo/tax/metadata.txt"
