#FROM ubuntu:22.04
FROM ghcr.io/xu-cheng/texlive-full:latest

ENV DEBIAN_FRONTEND=noninteractive

#RUN apt update && apt install --no-install-recommends -y texlive-full

RUN mkdir /build
RUN mkdir /tex
RUN mkdir /output


RUN cat > texpdf.sh <<'EOF'
#!/bin/bash

# ficha.pdf (ficha catalográfica) fica em /output junto com os PDFs gerados
export TEXINPUTS=/output:

echo 'Step 1/5: pdflatex'
pdflatex -shell-escape -synctex=1 -interaction=nonstopmode \
  -file-line-error \
  -output-directory=/build \
  $1.tex \
  1> /build/$1.stdout.pdflatex.log \
  2> /build/$1.stderr.pdflatex.log

echo 'Step 2/5: makeglossaries'
makeglossaries -d /build $1 \
  1> /build/$1.stdout.makeglossaries.log \
  2> /build/$1.stderr.makeglossaries.log

echo 'Step 3/5: biber'
biber /build/$1 \
  1> /build/$1.stdout.biber.log \
  2> /build/$1.stderr.biber.log

echo 'Step 4/5: makeindex'
openout_any=a makeindex /build/$1.idx \
  1> /build/$1.stdout.makeindex.log \
  2> /build/$1.stderr.makeindex.log

echo 'Step 5/5: pdflatex'
pdflatex -shell-escape -synctex=1 -interaction=nonstopmode \
  -file-line-error \
  -output-directory=/build \
  $1.tex \
  1> /build/$1.stdout.pdflatex.log \
  2> /build/$1.stderr.pdflatex.log

cp /build/*.pdf /output

grep -n \
  -e 'Warning:' \
  -e 'Error:' \
  -e 'Output written on' \
  /build/$1.stdout.pdflatex.log \
  > /output/$1.output.log

echo 'Done!'
EOF

RUN chmod +x texpdf.sh

WORKDIR /tex
