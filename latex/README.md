# Compilando com o docker

Usando um terminal, navegue até a pasta *.devcontainer* e execute:

```bash
docker compose up
```

Isso compila os três documentos (serviços `ficha`, `ata` e `principal`; o `principal` espera os outros dois terminarem, pois inclui a ficha e a ata). Para compilar só um:

```bash
docker compose up principal
```

Os PDFs e LOGs são gerados na pasta *output*. A primeira execução demora alguns minutos para baixar a imagem; as seguintes levam poucos segundos.

## Estrutura

- `tex/`: fontes LaTeX. Tudo que o aluno edita fica em `tex/Texto/`: `info.tex` (dados do trabalho), `referencias.bib` e os capítulos.
- `output/`: documentos gerados (`principal.pdf`, `ata.pdf` e `ficha.pdf`).
- `.devcontainer/`: Dockerfile e docker-compose (a pasta `build/` guarda os logs intermediários).

## Ficha catalográfica

O `output/ficha.pdf` é gerado a partir do `tex/ficha.tex`, com os dados do `info.tex` (bloco "Ficha catalográfica"). O `principal.tex` o inclui na fase `Final`.
