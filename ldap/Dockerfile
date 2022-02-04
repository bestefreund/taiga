FROM taigaio/taiga-back:latest

COPY ldap_config /ldap_config

RUN pip install --no-cache-dir --upgrade pip \
 && pip install --no-cache-dir taiga-contrib-ldap-auth-ext \
 && sed -i -e '/chown -R taiga:taiga \/taiga-back/{r /ldap_config' -e 'd}' /taiga-back/docker/entrypoint.sh \
 && rm -f /ldap_config
