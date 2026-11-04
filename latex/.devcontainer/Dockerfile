# Ambiente verificado em 04/11/2026 (TeX Live 2026, linux/amd64).
FROM ghcr.io/xu-cheng/texlive-full@sha256:c06416ebbc69c8e90e07d1f1a6f7a3f9b334e773daa3543ce879ea533317c3a7

ENV DEBIAN_FRONTEND=noninteractive

# FEI 4.10.4 carrega newtxtext antes de memoir. newtxtext 1.744 carrega
# xcolor antes da classe, causando a dupla definição de \@namelet.
# O pacote completo newtx 1.71 arquivado no TeX Live 2022 evita essa ordem.
# Preserva fei.cls, memoir e as demais dependências; verifica o download.
ENV TEXMFHOME=/opt/texmf-fei
RUN mkdir -p "$TEXMFHOME" && \
    curl --fail --location --retry 3 \
      https://ftp.math.utah.edu/pub/tex/historic/systems/texlive/2022/tlnet-final/archive/newtx.tar.xz \
      -o /tmp/newtx.tar.xz && \
    echo '50bfa3e5182ce32281cef269dbb8d4d2b727899391df1ef6c1ca1be2108e215e  /tmp/newtx.tar.xz' | sha256sum -c - && \
    tar -xJf /tmp/newtx.tar.xz -C "$TEXMFHOME" && \
    rm /tmp/newtx.tar.xz

RUN mkdir -p /build /tex /output

RUN cat > /texpdf.sh <<'EOF'
#!/bin/bash
set -euo pipefail

name=${1:?Informe o documento sem a extensão .tex}
[[ "$name" =~ ^[A-Za-z0-9_-]+$ ]] || exit 2
export TEXINPUTS=/output:
# Uma pasta nova impede que auxiliares ou PDFs antigos simulem sucesso.
build_dir=$(mktemp -d "/build/${name}.XXXXXX")
trap 'echo "Falha na compilação; logs preservados em $build_dir" >&2' ERR

compile_pass() {
  pdflatex -no-shell-escape -synctex=1 -interaction=nonstopmode \
    -halt-on-error -file-line-error -output-directory="$build_dir" \
    "$name.tex" > "$build_dir/pass$1.log" 2>&1
}

compile_pass 1
if [[ -s "$build_dir/$name.glo" || -s "$build_dir/$name.acn" || -s "$build_dir/$name.slo" ]]; then
  makeglossaries -d "$build_dir" "$name" > "$build_dir/makeglossaries.log" 2>&1
fi
if [[ -s "$build_dir/$name.bcf" ]]; then
  biber --input-directory "$build_dir" --output-directory "$build_dir" \
    "$name" > "$build_dir/biber.log" 2>&1
fi
if [[ -s "$build_dir/$name.idx" ]]; then
  (cd "$build_dir" && makeindex "$name.idx" > makeindex.log 2>&1)
fi
compile_pass 2
compile_pass 3
# Pendências de referências precisam ser resolvidas antes de publicar o PDF.
if grep -Eq 'There were undefined references|Please.*rerun Biber|Rerun to get cross-references right|Label.s. may have changed' "$build_dir/pass3.log"; then
  echo "Referências ainda não estabilizadas: $build_dir/pass3.log" >&2
  exit 1
fi
test -s "$build_dir/$name.pdf"
cp "$build_dir/$name.pdf" "/output/$name.pdf"
cp "$build_dir/pass3.log" "/output/$name.output.log"
echo "PDF novo: /output/$name.pdf; logs: $build_dir"
EOF

RUN chmod +x /texpdf.sh
WORKDIR /tex
