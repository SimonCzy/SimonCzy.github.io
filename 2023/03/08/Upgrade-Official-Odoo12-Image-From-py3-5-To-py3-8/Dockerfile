# derived from odoo:12.0 original image
FROM odoo:12.0

# install the dependencies for python3.8
USER root
RUN apt-get update && apt-get install -y default-libmysqlclient-dev build-essential git gcc make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev libldap2-dev libsasl2-dev

# install python 3.8
ENV PYENV_ROOT=/var/local/pyenv/
RUN curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
RUN /var/local/pyenv/bin/pyenv install 3.8.15 && /var/local/pyenv/bin/pyenv global 3.8.15

# change python 3.5 -> 3.8
RUN rm /usr/bin/python3 && ln -s /var/local/pyenv/shims/python3 /usr/bin/python3

# install odoo dependencies
RUN mv /usr/lib/python3/dist-packages/odoo /var/local/pyenv/versions/3.8.15/lib/python3.8/site-packages/odoo && mv /usr/lib/python3/dist-packages/odoo-12.0.post20211006.egg-info/ /var/local/pyenv/versions/3.8.15/lib/python3.8/site-packages/odoo-12.0.post20211006.egg-info/
COPY ./requirements.txt /
RUN /var/local/pyenv/shims/pip install -r /requirements.txt

USER odoo
