FROM insideo/uc-linux:hydrogen
MAINTAINER ccondit@randomcoder.com

ADD control /control
RUN \
	mkdir -p /build /control /download /packages && \
	wget -O /download/kafka_2.12-1.0.0.tgz \
		http://apache.mirrors.tds.net/kafka/1.0.0/kafka_2.12-1.0.0.tgz && \
	cd /build && \
	tar xf /download/kafka_2.12-1.0.0.tgz && \
	cd kafka_2.12-1.0.0 && \
	chown -R root:root . && \
	pre-root /build/kafka-root && \
	mkdir -p /build/kafka-root/usr/share/kafka && \
	mkdir -p /build/kafka-root/usr/share/kafka/bin && \
	cp -a bin/*.sh /build/kafka-root/usr/share/kafka/bin/ && \
	mkdir -p /build/kafka-root/usr/share/kafka/libs && \
	cp -a libs/*.jar /build/kafka-root/usr/share/kafka/libs/ && \
	mkdir -p /build/kafka-root/usr/share/kafka/bin && \
	cp -a bin/*.sh /build/kafka-root/usr/share/kafka/bin/ && \
	mkdir -p /build/kafka-root/etc/kafka && \
	cp -a config/* /build/kafka-root/etc/kafka/ && \
	ln -sf ../../../etc/kafka /build/kafka-root/usr/share/kafka/config && \
	mkdir -p /build/kafka-root/var/log/kafka && \
	ln -sf ../../../var/log/kafka /build/kafka-root/usr/share/kafka/logs && \
	post-root /build/kafka-root && \
	cd /build/kafka-root && \
	mkdir -p var/lib/kafka/data && \
	rm -f usr/share/kafka/bin/zookeeper-*.sh && \
	rm -f usr/share/kafka/libs/kafka_*-javadoc.jar && \
	rm -f usr/share/kafka/libs/kafka_*-scaladoc.jar && \
	rm -f usr/share/kafka/libs/kafka_*-sources.jar && \
	rm -f usr/share/kafka/libs/kafka_*-test.jar && \
	rm -f etc/kafka/zookeeper.properties && \
	make-deb \
		/build/kafka-deb \
		/build/kafka-root \
		/control/kafka \
		/packages/kafka_1.0.0-1_all.deb

