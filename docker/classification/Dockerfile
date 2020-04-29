FROM gcr.io/wise-cycling-267806/silva
USER root
COPY taxa taxa
RUN chown -R bioinfo:bioinfo /home/bioinfo
# become the bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
