# Created by: Li-Wen Hsu <lwhsu@FreeBSD.org>
# $FreeBSD: head/textproc/py-sphinx/Makefile 327773 2013-09-20 23:17:30Z bapt $

PORTNAME=	sphinx
PORTVERSION=	1.1.3
PORTREVISION=	2
CATEGORIES=	textproc python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
DISTNAME=	Sphinx-${PORTVERSION}
DIST_SUBDIR=	python

MAINTAINER=	lwhsu@FreeBSD.org
COMMENT=	Python documentation generator

LICENSE=	BSD

RUN_DEPENDS+=	${PYTHON_PKGNAMEPREFIX}pygments>=1.2:${PORTSDIR}/textproc/py-pygments \
		${PYTHON_PKGNAMEPREFIX}Jinja2>=2.3:${PORTSDIR}/devel/py-Jinja2 \
		${PYTHON_PKGNAMEPREFIX}docutils>=0.7:${PORTSDIR}/textproc/py-docutils

USE_PYTHON=	yes
USE_PYDISTUTILS=	easy_install
PYDISTUTILS_PKGNAME=	Sphinx

PLIST_SUB=	PYTHON_VER=${PYTHON_VER}

NO_STAGE=	yes
post-install:
	@${SETENV} PYTHONPATH=${PYTHONPREFIX_SITELIBDIR} \
	${PYTHON_CMD} -m sphinx.pycode.pgen2.driver -c 'import load_grammar'

.include <bsd.port.mk>
