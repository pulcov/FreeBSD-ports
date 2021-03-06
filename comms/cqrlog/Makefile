# Created by: Stephen Hurd <shurd@FreeBSD.org>
# $FreeBSD$

PORTNAME=	cqrlog
PORTVERSION=	2.0.4
DISTVERSIONPREFIX=	v
CATEGORIES=	comms hamradio

MAINTAINER=	hamradio@FreeBSD.org
COMMENT=	Amateur Radio logging application

LICENSE=	GPLv2

BUILD_DEPENDS=	lazbuild:editors/lazarus
PATCH_DEPENDS=	${LAZARUS_DIR}/tools/lazres:editors/lazarus
LIB_DEPENDS=	libhamlib.so:comms/hamlib

USE_GITHUB=	yes
GH_ACCOUNT=	ok2cqr

USES=		shebangfix
SHEBANG_FILES=	tools/cqrlog-apparmor-fix \
		voice_keyer/voice_keyer.sh

USE_FPC=	cairo fcl-base fcl-db fcl-image fcl-json fcl-net fcl-web \
		fcl-registry rtl-extra fcl-xml mysql numlib openssl pasjpeg x11

ALL_TARGET=	${PORTNAME}

LAZARUS_VER=	1.6.4
LAZARUS_DIR=	${LOCALBASE}/share/lazarus-${LAZARUS_VER}

OPTIONS_SINGLE=		LCL
OPTIONS_SINGLE_LCL=	GTK2 QT4
OPTIONS_DEFAULT=	GTK2

GTK2_USE=	fpc=gtk2 gnome=gtk20
GTK2_BUILD_DEPENDS=	${LAZARUS_DIR}/lcl/units/${BUILDNAME}/gtk2/interfaces.ppu:editors/lazarus-lcl-gtk2
GTK2_MAKE_ARGS=	PLATFORM=gtk2

QT4_LIB_DEPENDS=	libQt4Pas.so:x11-toolkits/qt4pas
QT4_BUILD_DEPENDS=	${LAZARUS_DIR}/lcl/units/${BUILDNAME}/qt/interfaces.ppu:editors/lazarus-lcl-qt
QT4_MAKE_ARGS=	PLATFORM=qt

post-extract:
	@${RM} -r ${WRKSRC}/src/lnet/lib/openssl.pas

post-patch:
	@${SED} -e s!%%LOCALBASE%%!${LOCALBASE}!g \
		-e s!%%MAKE_CMD%%!${MAKE_CMD}!g \
		-e s!%%LAZARUSDIR%%!${LAZARUS_DIR}!g \
		${FILESDIR}/environmentoptions.xml.in \
		> ${WRKSRC}/environmentoptions.xml
	${REINPLACE_CMD} -e s!%%LOCALBASE%%!${LOCALBASE}!g \
		${WRKSRC}/help/cwd.html ${WRKSRC}/help/h1.html \
		${WRKSRC}/src/cqrlog.lpi ${WRKSRC}/src/dData.pas \
		${WRKSRC}/src/dUtils.pas \
		${WRKSRC}/src/fLoTWExport.pas ${WRKSRC}/src/fLoTWExport.lfm \
		${WRKSRC}/src/fPreferences.pas ${WRKSRC}/src/fRotControl.pas \
		${WRKSRC}/src/fTRXControl.pas ${WRKSRC}/src/fGrayline.pas \
		${WRKSRC}/src/fPreferences.lfm ${WRKSRC}/src/fPreferences.pas
	${REINPLACE_CMD} -e s!%%DATADIR%%!${DATADIR}!g \
		${WRKSRC}/src/dData.pas ${WRKSRC}/src/fGrayline.pas
	${REINPLACE_CMD} -e s!Linux!FreeBSD!g \
		${WRKSRC}/src/fMain.lfm
	${REINPLACE_CMD} -e s!%%LAZARUSDIR%%!${LAZARUS_DIR}!g \
		${WRKSRC}/Makefile
	${RM} -r ${WRKSRC}/src/mysql

.include <bsd.port.mk>
