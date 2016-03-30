FROM centos:centos7
MAINTAINER Ibtissam Taibi

# Update base images.
RUN yum distribution-synchronization -y

# Install EPEL, MySQL, Zabbix release packages.
RUN yum install -y epel-release
RUN yum install -y http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/zabbix-release-3.0-1.el7.noarch.rpm
RUN yum makecache

# Installing SNMP Utils
RUN yum -y -q install net-snmp-devel net-snmp-libs net-snmp net-snmp-perl net-snmp-python net-snmp-utils

# Install zabbix server and php frontend
RUN yum install -y --nogpgcheck http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/zabbix-server-mysql-3.0.0-1.el7.x86_64.rpm
#ADD ./zabbix/zabbix-server-mysql-3.0.1-1.el7.x86_64.rpm /tmp/zabbix-server-mysql-3.0.1-1.el7.x86_64.rpm
#RUN yum -y -q localinstall --nogpgcheck /tmp/zabbix-server-mysql-3.0.1-1.el7.x86_64.rpm

# Cleaining up.
RUN yum clean all

# Zabbix Conf Files
ADD ./zabbix/zabbix_server.conf /etc/zabbix/zabbix_server.conf
#RUN chmod 777 /etc/zabbix/zabbix_server.conf
#RUN groupadd zabbix
#RUN useradd -g zabbix zabbix
#RUN useradd zabbixnew
#RUN chown zabbixnew:zabbixnew /etc/zabbix/zabbix_server.conf
#RUN chown -R zabbixnew:zabbixnew /var/log/zabbix
#RUN chown -R zabbixnew:zabbixnew /var/run/zabbix

# Enable networking
RUN echo "NETWORKING=yes" > /etc/sysconfig/network

# Expose the Zabbix Server port 10051
EXPOSE 10051
#RUN su zabbix
# Start the custom zabbix_server binary in foreground mode ( -f )
CMD ["/usr/sbin/zabbix_server","-f","-c", "/etc/zabbix/zabbix_server.conf"]
