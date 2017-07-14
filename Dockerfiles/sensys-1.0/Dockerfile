FROM intelctrlsys/sensys-bld-centos7.3

RUN yum install -y net-snmp-devel libesmtp-devel && \
    wget https://github.com/intel-ctrlsys/sensys/releases/download/v1.0.0/sensys-1.0.src.rpm && \
    rpmbuild --rebuild sensys-1.0.src.rpm && \
    cd ~/rpmbuild/RPMS/x86_64 && \
    rpm -ivh sensys-*.rpm --nodeps
