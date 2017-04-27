FROM intelctrlsys/sensys-bld-centos7.3

RUN yum install -y net-snmp-devel libesmtp-devel && \
    wget https://github.com/intel-ctrlsys/sensys/releases/download/v0.29.0/sensys-0.29.0-1.el7.src.rpm && \
    rpmbuild --rebuild sensys-0.29.0-1.el7.src.rpm && \
    cd ~/rpmbuild/RPMS/x86_64 && \
    rpm -ivh sensys-*.rpm --nodeps
