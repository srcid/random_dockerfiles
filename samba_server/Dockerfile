FROM debian:12

LABEL description="samba server"
LABEL version="1.0.0"

ENV SAMBA_USER="smbuser" SAMBA_PASSWD="smbpassword" SAMBA_FOLDER_NAME="shared"

RUN apt update && \
    apt install samba -y && \
    apt clean && \
    useradd -m -s /usr/sbin/nologin ${SAMBA_USER} && \
    mkdir /home/${SAMBA_USER}/${SAMBA_FOLDER_NAME} && \
    chown -R ${SAMBA_USER}:${SAMBA_USER} /home/${SAMBA_USER}/${SAMBA_FOLDER_NAME} && \
    printf "%s\n%s\n" ${SAMBA_PASSWD} ${SAMBA_PASSWD} | smbpasswd -a ${SAMBA_USER}

COPY smb.conf /etc/samba/

ENTRYPOINT [ "/usr/sbin/smbd" ]

CMD [ "--no-process-group", "-F", "-p", "445" ]

EXPOSE 445