# Created by: Olivier Duchateau
# $FreeBSD$

PORTNAME=	sparqlwrapper
PORTVERSION=	1.8.4
CATEGORIES=	textproc python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
DISTNAME=	SPARQLWrapper-${PORTVERSION}

MAINTAINER=	python@FreeBSD.org
COMMENT=	SPARQL endpoint interface to Python

LICENSE=	W3C
LICENSE_NAME=	W3C Software Notice and License
LICENSE_FILE=	${WRKSRC}/LICENSE.txt
LICENSE_PERMS=	dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

USES=		python
USE_PYTHON=	autoplist distutils

NO_ARCH=	yes
USE_LOCALE=	en_US.UTF-8

post-patch:
	@${REINPLACE_CMD} '/keepalive/d' ${WRKSRC}/requirements.txt

.include <bsd.port.mk>
