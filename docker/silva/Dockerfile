FROM gcr.io/wise-cycling-267806/deblur
USER root
COPY deblur_table_summary.qzv deblur_output
RUN ln -s /mnt/genome/taxa_classifiers /home/bioinfo/tax/taxa_classifiers
COPY taxa taxa
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
