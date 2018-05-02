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

RUN rpm -q logrotate || yum install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/logrotate-3.8.6-14.el7.x86_64.rpm -y
RUN yum repolist all
RUN yum install epel-release -y || yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y
RUN yum repolist all

RUN yum install redis hostname iperf iputils net-tools telnet nc nmap -y ; yum clean all
RUN rpm -q hostname || yum install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/hostname-3.13-3.el7.x86_64.rpm -y || echo download failed
RUN rpm -q iputils || yum install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/iputils-20160308-10.el7.x86_64.rpm -y || echo download failed
RUN rpm -q net-tools || yum install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/net-tools-2.0-0.22.20131004git.el7.x86_64.rpm -y || echo download failed
RUN rpm -q telnet || yum install mirror.centos.org/centos/7/os/x86_64/Packages/telnet-0.17-64.el7.x86_64.rpm -y || echo download failed
RUN rpm -q nc || yum install mirror.centos.org/centos/7/os/x86_64/Packages/nmap-ncat-6.40-7.el7.x86_64.rpm -y || echo download failed
RUN rpm -q nmap || yum install https://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/nmap-6.40-7.el7.x86_64.rpm -y || echo download failed

COPY redis-master.conf /redis-master/redis.conf
COPY redis-slave.conf /redis-slave/redis.conf
RUN mkdir -p /redis-sentinel ; chmod -R 777 /redis-sentinel /redis-slave
COPY run.sh /run.sh

CMD [ "/run.sh" ]

ENTRYPOINT [ "bash", "-c" ]
