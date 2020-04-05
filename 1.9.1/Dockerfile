FROM comics/centos8
MAINTAINER Ian Merrick <MerrickI@Cardiff.ac.uk>

##############################################################
# Software:             MITObim
# Software Version:     1.9.1
# Software Website:     https://github.com/chrishah/MITObim
# Description:          mitochondrial baiting and iterative mapping
##############################################################

RUN  dnf install -y boost-devel \
                    bzip2       \
                    bzip2-devel \
                    expat-devel \
                    flex        \
                    gperftools-devel \
                    vim-common  \
                    zlib-devel && \
     curl -L https://jaist.dl.sourceforge.net/project/mira-assembler/MIRA/stable/mira-4.0.2.tar.bz2 | tar xjf - && \
     cd mira-4.0.2 && \
     sed -i '/^#include "ads.H"/a #include <math.h>' src/mira/ads.C && \
     sed -i '/^#include <boost\/filesystem.hpp>/a #include <iostream>' src/progs/quirks.C && \
     CXXFLAGS="-fpermissive" CFLAGS="-fpermissive" ./configure && \
     make || ( make clean && CXXFLAGS="-fpermissive" CFLAGS="-fpermissive" ./configure && make ) && \
     make install && \
     mkdir -p /usr/share/licenses/mira_4.0.2/ && \
     mv COPYING /usr/share/licenses/mira_4.0.2/  && \
     cd .. && \
     rm -rf mira* && \
     dnf clean all && \
     rm -rf /var/cache/dnf/
     
     

RUN curl -L https://github.com/chrishah/MITObim/archive/v1.9.1.tar.gz | tar xzf - && \
    chmod 755 MITObim-1.9.1/MITObim.pl && \
    mv MITObim-1.9.1/MITObim.pl /usr/local/bin/ && \
    mkdir /usr/share/MITObim-1.9.1/ && \
    mv MITObim-1.9.1/LICENSE /usr/share/MITObim-1.9.1/    && \
    rm -rf MITO*
CMD ["/bin/bash"]

