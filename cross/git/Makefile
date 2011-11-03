
#http://git-core.googlecode.com/files/git-1.7.7.2.tar.gz

PKG_NAME = git
PKG_VERS = 1.7.7.2
PKG_EXT = tar.gz
PKG_DIST_NAME = $(PKG_NAME)-$(PKG_VERS).$(PKG_EXT)
PKG_DIST_SITE = http://git-core.googlecode.com/files/
PKG_DIR = $(PKG_NAME)-$(PKG_VERS)

DEPENDS = 
# cross/zlib cross/openssl

MAINTAINER=	packages@packages.nas-forum.com
HOMEPAGE=	http://git-scm.com/
COMMENT=	Open source version of SSH connectivity tools
LICENSE=	

DESTDIR = $(INSTALL_DIR)

CONFIGURE_TARGET = myConfigure
INSTALL_TARGET = myInstall

include ../../mk/spksrc.cross-cc.mk

.PHONY: myConfigure
myConfigure:
	@$(RUN) LD=$(CC) LDFLAGS=" -L$(STAGING_INSTALL_PREFIX)/lib " CFLAGS=" -I$(STAGING_INSTALL_PREFIX)/include -O " ./configure $(TC_CONFIGURE_ARGS)	--disable-lastlog --disable-utmp --disable-utmpx --disable-wtmp --disable-wtmpx --disable-strip --with-zlib=$(STAGING_INSTALL_PREFIX) --with-ssl-dir=$(STAGING_INSTALL_PREFIX)

.PHONY: myInstall
myInstall:
	$(RUN) $(MAKE) install DESTDIR=$(INSTALL_DIR)


