FROM gcr.io/wise-cycling-267806/deblur-output
USER root
RUN ln -s /mnt/genome/taxa_classifiers /home/bioinfo/tax/taxa_classifiers
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
