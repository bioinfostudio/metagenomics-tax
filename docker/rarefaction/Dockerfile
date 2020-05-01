FROM gcr.io/wise-cycling-267806/sepp
USER root
COPY rarefaction_curves.qzv .
RUN chown -R bioinfo:bioinfo /home/bioinfo
USER bioinfo
WORKDIR /home/bioinfo/tax
ENV METADATA "/home/bioinfo/tax/metadata.txt"
