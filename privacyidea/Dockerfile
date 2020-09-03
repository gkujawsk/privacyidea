FROM ubuntu:18.04
RUN apt-get update
RUN apt-get install -y libjpeg-dev libz-dev python-dev libffi-dev libssl-dev libxslt1-dev libpq-dev python-pip
RUN rm -rf /var/lib/apt/lists/*
RUN pip install privacyidea && pip install "cbor2==5.0.1"
RUN pi-manage create_enckey && pi-manage create_audit_keys && pi-manage createdb
RUN pi-manage admin add admin -e admin@localhost -p Csco100c
ENTRYPOINT pi-manage runserver --host=0.0.0.0