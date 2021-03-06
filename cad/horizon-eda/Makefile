# $FreeBSD$

PORTNAME=	horizon-eda
DISTVERSIONPREFIX=	v
DISTVERSION=	1.2.1
CATEGORIES=	cad

PATCH_SITES=	https://github.com/${GH_ACCOUNT}/${GH_PROJECT}/commit/
PATCHFILES=	b40e3ed3f92c4b28af307135223ecf05eacecc82.patch:-p1 # backport the build failure fix

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	EDA package for printed circuit board design

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	${LOCALBASE}/include/boost/optional.hpp:devel/boost-libs \
		cppzmq>0:net/cppzmq \
		glm>0:math/glm
LIB_DEPENDS=	libcurl.so:ftp/curl \
		libepoxy.so:graphics/libepoxy \
		libgit2.so:devel/libgit2 \
		libpodofo.so:graphics/podofo \
		libTKSTEP.so:cad/opencascade \
		libuuid.so:misc/e2fsprogs-libuuid \
		libzip.so:archivers/libzip \
		libzmq.so:net/libzmq4

USES=		compiler:c++17-lang gmake gnome localbase pkgconfig python:build sqlite
USE_GITHUB=	yes
GH_PROJECT=	horizon
USE_GNOME=	atkmm gdkpixbuf2 gtkmm30 librsvg2

BINARY_ALIAS=	python3=${PYTHON_CMD}

INSTALLS_ICONS=	yes

post-install:
	cd ${STAGEDIR}${PREFIX}/bin && ${STRIP_CMD} horizon-imp horizon-eda

.include <bsd.port.mk>
