FROM gcr.io/wise-cycling-267806/table-filt
USER root
COPY deblur_table_filt_contam.qza deblur_output
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
