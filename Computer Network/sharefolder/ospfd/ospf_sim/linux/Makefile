
vpath %.C ../../src:../../linux:..
vpath %.c ../../src/contrib

#--Edite by M
#INSTALL_DIR = /usr/local/bin
#CGI_DIR = /home/httpd/cgi-bin
INSTALL_DIR = ${HOME}/Local/bin
CGI_DIR = ${HOME}/httpd/cgi-bin
CC = g++
#CPPFLAGS = -I. -I../../src -I../../linux -I.. 
CPPFLAGS = -I. -I../../src -I../../linux -I.. -I${HOME}/Local/include -L${HOME}/Local/lib
CFLAGS = -O -g -Wall -Woverloaded-virtual -Wcast-qual -Wuninitialized
CXXFLAGS = -O -g -Wall -Woverloaded-virtual -Wcast-qual -Wuninitialized
LDFLAGS = 

OBJS	= asbrlsa.o \
	  asexlsa.o \
	  avl.o \
	  cksum.o \
	  config.o \
	  dbage.o \
	  grplsa.o \
	  hostmode.o \
	  ifcfsm.o \
	  lsa.o \
	  lsalist.o \
	  lsdb.o \
	  monitor.o \
	  mospf.o \
	  mtrace.o \
	  nbrfsm.o \
	  netlsa.o \
	  ospf.o \
	  pat.o \
	  phyint.o \
	  priq.o \
	  rte.o \
	  rtrlsa.o \
	  spfack.o \
	  spfarea.o \
	  spfcalc.o \
	  spfdd.o \
	  spfhello.o \
	  spfifc.o \
	  spflood.o \
	  spfnbr.o \
	  spforig.o \
	  spfutil.o \
	  spfvl.o \
	  summlsa.o \
	  timer.o \
	  md5c.o \
	  linux.o \
	  ospfd_sim.o \
	  tcppkt.o \
	  sim_system.o


install:  ospf_sim ospfd_sim ospfd_mon ospfd_browser
	install ospf_sim ${INSTALL_DIR}
	install ospfd_sim ${INSTALL_DIR}
	install ospfd_mon ${INSTALL_DIR}
	install ospfd_browser ${CGI_DIR}
	cp ../ospf_sim.tcl ${INSTALL_DIR}

ospfd_sim: ${OBJS}

ospfd_mon: tcppkt.o lsa_prn.o

ospf_sim: tcppkt.o avl.o pat.o sim_linux.o ../sim.C
	g++ tcppkt.o avl.o pat.o sim_linux.o ../sim.C -ltcl8.0 -ltk8.0 \
	${CPPFLAGS} ${CXXFLAGS} -DINSTALL_DIR=\"${INSTALL_DIR}\" \
	-L/usr/X11R6/lib -lX11 -lm -ldl -o ospf_sim

ospfd_browser:	tcppkt.o pat.o lsa_prn.o

clean:
	rm -rf .depfiles
	rm -f *.o ospf_sim ospfd_sim ospfd_mon ospfd_browser

# Stuff to automatically maintain dependency files

.c.o:
	gcc -MD $(CFLAGS) $(CPPFLAGS) -c $<
	@mkdir -p .depfiles ; mv $*.d .depfiles

.C.o:
	g++ -MD $(CXXFLAGS) $(CPPFLAGS) -c $<
	@mkdir -p .depfiles ; mv $*.d .depfiles

-include $(OBJS:%.o=.depfiles/%.d)
