FROM gcr.io/wise-cycling-267806/filter-samples
USER root
COPY 16S rRNA_db/16S
COPY rep_seqs_final.qza deblur_output
COPY deblur_table_final_summary.qzv deblur_output
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
