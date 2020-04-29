FROM gcr.io/wise-cycling-267806/join-paired
USER root
COPY deblur_output deblur_output
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
