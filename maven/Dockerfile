FROM insideo/uc-linux:hydrogen
MAINTAINER ccondit@randomcoder.com

ADD control /control
RUN \
	mkdir -p /build /control /download /packages && \
	wget -O /download/apache-maven-3.3.9-bin.tar.gz \
		http://www.us.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz && \
	cd /build && \
	tar xf /download/apache-maven-3.3.9-bin.tar.gz && \
	cd apache-maven-3.3.9 && \
	pre-root /build/maven-root && \
	mkdir -p /build/maven-root/usr/share/maven && \
	cp -a . /build/maven-root/usr/share/maven/ && \
	post-root /build/maven-root && \
	cd /build/maven-root && \
	make-deb \
		/build/maven-deb \
		/build/maven-root \
		/control/maven \
		/packages/maven_3.3.9-1_all.deb

