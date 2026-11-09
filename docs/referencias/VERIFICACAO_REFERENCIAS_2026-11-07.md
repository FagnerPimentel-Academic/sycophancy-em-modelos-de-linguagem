# Verificação das referências — 07/11/2026

**Escopo:** revisão de `latex/tex/Texto/referencias.bib` após duas auditorias por deep research (ChatGPT) e conferência própria nas fontes primárias.
**Status:** EXECUTADO para metadados; NÃO altera texto dos capítulos; novas referências ainda não citadas.
**Validação técnica:** `biber --tool --validate-datamodel` sem avisos ou erros. Compilação completa com `fei.cls` ainda PENDENTE.

## 1. Alterações nas referências já citadas

| Chave | Alteração | Verificado em |
|---|---|---|
| `sinha2026sycobench` | Acrescentado DOI `10.18653/v1/2026.findings-acl.1759` | Página oficial na ACL Anthology |
| `sharma2024towards` | Lista completa de 19 autores (antes truncada) | Primeira página do PDF publicado (ICLR 2024) |
| `sharma2024towards` | Mantido sem DOI: a ICLR não atribui DOI; o DOI `10.48550/arXiv.2310.13548` é do preprint e não deve ser usado como DOI da conferência | Auditoria do GPT; coerente com o registro da ICLR |
| `vaswani2017attention`, `brown2020language`, `christiano2017deep`, `ouyang2022training` | URL do arXiv trocada pela página oficial dos proceedings do NeurIPS; acrescentado volume | Páginas oficiais NeurIPS (títulos, volumes e, quando exibidas, páginas conferidos) |
| `ouyang2022training` | Acrescentado DOI `10.52202/068431-2011` | Página oficial NeurIPS 2022 |
| `jalongo2016writing` | Removida (resíduo do template, não citada) | — |

`perez2023discovering` e `hong2025measuring` estavam corretas e não mudaram.

## 2. Referências candidatas acrescentadas (não citadas, não aparecem no PDF)

| Chave | Situação | Uso pretendido |
|---|---|---|
| `xie2024askagain` | ACL 2024, DOI conferido | Sugestão falsa após acerto inicial (antecedente direto) |
| `maraia2026sounding` | Findings ACL 2026, DOI e páginas conferidos | Sycophancy em português e efeito de autoridade/registro |
| `laban2024flipflop` | Preprint arXiv | Queda de acurácia após contestação |
| `fanous2025syceval` | AIES 2025; **páginas não conferidas** | Progressiva × regressiva; matemática × medicina |
| `chen2025helpfulness` | npj Digital Medicine; **autores completos não conferidos** | Motivação da criticidade em saúde |
| `zheng2024selectors` | ICLR 2024, página oficial conferida | Viés de seleção A/B/C/D |
| `atil2024nondeterminism` | Preprint arXiv | Não determinismo com temperatura 0 |
| `aldahlawi2026language` | Preprint arXiv | Idiomas, incluindo português |
| `shah2026multilingual` | Preprint arXiv; **autores completos não conferidos** | Sycophancy multilíngue |
| `wei2023synthetic` | Preprint arXiv | Mitigação (contexto) |
| `mekala2025quantization` | EMNLP 2025, DOI conferido (substitui o preprint arXiv:2505.20276) | Cautela com modelos locais quantizados |
| `field2007bootstrapping` | JRSS B, DOI conferido | Bootstrap agrupado |
| `landis1977agreement`, `mchugh2012kappa` | Periódicos | Interpretação do kappa |
| `nist2023airmf` | NIST AI 100-1 | Criticidade como impacto potencial, distinta de probabilidade |

## 3. Pendências

1. Compilar o `principal.tex` e conferir a renderização ABNT (nomes, proceedings, preprints, URLs).
2. Conferir páginas do SycEval e autores completos de Chen et al. e Shah et al.
3. Antes de citar qualquer candidata: ler o original e registrar seção/página (protocolo 01).
4. `pretextuais/epigrafe.tex` usa `\nocite{george_bernard}`, chave inexistente. Afeta só a fase Final. Identificar a fonte real ou remover a epígrafe; não criar referência fictícia.
5. Guia de referências da FEI (NBR 6023, versão 2025) deve prevalecer sobre o estilo padrão do biblatex-abnt na revisão final.
