# Created by: mat
# $FreeBSD$

PORTNAME=	acme-tiny
PORTVERSION=	0.0.g.2016.08.18
CATEGORIES=	security python

MAINTAINER=	mat@FreeBSD.org
COMMENT=	Tiny script to issue and renew TLS certs from Let's Encrypt

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		python shebangfix ssl
SHEBANG_FILES=	acme_tiny.py

USE_GITHUB=	yes
GH_ACCOUNT=	diafygi
GH_TAGNAME=	daba51d

SUB_FILES=	pkg-message
NO_BUILD=	yes

NO_ARCH=	yes

PLIST_FILES=	bin/acme_tiny ${DOCSDIR}/README.md

do-install:
	${INSTALL_SCRIPT} ${WRKSRC}/acme_tiny.py ${STAGEDIR}${PREFIX}/bin/acme_tiny
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/README.md ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
