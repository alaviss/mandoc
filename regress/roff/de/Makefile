# $OpenBSD: Makefile,v 1.9 2015/02/03 19:37:25 schwarze Exp $

REGRESS_TARGETS	 = append cond escname factorial indir infinite startde TH Dd
LINT_TARGETS	 = escname indir infinite

# groff-1.22.3 defect:
# infinite recursion aborts output completely

SKIP_GROFF	 = infinite

.include <bsd.regress.mk>


# OpenBSD only: non-standard targets

# --- additions to public targets ---

all ascii: ascii-diff-opt

ascii-clean: ascii-clean-opt

groff: TH.out_ascii_opt Dd.out_ascii_opt

groff-clean: groff-clean-opt


# --- local rules ---

ascii-diff-opt: TH.mandoc_ascii_opt Dd.mandoc_ascii_opt
	@${DIFF} ${.CURDIR}/TH.out_ascii_opt TH.mandoc_ascii_opt
	@${DIFF} ${.CURDIR}/Dd.out_ascii_opt Dd.mandoc_ascii_opt

TH.mandoc_ascii_opt: TH.in
	@${MANDOC} -Ios=OpenBSD -Tascii -man ${.ALLSRC} > ${.TARGET}

Dd.mandoc_ascii_opt: Dd.in
	@${MANDOC} -Ios=OpenBSD -Tascii -mdoc ${.ALLSRC} > ${.TARGET}

ascii-clean-opt:
	@rm -f TH.mandoc_ascii_opt Dd.mandoc_ascii_opt

TH.out_ascii_opt: TH.in
	/usr/local/bin/nroff -c -man -Tascii ${.ALLSRC} > ${.TARGET}

Dd.out_ascii_opt: Dd.in
	/usr/local/bin/nroff -c -mdoc -Tascii ${.ALLSRC} > ${.TARGET}

groff-clean-opt:
	rm -f TH.out_ascii_opt Dd.out_ascii_opt
