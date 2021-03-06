# $FreeBSD$

PORTNAME=	gmmlib
DISTVERSIONPREFIX=	intel-${PORTNAME}-
DISTVERSION=	19.4.1
CATEGORIES=	multimedia

PATCH_SITES=	https://github.com/${GH_ACCOUNT}/${GH_PROJECT}/commit/
PATCHFILES+=	f17dd87c7f57.patch:-p1 # https://github.com/intel/gmmlib/pull/67

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	Intel Graphics Memory Management Library

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE.md

ONLY_FOR_ARCHS=	amd64 i386
ONLY_FOR_ARCHS_REASON=	Only Intel GPUs on x86 are supported

USES=		cmake compiler:c++11-lib
USE_GITHUB=	yes
USE_LDCONFIG=	yes
GH_ACCOUNT=	intel
CMAKE_ARGS=	-DBUILD_TYPE:STRING="${CMAKE_BUILD_TYPE}" \
		-DGMMLIB_MARCH:STRING="${CPUTYPE}"

OPTIONS_DEFINE=	TEST

# XXX Unbundle googletest
TEST_CMAKE_BOOL=	RUN_TEST_SUITE
TEST_TEST_TARGET=	Run_ULT

post-patch:
# Silence -Wmacro-redefined
	@${REINPLACE_CMD} -e '/__fastcall/d' \
		${WRKSRC}/Source/inc/portable_compiler.h
# XXX Uncomment and drop patches if upstream doesn't regain sanity
.if !exists(${.CURDIR}/files/patch-gcc-atomics) && !exists(${.CURDIR}/files/patch-unix)
# Avoid platform whitelists for generic non-Windows code
	@${GREP} --exclude='*/os.h*' --exclude='*/googletest/*' -Flr '__linux' ${WRKSRC} | ${XARGS} \
		${REINPLACE_CMD} -i .opsys -E 's/__linux(__)?/__unix__/'
.endif

post-install:
# Clean up after PATTERN-based install
	@${FIND} ${STAGEDIR}${PREFIX}/include -type d -empty -delete

.include <bsd.port.mk>
