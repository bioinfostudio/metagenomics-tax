FROM gcr.io/wise-cycling-267806/tabulate
USER root
COPY deblur_table_final.qza deblur_output
COPY rep_seqs_final.qza deblur_output
COPY 16S rRNA_db/16S
RUN chown -R bioinfo:bioinfo /home/bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
ENV METADATA "/home/bioinfo/tax/metadata.txt"
