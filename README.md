# Sherlock Ramos Blog

![Hugo](https://img.shields.io/badge/Hugo-0.146.0-ff4088?logo=hugo&logoColor=fff) ![Tema PaperMod](https://img.shields.io/badge/Tema-PaperMod-0a192f)

Blog estático em Hugo configurado com o tema PaperMod (ProfileMode) e conteúdo principal em Português. O projeto já traz estilos personalizados, documentação interna e scripts para build reproduzíveis.

## Sumário
- [Visão Geral](#visão-geral)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Requisitos](#requisitos)
- [Como Executar](#como-executar)
- [Fluxo de Conteúdo](#fluxo-de-conteúdo)
- [Personalização de Tema](#personalização-de-tema)
- [Documentação Interna](#documentação-interna)
- [Contribuição](#contribuição)
- [Licença](#licença)

## Visão Geral
- Gerador estático: Hugo `v0.146.0`, configurado em `hugo.yaml`.
- Tema: PaperMod com ProfileMode, botões de navegação e ícones sociais.
- Idioma padrão: Português do Brasil (`defaultContentLanguage: pt-br`).
- Deploy: saída no diretório `public/`, pronta para qualquer serviço de hospedagem estática.

## Estrutura do Projeto
```text
.
├── archetypes/           # Arquétipos para novos conteúdos (ex.: posts)
├── assets/css/extended/  # Overrides de estilo (custom.css)
├── content/              # Markdown do site (posts, about, etc.)
├── docs/                 # Guias internos sobre personalização e UX
├── layouts/              # Sobrescritas de layouts do PaperMod
├── static/               # Arquivos estáticos servidos como estão
├── build.sh              # Script que instala e executa o Hugo fixo
├── hugo.yaml             # Configuração principal
└── public/               # Saída gerada (não editar manualmente)
```

## Requisitos
- Hugo `v0.146.0` (o script `build.sh` baixa automaticamente se necessário).
- `curl` e `tar` para executar o script de build em ambientes Unix-like.
- Opcional: navegador para visualizar o servidor local.

## Como Executar
### Ambiente local (hot reload)
```bash
hugo server -D
```
Roda o servidor em `http://localhost:1313`, incluindo rascunhos (`draft: true`).

### Build de produção
```bash
hugo --gc --minify
```
Gera a versão otimizada removendo assets órfãos.

```bash
./build.sh
```
Garante a versão oficial do Hugo e executa o build completo (recomendado antes de publicar).

## Fluxo de Conteúdo
- Crie novos posts com:
  ```bash
  hugo new posts/meu-post.md
  ```
- Use nomes de arquivo em *kebab-case* e mantenha o front matter em YAML (`title`, `date`, `draft`, `tags`).
- Para conteúdos em rascunho, mantenha `draft: true` até a revisão final.

## Personalização de Tema
- Ajuste cores e variáveis em `assets/css/extended/custom.css`.
- Componentes ou layouts customizados devem ir para `layouts/` (não altere arquivos em `themes/PaperMod`).
- Ícones sociais são configurados em `hugo.yaml` (`params.socialIcons`).

## Documentação Interna
- `docs/1-personalizacao.md`: guia de personalização.
- `docs/2-criacao-de-conteudo.md`: passos para publicar conteúdo.
- `docs/3-mudanca-tema-navy.md`: histórico do tema azul-marinho.
- `docs/4-avaliacao-ui-ux.md`: relatório de UX.

## Contribuição
- Consulte `AGENTS.md` para orientações completas (estrutura, comandos e revisão).
- Mantenha mensagens de commit no imperativo e descreva no pull request os testes executados.
- Sempre valide com `./build.sh` antes de enviar alterações.

## Licença
Distribuído sob a [Licença MIT](LICENSE).
