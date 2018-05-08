# Copyright 2016 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM rhel7

RUN cat /proc/cpuinfo
RUN df -h / /tmp
RUN time dd if=/dev/zero of=/tmp/grr count=10000000 && rm -f /tmp/grr
RUN rm -f /tmp/grr
RUN df -h / /tmp
RUN uptime
RUN free -g
RUN date
RUN rpm -q logrotate || yum -v install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/logrotate-3.8.6-14.el7.x86_64.rpm -y
RUN date
RUN yum -v repolist all
RUN date
RUN yum -v install epel-release -y || yum -v install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y
RUN date
RUN yum -v repolist all

RUN date
RUN yum -v install redis hostname -y ; yum -v clean all
RUN date
RUN yum -v install redis hostname iperf iputils net-tools telnet nc nmap -y ; yum -v clean all
RUN date
RUN rpm -q hostname || yum -v install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/hostname-3.13-3.el7.x86_64.rpm -y || echo download failed
RUN date
RUN rpm -q iputils || yum -v install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/iputils-20160308-10.el7.x86_64.rpm -y || echo download failed
RUN date
RUN rpm -q net-tools || yum -v install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/net-tools-2.0-0.22.20131004git.el7.x86_64.rpm -y || echo download failed
RUN date
RUN rpm -q telnet || yum -v install mirror.centos.org/centos/7/os/x86_64/Packages/telnet-0.17-64.el7.x86_64.rpm -y || echo download failed
RUN date
RUN rpm -q nc || yum -v install mirror.centos.org/centos/7/os/x86_64/Packages/nmap-ncat-6.40-7.el7.x86_64.rpm -y || echo download failed
RUN date
RUN rpm -q nmap || yum -v install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/nmap-6.40-7.el7.x86_64.rpm -y || echo download failed
RUN date
RUN uptime
RUN free -g

COPY redis-master.conf /redis-master/redis.conf
COPY redis-slave.conf /redis-slave/redis.conf
RUN mkdir -p /redis-sentinel ; chmod -R 777 /redis-sentinel /redis-slave
COPY run.sh /run.sh

CMD [ "/run.sh" ]

ENTRYPOINT [ "bash", "-c" ]
