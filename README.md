# Bellas Imports — Sistema

Sistema web da Bellas Imports para clientes, produtos, estoque, viagens ao Paraguai,
pedidos de WhatsApp, fluxo de caixa e futuras integrações com marketplaces.

## Estrutura

- `index.html` — aplicação web.
- `supabase/schema.sql` — banco de dados do Supabase.
- `supabase/config.js` — configuração do projeto Supabase.

## Publicar no GitHub Pages

1. Crie um repositório no GitHub.
2. Envie os arquivos deste projeto.
3. Em **Settings → Pages**, selecione a branch `main` e a pasta `/root`.
4. O GitHub Pages publicará o `index.html`.

## Configurar Supabase

1. Crie um projeto no Supabase.
2. Abra **SQL Editor**.
3. Cole e execute `supabase/schema.sql`.
4. Copie `supabase/config.js` para a raiz se preferir uma configuração externa, ou
   coloque os valores no objeto `window.BELLAS_SUPABASE` do `index.html`.
5. Use apenas a chave pública `anon`/publishable no frontend.
6. Nunca coloque `service_role` ou qualquer segredo no GitHub.

> Importante: esta versão já possui o desenho do banco e o cliente Supabase,
> mas os CRUDs da interface ainda usam `localStorage`. A próxima etapa é trocar
> os `DB.*` por consultas ao Supabase e ativar autenticação.

## WhatsApp

Para puxar automaticamente encomendas do WhatsApp será necessário:
- WhatsApp Business Platform / Cloud API;
- webhook público;
- uma função Edge do Supabase para receber as mensagens;
- regras para identificar cliente, produto, quantidade e viagem;
- gravação em `pedidos` e `pedido_itens`.

O token do WhatsApp deve ficar somente no backend/Edge Function, nunca no HTML.

## Mercado Livre

A integração deve usar OAuth e a API do Mercado Livre. Tokens privados ficam no
backend/Edge Functions. O estoque do Supabase deve ser a fonte central para evitar
venda de produto sem disponibilidade.

## Próxima versão recomendada

1. Login de funcionários.
2. CRUD real no Supabase.
3. Estoque com histórico de movimentações.
4. Vínculo automático de encomendas com a próxima viagem.
5. WhatsApp Cloud API + webhook.
6. Mercado Livre com sincronização de estoque e pedidos.
7. Dashboard financeiro real.
8. Controle de fornecedores e custos de viagem.


## Login e senha

O login do sistema usa **Supabase Auth** (`signInWithPassword`).

### Criar o primeiro usuário

No Supabase:
1. Abra **Authentication → Users**.
2. Clique em **Add user**.
3. Cadastre o e-mail e a senha do administrador.
4. Use esse e-mail e senha na tela de login da Bellas Imports.

Não existe senha de administrador fixa dentro do HTML. Isso é proposital para evitar
que a senha fique pública no GitHub.

### Publicação

Mantenha `logo-crop.png`, `index.html`, `supabase/config.js` e a pasta `supabase/`
no mesmo nível no GitHub Pages.
