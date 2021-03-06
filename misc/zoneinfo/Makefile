# Created by: Edwin Groothuis <edwin@mavetju.org>
# $FreeBSD$

PORTNAME=	zoneinfo
DISTVERSION=	2016i
CATEGORIES=	misc
MASTER_SITES=	ftp://ftp.iana.org/tz/releases/ \
		ftp://munnari.oz.au/pub/
DISTNAME=	tzdata${DISTVERSION}

MAINTAINER=	skreuzer@FreeBSD.org
COMMENT=	Updated timezone definitions

LICENSE=	PD

NO_WRKSUBDIR=	yes
PREFIX=		/usr
NO_ARCH=	yes

TZFILES=	africa antarctica asia australasia etcetera europe \
		factory northamerica southamerica systemv
POSIXRULES=	America/New_York

# Run with "DEVELOPER=1 make check-plist" before commiting!

# Make sure it breaks when the distfile isn't there anymore.
.if !defined(PACKAGE_BUILDING)
MASTER_SITES+=	http://people.freebsd.org/~edwin/
.endif

.include <bsd.port.pre.mk>

# The following country codes can be missing from /usr/share/misc/iso3166 and
# shouldn't appear in the zoneinfo file.
MISSING=	ax bl bq cw gg im je me mf rs ss sx

.ifndef NOMISSING
.for M in ${MISSING}
HAS_${M:tu}!=	${GREP} -c ^${M:tu} /usr/share/misc/iso3166 || ${TRUE}
.if ${HAS_${M:tu}} == "0"
EXTRA_PATCHES+=	${FILESDIR}/patchremove-${M}
.endif
.endfor
.endif

do-build:
	umask 022; \
	cd ${WRKSRC}; \
	zic -d ${WRKSRC}/zoneinfo -p ${POSIXRULES} -m ${NOBINMODE} \
		${LEAPFILE} -y ${.OBJDIR}/yearistype ${TZFILES}

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/share/zoneinfo
	${CP} -R -p ${WRKSRC}/zoneinfo/ ${STAGEDIR}${PREFIX}/share/zoneinfo
	${INSTALL_DATA} ${WRKSRC}/zone.tab ${STAGEDIR}${PREFIX}/share/zoneinfo

test-patches:
.for M in ${MISSING}
	make clean
	NOMISSING=1 EXTRA_PATCHES=${FILESDIR}/patchremove-${M} make patch
.endfor

test-pkgplist:
	for f in $$(find work/stage/usr/share/zoneinfo/ | sed -e 's,work/stage/usr/share/zoneinfo/,,' ); do if [ $$(grep -c $$f pkg-plist) -eq 0 ]; then echo $$f; fi ; done

.include <bsd.port.post.mk>
