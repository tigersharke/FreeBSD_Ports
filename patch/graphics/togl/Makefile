# Created by: Randall Hopper <aa8vb@ipass.net>
# $FreeBSD: head/graphics/togl/Makefile 300896 2012-07-14 13:54:48Z beat $

PORTNAME=	togl
PORTVERSION=	2.0
CATEGORIES=	graphics tk
MASTER_SITES=	SF/${PORTNAME}/Togl/${PORTVERSION}
DISTNAME=	Togl${PORTVERSION}-src

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Tk OpenGL widget

WRKSRC=		${WRKDIR}/Togl${PORTVERSION}

USE_XORG=	x11 xt xmu
USE_GL=		gl
USE_TCL_BUILD=	84+
USE_TCL=	84+
USE_TK_BUILD=	84+
USE_TK=		84+
USE_GMAKE=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-tk=${TK_LIBDIR} \
		--with-tcl=${TCL_LIBDIR} \
		--with-tclinclude=${TCL_INCLUDEDIR}
MAKE_ENV=	PTHREAD_LIBS="${PTHREAD_LIBS}" \
		PTHREAD_CFLAGS="${PTHREAD_CFLAGS}"
USE_LDCONFIG=	yes

TOGL_INSTDIR=	${PREFIX}/lib/tk${TK_VER}/${DISTNAME}
PLIST_SUB=	TOGL_INSTDIR="${TOGL_INSTDIR:S,^${PREFIX}/,,}"

CPPFLAGS+=	-I${TK_INCLUDEDIR}
LDFLAGS+=	-L${TK_LIBDIR}

OPTIONS_DEFINE=	DOCS

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MDOCS}
PLIST_SUB+=	PORTDOCS=""
.else
PLIST_SUB+=	PORTDOCS="@comment "
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|wish |${WISH:T} |' ${WRKSRC}/*.tcl

do-install:
	@${MKDIR} ${TOGL_INSTDIR}
.for i in togl.h togl_ws.h libTogl1.7.so pkgIndex.tcl
	${INSTALL_DATA} ${WRKSRC}/${i} ${TOGL_INSTDIR}
.endfor
	${LN} -s ${TOGL_INSTDIR}/libTogl1.7.so  ${TOGL_INSTDIR}/libtogl.so.1
	${LN} -s ${TOGL_INSTDIR}/libTogl1.7.so  ${PREFIX}/lib/libtogl.so
	${LN} -s ${TOGL_INSTDIR}/libTogl1.7.so  ${PREFIX}/lib/libtogl.so.1

.if ${PORT_OPTIONS:MDOCS}
	@${MKDIR} ${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/Togl.html ${DOCSDIR}
.endif

.if ${PORT_OPTIONS:MEXAMPLES}
	@${MKDIR} ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/Makefile ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/ben.rgb ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/double.c ${WRKSRC}/double.tcl ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/gears.c ${WRKSRC}/gears.tcl ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/image.c ${WRKSRC}/image.h ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/index.c ${WRKSRC}/index.tcl ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/overlay.c ${WRKSRC}/overlay.tcl ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/stereo.c ${WRKSRC}/stereo.tcl ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/texture.c ${WRKSRC}/texture.tcl ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/togl.c ${WRKSRC}/togl.h ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/tree2.rgba ${EXAMPLESDIR}
.endif

.include <bsd.port.mk>
