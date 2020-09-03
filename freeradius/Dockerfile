FROM ubuntu:18.04
RUN apt-get update
RUN apt-get install -y freeradius wget libwww-perl build-essential
RUN wget https://raw.githubusercontent.com/privacyidea/FreeRADIUS/master/privacyidea_radius.pm
RUN cp privacyidea_radius.pm /etc/freeradius/3.0/mods-config/perl
RUN PERL_MM_USE_DEFAULT=1 cpan install Config::IniFiles JSON
COPY rlm_perl.ini /etc/freeradius/rlm_perl.ini
COPY perl /etc/freeradius/3.0/mods-available/perl
COPY authorize /etc/freeradius/3.0/mods-config/files/authorize
COPY default /etc/freeradius/3.0/sites-available/default
RUN chown freerad.freerad \
/etc/freeradius/3.0/mods-available/perl \
/etc/freeradius/3.0/mods-config/files/authorize \
/etc/freeradius/3.0/sites-available/default \
/etc/freeradius/rlm_perl.ini
RUN ln -s /etc/freeradius/3.0/mods-available/perl /etc/freeradius/3.0/mods-enabled/
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get remove -y build-essential
CMD freeradius -f -l /tmp/log -XX