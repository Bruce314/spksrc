
SPK_NAME = SABnzbd
SPK_VERS = 0.6.15
SPK_REV = 2
SPK_ICON = src/sab2_256.png

DEPENDS  = cross/busybox cross/par2cmdline cross/sabnzbd

MAINTAINER = superzebulon@superzebulon.org
COMMENT    = "SABnzbd makes Usenet as simple and streamlined as possible by automating everything we can. All you have to do is add an .nzb. SABnzbd takes over from there, where it will be automatically downloaded, verified, repaired, extracted and filed away with zero human interaction."
ADMIN_PORT = 8080
RELOAD_UI = yes
DISPLAY_NAME = SABnzbd

HOMEPAGE   = http://sabnzbd.org/
LICENSE    = GPL

INSTALLER_SCRIPT = src/installer.sh
SSS_SCRIPT       = src/dsm-control.sh
ADDITIONAL_SCRIPTS = 

PYTHON_VERS = 26

SPK_DEPENDS = "Python${PYTHON_VERS}>=2.6.6-5"

INSTALL_PREFIX = /usr/local/sabnzbd

POST_STRIP_TARGET = xz-compress

include ../../mk/spksrc.spk.mk


ifeq ($(findstring $(ARCH),88f5281 bromolow powerpc ppc824x ppc853x ppc854x x86),$(ARCH))
# No support for building ionice
ENV += BUSYBOX_CONFIG=src/nice_defconfig
else
ENV += BUSYBOX_CONFIG=src/niceionice_defconfig
endif

.PHONY: xz-compress
xz-compress:
	@$(MSG) "Patching SABnzbd files"
	sed -i.orig $(STAGING_DIR)/share/SABnzbd/SABnzbd.py \
	     -e 's#\(/usr\)\(/bin/python\)#\1/local/python${PYTHON_VERS}\2#'
	sed -i.orig $(STAGING_DIR)/share/SABnzbd/SABHelper.py \
	     -e 's#\(/usr\)\(/bin/python\)#\1/local/python${PYTHON_VERS}\2#'
	sed -i.orig $(STAGING_DIR)/share/SABnzbd/sabnzbd/constants.py \
	     -e "s#\(DEF_DOWNLOAD_DIR = '\)Downloads\(/incomplete'\)#\1/volume1/downloads\2#" \
	     -e "s#\(DEF_COMPLETE_DIR = '\)Downloads\(/complete'\)#\1/volume1/downloads\2#"
	@$(MSG) "Adding files for DSM integration"
	install -m 755 -d $(STAGING_DIR)/share/synoman
	install -m 755 -d $(STAGING_DIR)/sbin
	install -m 755 src/updateInfo.py $(STAGING_DIR)/sbin/updateInfo
	install -m 644 src/config.json $(STAGING_DIR)/share/synoman/config
	install -m 755 src/sabnzbd.cgi.py $(STAGING_DIR)/share/synoman/sabnzbd.cgi
	for size in 16 24 32 48 ; \
	do \
	    convert $(SPK_ICON) -thumbnail $${size}x$${size} -transparent white \
	            $(STAGING_DIR)/share/synoman/sab2-$${size}.png ; \
	done
	@$(MSG) "Compressing with xz"
	(cd $(STAGING_DIR) && tar cpJf $(WORK_DIR)/package.txz *)
	rm -fr $(STAGING_DIR)
	mkdir $(STAGING_DIR)
	mv $(WORK_DIR)/package.txz $(STAGING_DIR)/
	install -m 755 -d $(STAGING_DIR)/var
	install -m 644 src/config.ini $(STAGING_DIR)/var/ 
