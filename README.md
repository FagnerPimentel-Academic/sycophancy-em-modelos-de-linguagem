# Sycophancy em Grandes Modelos de Linguagem: avaliação de capitulação, correção seletiva e risco em múltiplos domínios

## Integrantes
- Natasha Almeida Trindade
- Douglas Henrique Honda
- Marcus Vinicius Zanelato

## Orientador
- [Prof. Dr. Fagner de Assis Moura Pimentel](http://lattes.cnpq.br/6747210702910392)

## Objetivo
- Quantificar e comparar o comportamento de sycophancy em diferentes LLMs sob pressão do usuário, avaliando capitulação, correção seletiva e gravidade potencial das falhas em cenários de diferentes níveis de criticidade.

## Resumo
- Grandes Modelos de Linguagem (LLMs) são utilizados na geração de conteúdo e no apoio a decisões. O alinhamento por preferências pode criar tensões entre produzir respostas apreciadas pelo usuário e preservar a correção factual. Nesse contexto, *sycophancy* designa comportamentos de concordância indevida com crenças ou sugestões do usuário; em diálogos com múltiplos turnos, contestações repetidas podem influenciar as respostas do modelo. Este trabalho propõe investigar a capitulação diante de sugestões incorretas e a aceitação de correções válidas, considerando também a criticidade potencial das consequências de uma resposta errada. Para isso, pretende-se desenvolver, após a análise metodológica dos trabalhos-base, um protocolo reproduzível com perguntas verificáveis, condições de contestação e registros das interações. As medidas candidatas incluem taxa de capitulação, turno da primeira mudança, frequência de mudanças e aceitação de correções válidas, com populações elegíveis definidas separadamente. A pesquisa buscará comparar comportamentos entre modelos e cenários, distinguindo criticidade de dificuldade da questão. Nesta etapa, o protocolo experimental permanece em elaboração e não são apresentados resultados de testes com LLMs.

# Como usar este repositório

Este repositório é o modelo de trabalho (IC, TCC, mestrado ou doutorado) do Centro Universitário FEI. Você escreve o texto em LaTeX e o repositório gera os PDFs automaticamente.

## O que fazer

1. **Preencha o formulário acima** (título, integrantes, orientador, objetivo e resumo).
2. **Preencha os arquivos da pasta `latex/tex/info/`.** Eles reúnem os dados do trabalho (veja a tabela abaixo). As linhas marcadas com `% Alterar` são as que você deve mudar.
3. **Escreva o texto** nos arquivos da pasta `latex/tex/Texto/` (veja a tabela abaixo) e as referências em `referencias.bib`.
4. **Compile** com o Docker e confira os PDFs (veja "Como compilar").
5. **Preencha a lista de recursos** em `latex/tex/recursos/` (materiais, outros, serviços internos e externos) para gerar o `recursos.pdf`.
6. **Se a pesquisa envolver pessoas, preencha** `latex/tex/etica/` para gerar o `etica.pdf`, que acompanha a submissão ao Comitê de Ética (veja "Comitê de Ética").
7. **Guarde no repositório** o código em `src/` e os demais documentos em `docs/`.
8. **Atualize a fase** em `info/trabalho.tex` (`\faseAtual`) quando for entregar o texto final.

## O que você pode editar

Os dados do trabalho ficam em `latex/tex/info/`:

| Arquivo | Conteúdo |
|---|---|
| `trabalho.tex` | Fase, tipo, curso e ano. |
| `orientacao.tex` | Orientador, coorientador e departamento. |
| `autores.tex` | Autores (alunos). |
| `projeto.tex` | Título, subtítulo (deixe `\sub` vazio se não houver) e palavras-chave. |
| `banca.tex` | Membros da banca (ata). |
| `ficha.tex` | Dados da ficha catalográfica (não usada em IC). |

Os elementos pré-textuais ficam em `latex/tex/pretextuais/`:

| Arquivo | Conteúdo |
|---|---|
| `resumo.tex` | Resumo. As palavras-chave vêm de `info/projeto.tex`. |
| `dedicatoria.tex`, `agradecimentos.tex`, `epigrafe.tex` | Dedicatória, agradecimentos e epígrafe (fase `Final`). |
| `glossario.tex` | Lista de abreviaturas e símbolos. |

O texto fica em `latex/tex/Texto/`:

| Arquivo | Conteúdo |
|---|---|
| `introducao.tex`, `conceitos.tex`, `trabalhos.tex`, `metodologia.tex` | Capítulos (em todas as fases). |
| `cronograma.tex` | Cronograma (fase `Projeto`). |
| `resultados.tex`, `conclusao.tex` | Capítulos da fase `Final`. |
| `referencias.bib` | Referências bibliográficas (BibTeX). |

Também são seus os arquivos de `latex/tex/recursos/` e `latex/tex/etica/` (veja as seções abaixo) e os de `src/` e `docs/`.

## O que NÃO editar

Estes arquivos são do modelo e não devem ser alterados:

- `latex/tex/principal.tex`, `ata.tex`, `ficha.tex`, `recursos.tex`, `recursosComum.tex`, `etica.tex`: montagem dos documentos.
- `latex/tex/processamento.tex` e `latex/tex/info/info.tex`: valores derivados dos dados de `info/` (nome completo do orientador, título conferido, descrição da folha de rosto etc.).
- `latex/tex/fei.cls`: classe LaTeX da FEI.
- `latex/.devcontainer/` e `.github/`: compilação e CI.
- `latex/output/`: PDFs gerados.

Se precisar de algo que exige mexer neles, fale com o orientador.

## Fases do trabalho

Em `info/trabalho.tex`, a opção `\faseAtual` define o que entra no `principal.pdf`:

- **`Projeto`**: resumo, introdução, conceitos, trabalhos relacionados, metodologia e cronograma.
- **`Final`**: tudo isso, menos o cronograma, e com resultados, conclusão, ficha catalográfica, folha de aprovação, dedicatória, agradecimentos, epígrafe e listas de figuras, tabelas e algoritmos.

O `\tipo` (Iniciação Científica, Conclusão de Curso, Mestrado ou Doutorado) ajusta automaticamente o texto da folha de rosto e o título conferido.

## Como compilar

É preciso ter o Docker instalado ([guia de instalação](https://docs.docker.com/engine/install/); no Windows ou macOS, use o [Docker Desktop](https://docs.docker.com/desktop/)). No terminal:

```bash
cd latex/.devcontainer
docker compose up
```

Os PDFs e os logs saem em `latex/output/`. A primeira execução demora alguns minutos; as seguintes, poucos segundos. Para compilar só um documento, use o nome do serviço, por exemplo `docker compose up recursos`. Detalhes em [`latex/README.md`](latex/README.md).

| PDF | Serviço | O que é |
|---|---|---|
| `principal.pdf` | `principal` | O texto do trabalho (projeto ou versão final, conforme a fase). |
| `ata.pdf` | `ata` | Ata da defesa, com a banca. |
| `ficha.pdf` | `ficha` | Modelo da ficha catalográfica (fase `Final`). |
| `recursos.pdf` | `recursos` | Lista de recursos do projeto, com os totais. |
| `etica.pdf` | `etica` | Projeto detalhado e TCLE para o Comitê de Ética. |

A cada `push`, o GitHub Actions também compila o texto e disponibiliza os PDFs como artefato "output" na aba *Actions*.

## Recursos do projeto

O `recursos.pdf` tem uma capa com os dados do projeto (vindos dos arquivos de `info/`), uma tabela para cada tipo de recurso e um resumo com o total geral. Cada tipo tem seu arquivo em `latex/tex/recursos/`, com um comando por item. Valores com ponto decimal, sem `R$`; subtotais e totais são calculados automaticamente.

| Arquivo | Comando por item |
|---|---|
| `materiais.tex` | `\material{descrição}{quantidade}{valor unitário}{link de compra}` |
| `outros.tex` | `\outro{descrição}{valor}` |
| `servicosInternos.tex` | `\servicoInterno{descrição}{horas}{valor por hora}` |
| `servicosExternos.tex` | `\servicoExterno{fornecedor}{data}{valor}` |

## Comitê de Ética (Plataforma Brasil)

O `etica.pdf` reúne o projeto detalhado e o TCLE para submissão ao Comitê de Ética em Pesquisa pela [Plataforma Brasil](https://plataformabrasil.saude.gov.br/). Título, autores e orientador (pesquisador responsável) vêm de `info/`, e o orçamento vem das tabelas de `recursos/`. O que é específico de ética fica em `latex/tex/etica/`:

| Arquivo | Conteúdo |
|---|---|
| `pesquisa.tex` | Local e período da coleta, público-alvo, número de participantes, financiamento e contatos (pesquisador e CEP). |
| `projetoDetalhado.tex` | Resumo, introdução, hipótese, objetivos, metodologia, riscos e benefícios, desfechos, sigilo, cronograma e orçamento. |
| `tcle.tex` | Termo de Consentimento Livre e Esclarecido. |

Troque os lembretes `\todo` pelo seu texto. Confira com a secretaria do CEP se a instituição exige algo além disso (termo de assentimento, carta de anuência, declaração de infraestrutura).

## Ficha catalográfica

O `ficha.pdf` gerado aqui é só um modelo, feito com os dados de `info/`. A ficha oficial é gerada pela biblioteca em <https://ficha.fei.edu.br/ficha/>. Quando a receber, copie o PDF para `latex/output/ficha.pdf` e avise o orientador, para ajustar o compose (senão o modelo sobrescreve a oficial).

## Dicas

- Troque os textos de orientação e as caixas `\todo` (notas em laranja na margem) pelo seu conteúdo e remova-as no final.
- Todos os documentos usam os mesmos dados de `info/`: mude o título, os autores ou o orientador uma vez e recompile.
- Se o PDF não mudar, olhe os logs em `latex/output/*.output.log` (erros e avisos do LaTeX).
- Se o `docker compose up` deixar arquivos que você não consegue apagar, eles pertencem ao root: apague com `sudo`.
