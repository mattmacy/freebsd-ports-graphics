# $FreeBSD$

PORTNAME=	cppunit
PORTVERSION=	1.13.2
PORTREVISION=	2
CATEGORIES=	devel
MASTER_SITES=	http://dev-www.libreoffice.org/src/

MAINTAINER=	bdrewery@FreeBSD.org
COMMENT=	C++ port of the JUnit framework for unit testing

LICENSE=	LGPL21

OPTIONS_DEFINE=	DOCS DOXYGEN

DOXYGEN_BUILD_DEPENDS=	doxygen:devel/doxygen \
			dot:graphics/graphviz
DOXYGEN_CONFIGURE_ENABLE=	dot doxygen html-docs
DOXYGEN_CONFIGURE_ON=	--htmldir="${DOCSDIR}/html"

GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
OPTIONS_SUB=	yes
USE_LDCONFIG=	yes
USES=		libtool pathfix

post-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/doc/FAQ ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/NEWS ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/README ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
