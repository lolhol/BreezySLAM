ifeq ("$(shell uname)","Darwin")
  LIBEXT = dylib
  LIBPATH = /Library/Java/Extensions
  JARPATH = /Library/Java/Extensions
else ifeq ("$(shell uname)","Linux")
  LIBEXT = so
  LIBPATH = /usr/lib/jni
  JARPATH = /usr/share/java
else
  LIBEXT = dll
  LIBPATH = C:/Program Files/Java
  JARPATH = C:/Program Files/Java
endif

all: jar

jar: build pack

build:
	cd edu/wlu/cs/levy/breezyslam; (cd algorithms && make); (cd components && make)

install: jar
	install -m 755 edu/wlu/cs/levy/breezyslam/algorithms/libjnibreezyslam_algorithms.$(LIBEXT) $(LIBPATH)
	install -m 755 edu/wlu/cs/levy/breezyslam/components/libjnibreezyslam_components.$(LIBEXT) $(LIBPATH)
	install -m 644 BreezySLAM.jar $(JARPATH)

uninstall:
	rm -f $(LIBPATH)/libjnibreezyslam_algorithms.$(LIBEXT)
	rm -f $(LIBPATH)/libjnibreezyslam_components.$(LIBEXT)
	rm -f $(JARPATH)/BreezySLAM.jar

pack:
	rm -f BreezySLAM.jar
	find . -name "*.class" | xargs jar cvf BreezySLAM.jar
	(cd edu/wlu/cs/levy/breezyslam/algorithms && jar uvf ../../../../../../BreezySLAM.jar *.$(LIBEXT))
	(cd edu/wlu/cs/levy/breezyslam/components && jar uvf ../../../../../../BreezySLAM.jar *.$(LIBEXT))
	rm -f *.tmp

clean:
	rm -f BreezySLAM.jar
	cd edu/wlu/cs/levy/breezyslam; (cd algorithms && make clean); (cd components && make clean)
