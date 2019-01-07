FROM i386/ubuntu:18.04

EXPOSE 28960/udp

WORKDIR /srv/cod4

VOLUME /srv/cod4/main \
       /srv/cod4/zone \
       /srv/cod4/mods \
       /srv/cod4/usermaps \
       /srv/cod4/main_shared \
       /srv/cod4/config

RUN useradd --home-dir /srv/cod4 cod4

COPY --chown=cod4 cod4-linux-server1.7/* ./
COPY --chown=cod4 start_server.sh ./entrypoint.sh
COPY --chown=cod4 server.cfg ./config/

RUN chown -R cod4 . && \
    chmod 700 . && \
    chmod -R 400 ./* && \
    chmod 500 ./entrypoint.sh ./cod4_lnxded && \
    chmod -R 700 ./main ./mods

USER cod4

ENTRYPOINT [ "/srv/cod4/entrypoint.sh" ]
CMD +set net_port "28960"+set sv_punkbuster "0"+set sv_pure "0"+exec "../config/server.cfg"+map_rotate