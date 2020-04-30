FROM gcr.io/wise-cycling-267806/contaminant
USER root
COPY rep_seqs_final.qza deblur_output
COPY rarefaction_curves_test.qzv deblur_output 
COPY deblur_table_final.qza deblur_output
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
