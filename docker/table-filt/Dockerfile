FROM gcr.io/wise-cycling-267806/tabulate
USER root
COPY deblur_table_filt.qza deblur_output
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
