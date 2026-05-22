# ✦ PostAI — Gerador de Posts com IA

SaaS de geração de posts para redes sociais usando Claude AI. Pronto para deploy e monetização.

## 🚀 Rodar localmente

### 1. Instalar dependências
```bash
npm install
```

### 2. Configurar variáveis de ambiente
Edite o arquivo `.env.local` e adicione sua chave da API Anthropic:
```
ANTHROPIC_API_KEY=sua_chave_aqui
```
Obtenha sua chave em: https://console.anthropic.com

### 3. Iniciar o servidor
```bash
npm run dev
```
Acesse: http://localhost:3000

---

## ☁️ Deploy na Vercel (grátis)

### Opção 1 — Via GitHub (recomendado)
1. Crie um repositório no GitHub e faça push do projeto
2. Acesse https://vercel.com e conecte sua conta GitHub
3. Importe o repositório
4. Em "Environment Variables", adicione `ANTHROPIC_API_KEY`
5. Clique em Deploy ✓

### Opção 2 — Via CLI
```bash
npm i -g vercel
vercel
# Siga as instruções e adicione a variável ANTHROPIC_API_KEY quando solicitado
```

---

## 💳 Adicionar pagamentos (Stripe)

### 1. Criar conta no Stripe
- Acesse https://stripe.com e crie sua conta
- Copie as chaves em Dashboard > Developers > API Keys

### 2. Criar produtos
No Stripe Dashboard:
- Crie produto "Básico" → R$29/mês
- Crie produto "Pro" → R$79/mês

### 3. Adicionar ao .env.local
```
STRIPE_SECRET_KEY=sk_live_...
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_live_...
STRIPE_WEBHOOK_SECRET=whsec_...
```

### 4. Instalar SDK do Stripe
```bash
npm install stripe @stripe/stripe-js
```

---

## 🔐 Adicionar autenticação (Supabase)

### 1. Criar projeto no Supabase
- Acesse https://supabase.com e crie um projeto gratuito

### 2. Adicionar ao .env.local
```
NEXT_PUBLIC_SUPABASE_URL=https://xxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJ...
```

### 3. Instalar SDK
```bash
npm install @supabase/supabase-js @supabase/auth-helpers-nextjs
```

### 4. Criar tabela de usuários
No Supabase SQL Editor:
```sql
CREATE TABLE profiles (
  id UUID REFERENCES auth.users PRIMARY KEY,
  plan TEXT DEFAULT 'free',
  generations_today INT DEFAULT 0,
  last_reset DATE DEFAULT CURRENT_DATE,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

---

## 📁 Estrutura do projeto

```
postai/
├── app/
│   ├── api/
│   │   └── generate/
│   │       └── route.ts     ← API route (Claude AI)
│   ├── globals.css          ← Estilos globais
│   ├── layout.tsx           ← Layout raiz + fontes
│   ├── page.tsx             ← Página principal
│   └── page.module.css      ← Estilos da página
├── .env.local               ← Variáveis de ambiente
├── next.config.js
├── package.json
├── tailwind.config.js
└── tsconfig.json
```

---

## 💰 Monetização sugerida

| Plano | Preço | Limite |
|-------|-------|--------|
| Grátis | R$0 | 3 posts/dia |
| Básico | R$29/mês | 30 posts/dia |
| Pro | R$79/mês | Ilimitado + agendamento |

**Meta**: 50 assinantes Básico = R$1.450/mês

---

## 🛠 Stack

- **Framework**: Next.js 14 (App Router)
- **IA**: Claude claude-sonnet-4-20250514 via Anthropic SDK
- **Estilo**: CSS Modules + Tailwind
- **Fontes**: DM Serif Display + DM Sans (Google Fonts)
- **Deploy**: Vercel (grátis)
- **Pagamentos**: Stripe (a integrar)
- **Auth/DB**: Supabase (a integrar)
