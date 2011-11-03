

SPK_NAME = git
SPK_VERS = 1.7.7.2
SPK_REV = 1
SPK_ICON = src/openssh.png

DEPENDS = cross/$(SPK_NAME)

MAINTAINER = packages@packages.nas-forum.com
COMMENT    = "git stuff"
RELOAD_UI = no
DISPLAY_NAME = Git

HOMEPAGE   = http://git-scm.com/
LICENSE    = 

INSTALLER_SCRIPT = src/installer.sh
SSS_SCRIPT       = src/start-stop-status
ADDITIONAL_SCRIPTS = 

INSTALL_PREFIX = /usr/local/$(SPK_NAME)
PRE_COPY_TARGET = install-openssh
COPY_TARGET = nop
STRIP_TARGET = myStrip

include ../../mk/spksrc.spk.mk

.PHONY: install-openssh
install-openssh:
	install -m 755 -d $(STAGING_DIR)/log
	install -m 755 -d $(STAGING_DIR)/bin
	install -m 755 src/bin/*.pl $(STAGING_DIR)/bin/
	install -m 755 $(INSTALL_DIR)/usr/local/bin/scp $(STAGING_DIR)/bin/
	install -m 755 $(INSTALL_DIR)/usr/local/bin/sftp $(STAGING_DIR)/bin/

.PHONY: myStrip 
myStrip:
	@$(RUN) $(STRIP) $(STAGING_DIR)/bin/scp
	@$(RUN) $(STRIP) $(STAGING_DIR)/bin/sftp