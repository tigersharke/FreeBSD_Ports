# Created by: erich@FreeBSD.org
# $FreeBSD: head/astro/xephem/Makefile 300895 2012-07-14 12:56:14Z beat $

PORTNAME=	xephem
PORTVERSION=	3.7.6
CATEGORIES=	astro
MASTER_SITES=	# http://www.clearskyinstitute.com/xephem/

MAINTAINER=	jpaetzel@FreeBSD.org
COMMENT=	Interactive astronomical ephemeris program

LIB_DEPENDS=	png15:${PORTSDIR}/graphics/png \
		jpeg:${PORTSDIR}/graphics/jpeg

USE_MOTIF=	yes
USE_GMAKE=	yes
USE_XORG=	xp xt xext xmu x11 xft
MAKE_JOBS_UNSAFE=	yes

WRKSRC=		${WRKDIR}/${DISTNAME}/GUI/xephem

MAN1=		xephem.1

RESTRICTED=	Personal use only

# XXX needs to be the same as DISTFILES
XEPHEMSRC=	${PORTNAME}-${PORTVERSION}.tar.gz

DESKTOP_ENTRIES="XEphem" "${COMMENT}" "${PORTNAME}" \
		"${PORTNAME}" "Astronomy;Education;Science;" false

.include <bsd.port.pre.mk>

.for file in ${XEPHEMSRC}
.if !exists(${DISTDIR}/${file}) && !defined(PACKAGE_BUILDING)#{
DISTFILE_INSTRUCTIONS=\n\
Because of licensing restrictions, you must manually fetch \n\ ${file} from http://www.clearskyinstitute.com/xephem/, \n\ place it in ${DISTDIR} and then run make again.\n\n
.endif
.endfor

pre-fetch:
.if defined(DISTFILE_INSTRUCTIONS)
	@${PRINTF} "${DISTFILE_INSTRUCTIONS}"
	@exit 1
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|%%LOCALBASE%%|${LOCALBASE}|' \
		-e 's|/usr/X11R6|${LOCALBASE}|g' \
		${WRKSRC}/Makefile
	@${FIND} ${WRKSRC}/../.. -name Makefile -type f | \
		${XARGS} ${REINPLACE_CMD} -e 's|CC =|CC?=|g ; \
		s|CFLAGS=|CFLAGS+=|g ; \
		s|-O2 ||g'

pre-build:
	@${ECHO_CMD} 'XEphem.ShareDir: ${PREFIX}/lib/X11/xephem' > ${WRKSRC}/XEphem.ad

pre-install:
	@${FIND} ${WRKSRC}/../.. -name Makefile.bak -type f | ${XARGS} ${RM} -f
	@${CP} ${WRKSRC}/xephem.man ${WRKSRC}/xephem.1

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/xephem ${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/xephem.1 ${MAN1PREFIX}/man/man1
	${INSTALL_DATA} ${WRKSRC}/XEphem.ad ${PREFIX}/lib/X11/app-defaults/XEphem
	@${MKDIR} ${PREFIX}/lib/X11/xephem
	${TAR} -C ${WRKSRC} -cf - auxil catalogs fifos fits gallery help lo \
		| ${TAR} -C ${PREFIX}/lib/X11/xephem --unlink -xf -
	@${FIND} ${PREFIX}/lib/X11/xephem | ${XARGS} ${CHOWN} ${SHAREOWN}:${SHAREGROUP}
	@${FIND} ${PREFIX}/lib/X11/xephem -type f | ${XARGS} ${CHMOD} ${SHAREMODE}
	${INSTALL_DATA} ${WRKSRC}/XEphem.png ${PREFIX}/share/pixmaps/${PORTNAME}.png

.include <bsd.port.post.mk>
