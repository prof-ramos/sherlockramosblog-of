# Repository Guidelines

## Project Structure & Module Organization
- Hugo + PaperMod comandam o site; ajustes globais vivem em `hugo.yaml`.
- Conteúdo Markdown fica em `content/` (ex.: `posts/`, `about/`); gere rascunhos com `hugo new posts/nome-do-post.md`, baseado em `archetypes/default.md`.
- Sobrescritas de layout moram em `layouts/` e estilos próprios em `assets/css/extended/custom.css`; trate `themes/PaperMod` como somente leitura para facilitar updates.
- Arquivos estáticos pertencem a `static/`, dados estruturados a `data/`, e manuais internos a `docs/`.
- `public/` é saída gerada e não deve ser editada; `resources/` guarda caches refeitos quando o Hugo roda com `--gc`.

## Build, Test, and Development Commands
- `hugo server -D`: inicia ambiente local com live reload e inclui itens `draft`.
- `hugo --gc --minify`: gera build de produção, limpa assets órfãos e minifica HTML/CSS/JS.
- `./build.sh`: instala Hugo v0.146.0 se necessário e executa o pipeline oficial antes de deploy ou PR.

## Coding Style & Naming Conventions
- Nomeie arquivos em kebab-case (`content/posts/analise-ux.md`) e mantenha o texto em português salvo indicação contrária.
- Front matter deve seguir YAML com chaves `title`, `date`, `draft`, `tags`, `summary`.
- Prefira headings curtos, evite HTML embutido e use shortcodes com moderação para preservar compatibilidade do tema.
- Em `custom.css`, utilize indentação de quatro espaços e agrupe variáveis por modo claro/escuro.

## Testing Guidelines
- Durante o desenvolvimento, execute `hugo server -D` e navegue pelas páginas alteradas, monitorando avisos no terminal.
- Antes de abrir PR, rode `hugo --gc --printI18nWarnings --printPathWarnings` para detectar traduções, links ou assets problemáticos.
- Revise os diffs em `public/` apenas para confirmar que refletem alterações planejadas; remova arquivos órfãos quando apontados pelo Hugo.
- Não há suíte automatizada: documente verificações manuais e anexe screenshots para ajustes visuais relevantes.

## Commit & Pull Request Guidelines
- Mensagens de commit devem ser imperativas, sentence case e sem ponto final (`Atualize paleta navy`).
- Separe commits por escopo (conteúdo, layout, estilo) e referencie issues relacionadas quando existirem.
- PRs precisam incluir resumo objetivo, passos de validação, evidências visuais e confirmação da execução de `./build.sh`.
- Garanta branch sincronizado com `main` e ausência de artefatos gerados antes da revisão.

## Security & Deployment Notes
- Nunca versione segredos; configure variáveis sensíveis na plataforma de hospedagem.
- Para pré-visualizações, publique `public/` em Netlify, Vercel ou GitHub Pages e valide cabeçalhos de cache após deploy.
