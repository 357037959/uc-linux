FROM insideo/uc-linux:hydrogen
MAINTAINER ccondit@randomcoder.com

ADD control /control
RUN \
	mkdir -p /build /control /download /packages && \
	opkg update && \
	opkg install gcc make file linux-devel libbz2-devel && \
	wget -O /download/zip30.tar.gz \
		http://downloads.sourceforge.net/project/infozip/Zip%203.x%20%28latest%29/3.0/zip30.tar.gz && \
	cd /build && \
	tar xf /download/zip30.tar.gz && \
	cd zip30 && \
	make -f unix/Makefile generic && \
	pre-root /build/zip-root && \
	make -f unix/Makefile prefix=/build/zip-root/usr install && \
	post-root /build/zip-root && \
	cd /build/zip-root && \
	rm -rf usr/man && \
	(strip --strip-unneeded usr/bin/* || true) && \
	mv usr/bin/zip usr/bin/zip.zip && \
	mv usr/bin/zipcloak usr/bin/zipcloak.zip && \
	mv usr/bin/zipnote usr/bin/zipnote.zip && \
	mv usr/bin/zipsplit usr/bin/zipsplit.zip && \
	make-deb \
		/build/zip-deb \
		/build/zip-root \
		/control/zip \
		/packages/zip_3.0-1_amd64.deb

