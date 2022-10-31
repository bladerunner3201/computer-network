
vpath %.C .:../src
vpath %.c ../src/contrib

#--Edited by M {
#INSTALL_DIR = /usr/sbin
INSTALL_DIR = ${HOME}/ospfd_assignment/bin
#}
#CGI_DIR = /home/httpd/cgi-bin
CGI_DIR = ${HOME}/httpd/cgi-bin
#--Edited by M {
CPPFLAGS = -I. -I../src -I/usr/local/include
CPPFLAGS = -I. -I../src -I/usr/local/include -I/usr/include/tcl8.6
#}
CXXFLAGS = -O -g -Wall -Woverloaded-virtual -Wcast-qual -Wuninitialized
CFLAGS = -O -g -Wall -Woverloaded-virtual -Wcast-qual -Wuninitialized

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
	  md5c.o

install: ospfd ospfd_mon ospfd_browser
	install ospfd ${INSTALL_DIR}
	install ospfd_mon ${INSTALL_DIR}
	install ospfd_browser ${CGI_DIR}
	rm -rf ${INSTALL_DIR}/ospfd.tcl
	cp ospfd.tcl ${INSTALL_DIR}

ospfd:	ospfd_linux.C linux.o system.o tcppkt.o ${OBJS}
	g++ $(CXXFLAGS) $(CPPFLAGS) ospfd_linux.C linux.o system.o \
	 tcppkt.o ${OBJS} \
	-DINSTALL_DIR=\"${INSTALL_DIR}\" -ltcl8.6 -lm -ldl -o ospfd
	#--Edited by M { -DINSTALL_DIR=\"${INSTALL_DIR}\" -ltcl8.0 -lm -ldl -o ospfd }

ospfd_mon: tcppkt.o lsa_prn.o

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

