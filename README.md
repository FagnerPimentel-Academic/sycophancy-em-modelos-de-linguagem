# Título
-

## Integrantes
-
-

## Orientador
- [Prof. Dr. Fagner de Assis Moura Pimentel](http://lattes.cnpq.br/6747210702910392)

## Objetivo
-

## Resumo
-

---

# Como usar este repositório

Este repositório é o modelo de trabalho (IC, TCC, mestrado ou doutorado) do Centro Universitário FEI. Você escreve o texto em LaTeX e o repositório gera os PDFs automaticamente.

## O que fazer

1. **Preencha o formulário acima** (título, integrantes, orientador, objetivo e resumo).
2. **Preencha o `latex/tex/Texto/info.tex`.** Ele reúne todos os dados do trabalho: fase, tipo, curso, ano, orientador, autores, título, banca, palavras-chave e dados da ficha catalográfica. As linhas marcadas com `% Alterar` são as que você deve mudar.
3. **Escreva o texto** nos arquivos da pasta `latex/tex/Texto/` (veja a tabela abaixo) e as referências em `referencias.bib`.
4. **Compile** com o Docker e confira os PDFs (veja "Como compilar").
5. **Guarde no repositório** o código em `src/` e os demais documentos em `docs/`.
6. **Atualize a fase** em `info.tex` (`\faseAtual`) quando for entregar o texto final.

## O que você pode editar

Tudo que você edita fica em `latex/tex/Texto/`:

| Arquivo | Conteúdo |
|---|---|
| `info.tex` | Dados do trabalho (capa, ata e ficha). |
| `resumo.tex` | Resumo. As palavras-chave vêm do `info.tex`. |
| `introducao.tex`, `conceitos.tex`, `trabalhos.tex`, `metodologia.tex` | Capítulos (em todas as fases). |
| `cronograma.tex` | Cronograma (fase `Projeto`). |
| `resultados.tex`, `conclusao.tex` | Capítulos da fase `Final`. |
| `dedicatoria.tex`, `agradecimentos.tex`, `epigrafe.tex` | Elementos pré-textuais (fase `Final`). |
| `glossaries.tex` | Lista de abreviaturas e símbolos. |
| `referencias.bib` | Referências bibliográficas (BibTeX). |

Também são seus os arquivos de `src/` e `docs/`.

## O que NÃO editar

Estes arquivos são do modelo e não devem ser alterados:

- `latex/tex/principal.tex`, `ata.tex`, `ficha.tex`: montagem dos documentos.
- `latex/tex/processamento.tex`: valores derivados dos dados do `info.tex` (nome completo do orientador, título conferido, descrição da folha de rosto etc.).
- `latex/tex/fei.cls`: classe LaTeX da FEI.
- `latex/.devcontainer/` e `.github/`: compilação e CI.
- `latex/output/`: PDFs gerados.

Se precisar de algo que exige mexer neles, fale com o orientador.

## Fases do trabalho

Em `info.tex`, a opção `\faseAtual` define o que entra no `principal.pdf`:

- **`Projeto`**: resumo, introdução, conceitos, trabalhos relacionados, metodologia e cronograma.
- **`Final`**: tudo isso, menos o cronograma, e com resultados, conclusão, ficha catalográfica, folha de aprovação, dedicatória, agradecimentos, epígrafe e listas de figuras, tabelas e algoritmos.

O `\tipo` (Iniciação Científica, Conclusão de Curso, Mestrado ou Doutorado) ajusta automaticamente o texto da folha de rosto e o título conferido.

## Como compilar

É preciso ter o Docker instalado ([guia de instalação](https://docs.docker.com/engine/install/); no Windows ou macOS, use o [Docker Desktop](https://docs.docker.com/desktop/)). No terminal:

```bash
cd latex/.devcontainer
docker compose up
```

Os PDFs (`principal.pdf`, `ata.pdf` e `ficha.pdf`) e os logs saem em `latex/output/`. A primeira execução demora alguns minutos; as seguintes, poucos segundos. Detalhes em [`latex/README.md`](latex/README.md).

A cada `push`, o GitHub Actions também compila o texto e disponibiliza os PDFs como artefato "output" na aba *Actions*.

## Ficha catalográfica

O `ficha.pdf` gerado aqui é só um modelo, feito com os dados do `info.tex`. A ficha oficial é gerada pela biblioteca em <https://ficha.fei.edu.br/ficha/>. Quando a receber, copie o PDF para `latex/output/ficha.pdf` e avise o orientador, para ajustar o compose (senão o modelo sobrescreve a oficial).

## Dicas

- Troque os textos de orientação e as caixas `\todo` (notas em laranja na margem) pelo seu conteúdo e remova-as no final.
- Se o PDF não mudar, olhe os logs em `latex/output/*.output.log` (erros e avisos do LaTeX).
- Se o `docker compose up` deixar arquivos que você não consegue apagar, eles pertencem ao root: apague com `sudo`.
