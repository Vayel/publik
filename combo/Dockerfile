FROM julienbayle/publik:latest-base

MAINTAINER Julien BAYLE <julien.bayle@loire-atlantique.fr>

# INSTALL COMBO
# + python3-django and python3-cryptography backports needed for combo
RUN apt-get update \
    && apt-get -t stretch-backports install -y python3-django python3-cryptography \
    && apt-get install -y --no-install-recommends \
       postgresql- \
       combo \
       publik-base-theme \
    && rm -rf /var/lib/apt/lists/*

# COMBO CONFIG
COPY combo.settings.py /etc/combo/settings.d/loire-atlantique.py
RUN cp /tmp/secret /etc/combo \
    && chmod 755 /etc/combo/secret

# NGINX CONFIG
COPY nginx.template /etc/nginx/conf.d/combo.template

# USEFULL TO BE ABLE TO RUN THE MANAGER 
RUN usermod combo -s /bin/bash

COPY start.sh stop.sh /usr/local/bin/
ENTRYPOINT ["start.sh"]

EXPOSE 8080 
CMD ["/bin/bash"]
