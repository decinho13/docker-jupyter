FROM decinho13/base-notebook:ros-tf
COPY . /home/jovyan
RUN chgrp -R 0 /home/jovyan && \
    chmod -R g=u /home/jovyan
RUN chmod g=u /etc/passwd
USER 10001
WORKDIR /home/jovyan
ENTRYPOINT [ "/home/jovyan/uid_entrypoint" ]

