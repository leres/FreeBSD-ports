# $FreeBSD$

PORTNAME=	wsjtx
DISTVERSION=	2.1.2
PORTREVISION=	2
CATEGORIES=	comms hamradio
MASTER_SITES=	SF/wsjt/${PORTNAME}-${PORTVERSION}${DISTVERSIONSUFFIX}

MAINTAINER=	hamradio@FreeBSD.org
COMMENT=	Weak signal ham radio communication package

LICENSE=	GPLv3

BUILD_DEPENDS=	asciidoctor:textproc/rubygem-asciidoctor \
		autoconf>=2.69:devel/autoconf \
		automake>=1.16.1:devel/automake \
		a2x:textproc/asciidoc \
		libtool:devel/libtool \
		${LOCALBASE}/share/xsl/docbook:textproc/docbook-xsl
LIB_DEPENDS=	libfftw3.so:math/fftw3 \
		libfftw3f.so:math/fftw3-float \
		libxslt.so:textproc/libxslt

USES=		cmake compiler:c++11-lib fortran gl \
		makeinfo pkgconfig qt:5 tar:tgz
USE_GL=		glu
USE_QT=		core gui network widgets \
		multimedia concurrent printsupport serialport sql sql-sqlite3 \
		buildtools_build linguisttools_build qmake_build

CMAKE_ARGS+=	-DCMAKE_PREFIX_PATH+=${LOCALBASE}/wsjtx/lib \
		-DLOCALBASE::STRING="${LOCALBASE}"
# for detailed debugging uncomment the next line
#CMAKE_ARGS+=   --debug-output --trace
PLIST_SUB+=	PORTVERSION="${PORTVERSION}"

_PATCHES=	wsjtx.patch hamlib.patch

post-patch:
.  for _patch in ${_PATCHES}
	# Keep a copy of the blank patch for the post-build target below
	${MV} ${WRKSRC}/${_patch} ${WRKSRC}/${_patch}.orig
	# Copy the patch provided by the ports system
	${CP} ${FILESDIR}/${_patch}  ${WRKSRC}
.  endfor

post-build:
	# With cmake 3.18, the patching stage in the internal build
	# is run again, trick it by removing the patch again.
.  for _patch in ${_PATCHES}
	${MV} ${WRKSRC}/${_patch}.orig  ${WRKSRC}/${_patch}
.  endfor

do-install:
	(cd ${CONFIGURE_WRKSRC};${MAKE} -f Makefile DESTDIR=${STAGEDIR} install)

post-install:
.for f in fcal fmeasure fmtave ft8code jt4code jt65code jt9 jt9code \
	message_aggregator msk144code qra64code qra64sim udp_daemon wsjtx wsprd
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/${f}
.endfor

.include <bsd.port.mk>
