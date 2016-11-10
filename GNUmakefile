
DESTDIR ?= 
PREFIX  ?= /usr
COMPRESS_MAN ?= yes
STRIP_BINARY ?= yes
DOCUMENTATION ?= yes

CSECFLAGS ?= -fstack-protector-all -Wall --param ssp-buffer-size=4 -D_FORTIFY_SOURCE=2 -fstack-check -DPARANOID
CFLAGS ?= -pipe -O2
CFLAGS += $(CSECFLAGS)
DEBUGCFLAGS ?= -pipe -Wall -Werror -ggdb3 -Wno-error=unused-variable $(CSECFLAGS)

CARCHFLAGS ?= -march=native

CFLAGS += -std=gnu11 $(CARCHFLAGS)

LIBS := $(shell pkg-config --libs glib-2.0) -lpthread
LDSECFLAGS ?= -Xlinker -zrelro
LDFLAGS += $(LDSECFLAGS)
INC := $(shell pkg-config --cflags glib-2.0) $(INC)

INSTDIR = $(DESTDIR)$(PREFIX)

objs=\
userchroot.o\

binary=userchroot

.PHONY: doc

all: $(objs)
	$(CC) $(NORMSYSTEMCFLAGS) $(CFLAGS) $(LDFLAGS) $(objs) $(LIBS) -o $(binary)
	chmod +s $(binary)

%.o: %.c
	$(CC) $(NORMSYSTEMCFLAGS) $(CFLAGS) $(INC) $< -c -o $@

clean:
	rm -f $(binary) $(objs)

distclean: clean

install:
	install -d "$(INSTDIR)/bin" "$(INSTDIR)/share/man/man1"
ifeq ($(DOCUMENTATION),yes)
	install -d "$(INSTDIR)/share/doc/userchroot"
	cp -a html/* "$(INSTDIR)/share/doc/userchroot/"
endif
ifeq ($(STRIP_BINARY),yes)
	strip --strip-unneeded -R .comment -R .GCC.command.line -R .note.gnu.gold-version userchroot
endif
	install -m 4755 userchroot "$(INSTDIR)"/bin/
	install -m 644 man/man1/userchroot.1 "$(INSTDIR)"/share/man/man1/
ifeq ($(COMPRESS_MAN),yes)
	rm -f "$(INSTDIR)"/share/man/man1/userchroot.1.gz
	gzip "$(INSTDIR)"/share/man/man1/userchroot.1
endif

deinstall:
	rm -f "$(INSTDIR)"/bin/userchroot "$(INSTDIR)"/share/man/man1/userchroot.1.gz "$(INSTDIR)/share/doc/userchroot"

