# Repository Guidelines

## Project Structure & Module Organization
- Hugo com tema PaperMod conduz o site; configurações centrais permanecem em `hugo.yaml`.
- Conteúdo Markdown mora em `content/` (ex.: `posts/`, `about/`); gere novos arquivos com `hugo new posts/nome-do-post.md`, baseado em `archetypes/default.md`.
- Sobrescritas de layout ficam em `layouts/`, enquanto estilos customizados vivem em `assets/css/extended/custom.css`; mantenha `themes/PaperMod` intacto para absorver atualizações.
- Arquivos estáticos residem em `static/`, dados estruturados em `data/`, e documentação complementar em `docs/`.
- `public/` reúne a saída gerada e não deve ser editada; `resources/` guarda caches recompilados pelo Hugo quando executado com `--gc`.

## Build, Test, and Development Commands
- `hugo server -D`: inicia servidor local com live reload e inclui rascunhos (`draft: true`).
- `hugo --gc --minify`: gera build otimizado, limpando assets órfãos e minificando HTML, CSS e JS.
- `./build.sh`: garante a instalação do Hugo v0.146.0 e reproduz o build aprovado para deploy.

## Coding Style & Naming Conventions
- Nomeie arquivos em kebab-case (`content/posts/analise-ux.md`) e priorize texto em português.
- Front matter usa YAML com chaves `title`, `date`, `draft`, `tags`, `summary`.
- Prefira headings curtos, evite HTML bruto e use shortcodes apenas quando necessários.
- Em `custom.css`, siga indentação de quatro espaços e agrupe variáveis por modo claro/escuro, registrando mudanças de paleta em comentários curtos.

## Testing Guidelines
- Durante o desenvolvimento, execute `hugo server -D` e valide manualmente as páginas afetadas observando avisos no terminal.
- Antes de abrir PR, rode `hugo --gc --printI18nWarnings --printPathWarnings` para localizar traduções ausentes, links quebrados e assets não utilizados.
- Analise a saída em `public/` para garantir que os diffs refletem apenas alterações intencionais; remova arquivos órfãos se reportados.
- Não há suíte automatizada: documente passos de verificação manual e inclua screenshots para mudanças visuais relevantes.

## Commit & Pull Request Guidelines
- Mensagens de commit devem ser imperativas, em sentence case e sem ponto final (`Atualize paleta navy`).
- Separe commits por escopo (conteúdo, layout, estilo) e referencie issues relacionadas quando existirem.
- PRs precisam incluir resumo objetivo, passos de validação, evidências visuais e confirmação da execução de `./build.sh`.
- Sincronize o branch com `main` e garanta ausência de artefatos gerados antes de solicitar revisão.

## Deployment & Configuration Tips
- Não versione segredos; configure variáveis sensíveis diretamente na plataforma de hospedagem.
- Para pré-visualizações estáticas, publique `public/` em hosts como Netlify, Vercel ou GitHub Pages.
