GSOAP_PREFIX=/usr
GSOAP_BASE=$(GSOAP_PREFIX)/share/gsoap
GSOAP_IMPORT=$(GSOAP_BASE)/import
GSOAP_PLUGINS=$(GSOAP_BASE)/plugin
GSOAP_CFLAGS= -I gen -I $(GSOAP_PREFIX)/include -I $(GSOAP_PLUGINS)
GSOAP_LDFLAGS= -lgsoap++ -L $(GSOAP_PREFIX)/lib/

all: gen/soapC.cpp wsd-probe.exe wsd-server.exe wsd-proxy.exe

gen/soapC.cpp: 
	mkdir -p gen
	$(GSOAP_PREFIX)/bin/soapcpp2 -2Cx $(GSOAP_IMPORT)/wsdd10.h -I $(GSOAP_IMPORT) -d gen

wsd-probe.exe:   $(GSOAP_PLUGINS)/wsddapi.c $(GSOAP_PLUGINS)/wsaapi.c  gen/soapC.cpp gen/soapClient.cpp probe.cpp 
	c++ -g -o $@ $^ $(GSOAP_LDFLAGS) $(GSOAP_CFLAGS) 
	
wsd-server.exe:   $(GSOAP_PLUGINS)/wsddapi.c $(GSOAP_PLUGINS)/wsaapi.c gen/soapC.cpp gen/soapClient.cpp wsd-server.cpp server.cpp
	c++ -g -o $@ $^ $(GSOAP_LDFLAGS) $(GSOAP_CFLAGS) 

wsd-proxy.exe:   $(GSOAP_PLUGINS)/wsddapi.c $(GSOAP_PLUGINS)/wsaapi.c  gen/soapC.cpp gen/soapClient.cpp proxy.cpp
	c++ -g -o $@ $^ $(GSOAP_LDFLAGS) $(GSOAP_CFLAGS) 
	
	
clean:
	rm -rf *.exe gen


