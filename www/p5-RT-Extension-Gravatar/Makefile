PORTNAME=	RT-Extension-Gravatar
PORTVERSION=	2.01
PORTREVISION=	3
CATEGORIES=	www perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	sysadmin@gkg.net
COMMENT=	RT Extension to change ticket metadata via email
WWW=		https://metacpan.org/release/RT-Extension-Gravatar

LICENSE=	GPLv2

BUILD_DEPENDS=	${LOCALBASE}/bin/rt:www/rt${RT_VER}
RUN_DEPENDS=	${LOCALBASE}/bin/rt:www/rt${RT_VER}

USES=		perl5
USE_PERL5=	configure

NO_ARCH=	yes

RT_VER=		44

PLIST_SUB+=	RTHOME=share/rt${RT_VER}

post-patch:
	@${REINPLACE_CMD} -e 's|LocalPath/man/man3|LocalPath/share/man/man3|g' ${WRKSRC}/inc/Module/Install/RTx.pm

# Note: You can install using an arbitrary $PREFIX but only if it
# matches the $PREFIX used to install www/rt44.  Hence ignore
# $PREFIX in the environment and inherit settings from RT.pm
do-configure:
	@cd ${CONFIGURE_WRKSRC} && \
		unset PREFIX && \
		${SETENV} ${CONFIGURE_ENV} ${PERL5} -I${SITE_PERL} ${CONFIGURE_CMD} && \
		${PERL5} -pi -e 's/ doc_(perl|site|\$$\(INSTALLDIRS\))_install$$//' Makefile

post-configure:
	${REINPLACE_CMD} "/RTxPlugin/d" ${WRKSRC}/Makefile

post-install:
	${RM} ${STAGEDIR}${PREFIX}/man/auto/RT/Extension/Gravatar/.packlist
	${RMDIR} -p ${STAGEDIR}${PREFIX}/man/auto/RT/Extension/Gravatar 2>/dev/null || :

.include <bsd.port.mk>
