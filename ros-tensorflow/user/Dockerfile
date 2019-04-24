FROM decinho13/base-notebook:ros-tf
COPY . /bin
RUN chgrp -R 0 /home/jovyan && \
    chmod -R g=u /home/jovyan
RUN chmod g=u /etc/passwd

WORKDIR /bin
ENTRYPOINT [ "/bin/uid_entrypoint" ]
USER 10001
