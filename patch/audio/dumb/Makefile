# Created by: Andreas Kohn <andreas@syndrom23.de>
# $FreeBSD: head/audio/dumb/Makefile 320972 2013-06-14 22:25:52Z bapt $

PORTNAME=	dumb
PORTVERSION=	0.9.3
PORTREVISION=	3
CATEGORIES=	audio
MASTER_SITES=	SF

MAINTAINER=	amdmi3@FreeBSD.org
COMMENT=	IT, XM, S3M, and MOD player library

USE_GMAKE=	yes

OPTIONS_DEFINE=	ALLEGRO DEVEL
ALLEGRO_DESC=	Enable allegro support
DEVEL_DESC=	Enable development version

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MALLEGRO} && ! ${PORT_OPTIONS:MDEVEL}
LIB_DEPENDS+=	alleg.42:${PORTSDIR}/devel/allegro
PLIST_SUB+=	ALLEGRO=""
MAKE_ARGS=	_PORT_ALLEGRO_CFLAGS="`allegro-config --cflags`"
PKGNAMESUFFIX=	-allegro
CONFLICTS=	dumb-[0-9]*
.else
PLIST_SUB+=	ALLEGRO="@comment "
MAKE_ARGS=	_PORT_ALLEGRO_CFLAGS=
CONFLICTS=	dumb-allegro-[0-9]*
.endif

.if ${PORT_OPTIONS:MALLEGRO} && ${PORT_OPTIONS:MDEVEL}
LIB_DEPENDS+=	alleg.4:${PORTSDIR}/devel/allegro-devel
PLIST_SUB+=	ALLEGRO=""
MAKE_ARGS=	_PORT_ALLEGRO_CFLAGS="`allegro-config --cflags`"
PKGNAMESUFFIX=	-allegro-devel
CONFLICTS=	dumb-[0-9]*
.else
PLIST_SUB+=	ALLEGRO="@comment "
MAKE_ARGS=	_PORT_ALLEGRO_CFLAGS=
CONFLICTS=	dumb-allegro-devel[0-9]*
.endif

.if ${ARCH} == "amd64" || ${ARCH} == "ia64" || ${ARCH} == "sparc64"
CFLAGS+=	-fPIC
.endif

pre-configure:
	@${CP} ${FILESDIR}/config.txt ${WRKSRC}/make
	@${REINPLACE_CMD} -e "s,@LOCALBASE@,${LOCALBASE}," ${WRKSRC}/make/config.txt
.if ${PORT_OPTIONS:MALLEGRO}
	@${REINPLACE_CMD} -e "s,@ALLEGRO@,," ${WRKSRC}/make/config.txt
.else
	@${REINPLACE_CMD} -e "s,@ALLEGRO@,#," ${WRKSRC}/make/config.txt
.endif

.include <bsd.port.mk>