# Created by: Marc G. Fournier <scrappy@FreeBSD.org>
# $FreeBSD$

DISTVERSION?=	9.6.7
PORTREVISION?=	0
PKGNAMESUFFIX?=	${PORTVERSION:R:S/.//}${COMPONENT}

MAINTAINER?=	pgsql@FreeBSD.org

INSTALL_DIRS?=	src/common src/timezone src/backend \
		src/backend/utils/mb/conversion_procs \
		src/backend/snowball src/backend/replication/libpqwalreceiver \
		src/bin/initdb src/bin/pg_ctl \
		src/bin/pg_controldata src/bin/pg_resetxlog src/pl \
		src/bin/pg_basebackup src/bin/pg_archivecleanup \
		src/bin/pg_rewind \
		src/bin/pg_test_fsync src/bin/pg_test_timing \
		src/bin/pg_xlogdump src/bin/pg_upgrade

PG_USER?=	postgres
PG_GROUP?=	postgres
PG_UID?=	770

ICU_PATCHFILE=	pg-96b4-icu-2016-10-02.diff.gz
OPTIONS_DEFAULT+=ICU

.include "${.CURDIR}/../postgresql10-server/Makefile"
