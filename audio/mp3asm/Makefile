# Created by: ijliao
# $FreeBSD$

PORTNAME=	mp3asm
PORTVERSION=	0.1.3.1
PORTREVISION=	1
CATEGORIES=	audio
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/0.1.3-1
DISTNAME=	${PORTNAME}-${PORTVERSION:R}-${PORTVERSION:E}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	MP3 frame level editor

LICENSE=	GPLv2

USES=		tar:bzip2 gmake
GNU_CONFIGURE=	yes
WRKSRC=		${WRKDIR}/${PORTNAME}-0.1
PLIST_FILES=	bin/mp3asm
PORTDOCS=	Changelog README

OPTIONS_DEFINE=	DOCS

post-extract:
	${RM} ${WRKSRC}/config.cache

post-patch:
	${REINPLACE_CMD} -e 's|^CFLAGS=|#CFLAGS=|g' ${WRKSRC}/configure
	${REINPLACE_CMD} -e 's|#include <argz.h>||' \
		-e 's|getprogname|_getprogname|g' \
		-e 's|\([ (!]\)\(log[\.;]\)|\1mp3asm\2|g' \
		${WRKSRC}/src/mp3asm.h ${WRKSRC}/src/*.c

post-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC}/ && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}/

.include <bsd.port.mk>
