# Compilando com o docker

Usando um terminal, navegue até a pasta *.devcontainer* e execute:

```bash
docker compose up
```

Isso compila os cinco documentos (serviços `ficha`, `ata`, `recursos`, `etica` e `principal`; o `principal` espera os outros dois terminarem, pois inclui a ficha e a ata). Para compilar só um, use o nome do serviço:

```bash
docker compose up principal
docker compose up recursos
docker compose up etica
```

Os PDFs e LOGs são gerados na pasta *output*. A primeira execução demora alguns minutos para baixar a imagem; as seguintes levam poucos segundos.

## Estrutura

- `tex/`: fontes LaTeX. Os arquivos na raiz (`principal.tex`, `ata.tex`, `ficha.tex`, `recursos.tex`, `etica.tex`, `recursosComum.tex` e `processamento.tex`) montam os documentos e não devem ser editados. Tudo que o aluno edita fica em `tex/info/` (dados do trabalho), `tex/recursos/` (materiais, outros, serviços internos e externos), `tex/etica/` (Comitê de Ética), `tex/pretextuais/` (resumo, dedicatória, agradecimentos, epígrafe e glossário) e `tex/Texto/` (`referencias.bib` e os capítulos).
- `output/`: documentos gerados (`principal.pdf`, `ata.pdf`, `ficha.pdf`, `recursos.pdf` e `etica.pdf`).
- `.devcontainer/`: Dockerfile e docker-compose (a pasta `build/` guarda os logs intermediários).

## Ficha catalográfica

O `output/ficha.pdf` é gerado a partir do `tex/ficha.tex`, com os dados de `tex/info/` (`ficha.tex`). O `principal.tex` o inclui na fase `Final`.
