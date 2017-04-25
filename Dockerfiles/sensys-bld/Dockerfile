FROM centos:centos7.3.1611

RUN yum install -y epel-release && \
    yum install -y wget unzip tar git gcc m4 gcc-c++ make flex libtool-ltdl openssl \
                   openssl-devel cmake unixODBC unixODBC-devel xz patch perl-CPAN perl-devel \
                   rpm-build libtool autoconf automake libesmtp zeromq zeromq-devel libcurl-devel munge-devel \
    && wget http://vault.centos.org/6.8/os/Source/SPackages/sigar-1.6.5-0.4.git58097d9.el6.src.rpm && \
       rpmbuild --rebuild ./sigar-1.6.5-0.4.git58097d9.el6.src.rpm && \
       rm -rf sigar-1.6.5* && \
       yum -y localinstall /root/rpmbuild/RPMS/x86_64/sigar-1.6.5-0.4.git58097d9.el7.centos.x86_64.rpm \
                           /root/rpmbuild/RPMS/x86_64/sigar-devel-1.6.5-0.4.git58097d9.el7.centos.x86_64.rpm \
    && wget https://sourceforge.net/projects/net-snmp/files/net-snmp/5.7.3/net-snmp-5.7.3.tar.gz && \
        tar xf net-snmp-5.7.3.tar.gz && pushd net-snmp-5.7.3 && \
        ./configure --prefix=/usr --with-default-snmp-version=3 --with-sys-contact=@@no.where --with-sys-location=Unknown \
        --with-logfile=/var/log/snmpd.log --with-persistent-directory=/var/net-snmp && \
        make && make install && popd && \
        rm -rf net-snmp-5.7.3* \
    && wget http://ipmiutil.sourceforge.net/FILES/archive/ipmiutil-2.9.6-1.src.rpm && \
        rpm -iv ./ipmiutil-2.9.6-1.src.rpm && rm ipmiutil-2.9.6-1.src.rpm \
    && sed -i '/^%configure/ s/$/ --enable-libsensors/' /root/rpmbuild/SPECS/ipmiutil.spec \
    && rpmbuild -bb --clean --rmsource --rmspec /root/rpmbuild/SPECS/ipmiutil.spec && \
       yum localinstall -y /root/rpmbuild/RPMS/x86_64/ipmiutil-2.9.6-1.el7.centos.x86_64.rpm \
                           /root/rpmbuild/RPMS/x86_64/ipmiutil-devel-2.9.6-1.el7.centos.x86_64.rpm && \
       rm -rf /root/rpmbuild/* \
    && yum localinstall -y http://yum.postgresql.org/9.3/redhat/rhel-7-x86_64/pgdg-centos93-9.3-3.noarch.rpm && \
        yum install -y postgresql93-server postgresql93-odbc postgresql93-devel \
    && wget https://github.com/google/googletest/archive/release-1.7.0.tar.gz  && tar xf release-1.7.0.tar.gz && \
         pushd googletest-release-1.7.0 && \
         pushd make && \
         make gtest_main.a && \
         install --directory /usr/local/lib && \
         install -m 644 gtest_main.a /usr/local/lib/libgtest_main.a && \
         popd && \
         install --directory /usr/local/include/gtest/internal && \
         install -m 644 include/gtest/*.h /usr/local/include/gtest && \
         install -m 644 include/gtest/internal/*.h /usr/local/include/gtest/internal && \
         popd && rm -rf googletest-release-1.7.0* \
    && curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" && \
       python get-pip.py && \
       rm get-pip.py && \
       pip install -U SQLAlchemy && \
       pip install -U pytest && \
       pip install -U mock && \
       pip install -U coverage
