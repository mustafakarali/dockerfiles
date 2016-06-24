FROM eboraas/apache:stable
MAINTAINER Daniel

RUN apt-get update && apt-get -y install php5 && apt-get clean

EXPOSE 80
EXPOSE 443

RUN cp /etc/apache2/mods-available/socache_shmcb.load /etc/apache2/mods-enabled/

# hack for pid error stopping container from running
ADD startup.sh /startup.sh
RUN chmod -v +x /startup.sh
CMD ["/startup.sh"]
