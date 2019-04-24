FROM decinho13/base-notebook:ros-tf

RUN chgrp -R 0 /home/jovyan && \
    chmod -R g=u /home/jovyan
RUN chmod g=u /etc/passwd
ENTRYPOINT [ "uid_entrypoint" ]
USER 1001
