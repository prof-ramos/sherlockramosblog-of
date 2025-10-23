# Configuração do Decap CMS

Este guia explica como configurar e usar o Decap CMS (anteriormente Netlify CMS) para gerenciar o conteúdo do blog via interface web.

## O que é Decap CMS?

Decap CMS é um sistema de gerenciamento de conteúdo open-source baseado em Git. Ele permite que você edite o conteúdo do seu site Hugo através de uma interface web amigável, sem precisar editar arquivos Markdown diretamente.

## Acesso ao CMS

Após a configuração, você poderá acessar o painel administrativo em:

```
https://prof-ramos.github.io/sherlockramosblog-of/admin/
```

## Configuração Inicial do GitHub OAuth

Para que o Decap CMS funcione, você precisa configurar autenticação via GitHub OAuth:

### 1. Criar um OAuth App no GitHub

1. Acesse: https://github.com/settings/developers
2. Clique em "OAuth Apps" → "New OAuth App"
3. Preencha os campos:
   - **Application name**: `Sherlock Ramos Blog CMS`
   - **Homepage URL**: `https://prof-ramos.github.io/sherlockramosblog-of/`
   - **Authorization callback URL**: `https://api.netlify.com/auth/done`
4. Clique em "Register application"
5. Anote o **Client ID** gerado
6. Clique em "Generate a new client secret" e anote o **Client Secret**

### 2. Opções de Autenticação

Você tem duas opções principais:

#### Opção A: Usar Netlify (Recomendado - Mais Fácil)

1. Faça deploy do site no Netlify (além do GitHub Pages)
2. No painel do Netlify, vá em: Site settings → Access control → OAuth
3. Clique em "Install provider"
4. Escolha "GitHub"
5. Cole o Client ID e Client Secret do OAuth App
6. O Netlify gerenciará a autenticação automaticamente

Depois, atualize o `static/admin/config.yml`:
```yaml
backend:
  name: github
  repo: prof-ramos/sherlockramosblog-of
  branch: main
  base_url: https://api.netlify.com
  auth_endpoint: auth
```

#### Opção B: GitHub Backend Direto (Desenvolvimento Local)

Para testar localmente, use o modo de desenvolvimento:

1. Clone o repositório
2. Execute: `npx decap-server`
3. Acesse: `http://localhost:8080/admin/`
4. Faça login com suas credenciais do GitHub

Atualize o `static/admin/config.yml` para desenvolvimento:
```yaml
backend:
  name: git-gateway
  # OU para desenvolvimento local:
  # name: test-repo
```

#### Opção C: Usar GitHub Actions para OAuth (Avançado)

Criar um servidor OAuth customizado usando GitHub Actions e Cloudflare Workers ou similar. Esta opção requer mais configuração técnica.

### 3. Alternativa: Usar GitHub Tokens (Apenas Local)

Para uso local sem servidor OAuth:

1. Gere um Personal Access Token no GitHub:
   - Acesse: https://github.com/settings/tokens
   - "Generate new token (classic)"
   - Selecione scopes: `repo` (acesso completo)
   - Anote o token

2. No navegador, abra o console de desenvolvedor em `/admin/`
3. Cole o token quando solicitado

**Nota**: Esta opção funciona apenas localmente e não é recomendada para produção.

## Recursos do CMS

### Collections Configuradas

1. **Posts** (`content/posts/`)
   - Criar, editar e excluir posts do blog
   - Campos: título, data, tags, resumo, imagem de capa, conteúdo
   - Rascunhos são marcados automaticamente

2. **Páginas**
   - Editar página "Sobre" (`content/about/_index.md`)

3. **Configurações**
   - Editar configurações do site em `hugo.yaml`
   - Alterar título, descrição, ícones sociais, etc.

### Funcionalidades

- ✅ Editor Markdown com preview
- ✅ Upload de imagens (salvas em `static/images/uploads/`)
- ✅ Interface em Português
- ✅ Rascunhos e publicação
- ✅ Tags e categorias
- ✅ Imagens de capa para posts

## Fluxo de Trabalho

1. Acesse `/admin/` no seu site publicado
2. Faça login com GitHub
3. Crie ou edite conteúdo
4. Clique em "Publicar"
5. O Decap CMS fará commit das alterações no GitHub
6. GitHub Actions automaticamente rebuilda e republica o site

## Estrutura de Arquivos

```
static/
├── admin/
│   ├── index.html          # Interface do Decap CMS
│   └── config.yml          # Configuração do CMS
└── images/
    └── uploads/            # Imagens enviadas via CMS
```

## Troubleshooting

### Erro de Autenticação

- Verifique se o OAuth App está configurado corretamente
- Confirme que a callback URL está correta
- Teste com `npx decap-server` localmente primeiro

### Não Consegue Salvar Alterações

- Verifique se você tem permissões de write no repositório
- Confirme que o branch `main` está correto no config.yml

### Preview Não Funciona

- O preview está desabilitado por padrão (`preview: false`)
- Para habilitar, remova essa linha do config.yml

## Referências

- Documentação Decap CMS: https://decapcms.org/docs/
- GitHub Backend: https://decapcms.org/docs/github-backend/
- Hugo + Decap CMS: https://decapcms.org/docs/hugo/

## Próximos Passos Recomendados

1. Configure o OAuth App no GitHub
2. Escolha entre Netlify (mais fácil) ou servidor OAuth customizado
3. Teste o CMS em `/admin/`
4. Crie seu primeiro post via interface web
5. Personalize os campos em `config.yml` conforme necessário
