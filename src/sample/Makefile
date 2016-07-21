# \begin{setting}[Suffixes]
# \comment{��ĥ�Ҥ���Ͽ}
.SUFFIXES: \
	.aux .bb .bbl .bib .blg .bmp .cls .dic .dtx  .dvi  .eps .htm \
	.html .idx .ilg .ind .ins .jpg .jpeg .lof .log .lol .lot .mp \
	.obj .out .pdf .pl .plt .png .ps .sty .tex .toc 
# \end{setting}

# \begin{setting}[Programs]
# \comment{DVI ����}
TEX=	platex
# \comment{��������}
MAKEIDX=mendex
# \comment{DVI \to PDF ����}
DVIPDF=	dvipdfmx
# \comment{���}
RM=	rm -f
# \comment{�Ƶ�Ū���}
RMFR=	rm -fr
# \comment{�Ƶ�Ū�ǥ��쥯�ȥ����}
MKDIR=	mkdir -p 
# \comment{Make ������}
AUTOMAKE=make
# \end{setting}

# \begin{setting}[Filenames]
# \comment{���ܤȤʤ�ե�����}
F=	main
# \comment{���ܤȤʤ�ޥ����ѥå�����}
M=	mymacros
# \comment{������������}
IST=	$M.ist 
# \comment{ɬ�פȤʤ륽����}
SRC=	$(IST) $F.dic $F.tex $F.pdf \
	$M.dtx $M.ins $M.sty $M.pdf \
	Makefile makebb 
# \comment{�����Υǥ��쥯�ȥ�}
IMG=	img
# \end{setting}

# \begin{setting}[CommandLineOptions]
# \comment{$TEX �Υ��ץ����}
TEXOPT=		-src-specials
# \comment{$DVIPDF �Υ��ץ����}
DVIPDFOPT=	-O 2 -p a4 -V 4 -r 1200
# \comment{$DVIPS �Υ��ץ����}
DVIPSOPT=	-t a4
# \comment{$MAKEIDX �Υ��ץ����}
IDXOPT=		-s $(IST) -d $F.dic
# \end{setting}

# \begin{setting}[Printer]
# \comment{�饤��ץ��}
LPNAME=	10.24.194.2
# \end{setting}

# \begin{setting}[Programs]
#    \begin{subsetting}[Mac OS X]
# \comment{DVI �ե�����ץ�ӥ塼��}
XDVI=	mxdvi  
# \comment{PDF �ե�����ץ�ӥ塼��}
PDFVIEWER=open
# \comment{DVI \to PS ����}
DVIPS=	dvips
#    \end{subsetting}

#    \begin{subsetting}[Linux]
#XDVI=	xdvi # or pxdvi
#PDFVIEWER=acroread
#DVIPS=	dvips # or pdvips
#    \end{subsetting}

#    \begin{subsetting}[Windows + Cygwin]
#XDVI=	/cygdrive/c/dviout/dviout.exe 
#PDFVIEWER=/cygdrive/c/Program\ Files/Adobe/Reader32.exe 
#DVIPS=dvipsk
#    \end{subsetting}
# \end{setting}

# \begin{dependency}
# \comment{ɸ��Υ������å�}
all: $F.pdf

$F.dvi: $F.tex
$F.ind: $F.idx
$F.idx: $F.tex
$F.pdf: $F.dvi

$M.dvi: $M.dtx
$M.pdf: $M.dvi
$M.sty: $M.dtx
# \end{dependency}

# \begin{GenerationRules}
.tex.dvi:
	$(TEX) $*; $(TEX) $*;
# \comment{��߻��Ȥβ�褬��λ����ޤǥ����ץ��åȤ�³���롥
	(while egrep "may have changed" $*.log; do $(TEX) $*; done)
.dtx.dvi:
	$(TEX) $<; $(TEX) $<
.tex.idx:
	$(TEX) $*;
.idx.ind:
	$(MAKEIDX) $(IDXOPT) -o $*.ind $*.idx
.dvi.pdf:
	$(DVIPDF) $(DVIPDFOPT) $*
.dvi.ps:
	$(DVIPS) $(DVIPSOPT) -o $@ $*
.dtx.sty:
	$(TEX) $*.ins
# \end{GenerationRules}

# \begin{aliases}
#    \begin{subsetting}[Primary]
# \comment{$F.tex �� PDF �ե����� $F.pdf �κ���}
pdf:	$F.pdf 
# \comment{$F.tex �� DVI �ե����� $F.dvi �κ���}
dvi:	$F.dvi 
# \comment{$F.tex �κ��� $F.ind �κ���}
ind:	$F.ind 
# \comment{�ޥ����ѥå����� istt.sty �κ���}
sty:	$M.sty 
# \comment{�ޥ����ѥå����� istt.sty �Υޥ˥奢��}
man:	$M.pdf 
#    \end{subsetting}

#     \begin{subsetting}[Secondary]
# \comment{��¸�ط���̵�뤷�����٤Υ����ץ��å�}
fast:   
	$(TEX) $F; $(TEX) $F
# \comment{��¸�ط���̵�뤷�����٤Υ����ץ��å�}
faster: 
	$(TEX) $F
# \comment{���������դ� PDF �ե���������}
today:	$F.pdf 
	cp $< $F-`date +%Y-%m-%d-%H-%M`.pdf
#    \end{subsetting}

#    \begin{subsetting}[Previewing]
view:	$F.dvi
	$(XDVI) $<
viewpdf: $F.pdf
	$(PDFVIEWER) $<
#    \end{subsetting}
# \end{aliases}

# \begin{setting}[Distribution]
clean:
	$(RM) $F.aux $F.log $F.toc $F.dvi $F.ind
	$(RM) $F.out $F.brf $F.idx $F.ilg *~
# \comment{���Ƥ������� TAR ball}
tar:	$M.pdf $F.pdf 
	$(MKDIR) $(F)src/img
	cp -r img $(F)src/
	cp $(SRC) $(F)src/
	tar czf $(F)src.tgz $(F)src/
	$(RMFR) $(F)src/
# \comment{���������֤Υ����å�}
checktar: 
	tar tzf $(F)src.tgz | sort | less
# \comment{PDF �Υե��������ȥե���Ⱦ���Υ����å�}
checkpdf: $F.pdf 
	pdfinfo $< | less;
	pdffonts $< | less
# \comment{���� ($IMG �ǥ��쥯�ȥ�) ��BoundingBox �κ���}
bb:	
	./makebb $(IMG)
ls:
	ls -lhGF --color=auto
# \end{setting}