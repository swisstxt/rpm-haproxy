# A Recipe for a haproxy 1.6.4 stable version RPM on CentOS

Perform the following on a build box as a regular user.

## Create an RPM Build Environment

Install rpmdevtools from the [EPEL][epel] repository:

    sudo yum install rpmdevtools pcre-devel
    rpmdev-setuptree

## Install Prerequisites for RPM Creation

    sudo yum groupinstall 'Development Tools'
    sudo yum install openssl-devel

## Download haproxy

    wget http://www.haproxy.org/download/1.6/src/haproxy-1.6.4.tar.gz
    mv haproxy-1.6.4.tar.gz rpmbuild/SOURCES/

## Get Necessary System-specific Configs

    git clone git@github.com:ITV/rpm-haproxy.git
    cp haproxy-centos/SOURCES/* rpmbuild/SOURCES/
    cp haproxy-centos/SPECS/* rpmbuild/SPECS/

## Build the RPM

    cd rpmbuild/
    rpmbuild -ba SPECS/haproxy.spec

The resulting RPM will be in ~/rpmbuild/RPMS/x86_64

## Credits

Based on the Red Hat 6.4 RPM spec for haproxy 1.4.

Maintained by [Russ Clare](russ.clare@itv.com)

[EPEL]: http://fedoraproject.org/wiki/EPEL#How_can_I_use_these_extra_packages.3F

Forked from https://github.com/swisstxt/rpm-haproxy (1.6 Dev support) which was Forked from https://github.com/bluerail/haproxy-centos (1.5 Stable support)

