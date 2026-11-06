# Calculadora - Preço atualizado com o IPCA

Calculadora online para o cliente conferir o valor faturado: parte do **preço contratado sem tributos**, aplica a **correção do IPCA desde a data-base** e inclui **PIS/Cofins e ICMS "por dentro"**.

## Como o cálculo é feito

1. **Preço reajustado** = Preço contratado × Fator IPCA
   (Fator IPCA = produto de (1 + IPCA mensal) no período)
2. **Preço c/ PIS/Cofins** = Preço reajustado ÷ (1 − PIS − Cofins)
3. **Preço final** = Preço c/ PIS/Cofins ÷ (1 − ICMS)
4. **Total da fatura** = Preço final × Volume (MWh)

O IPCA vem automaticamente da API do Banco Central (série SGS 433). Se ela não responder, a calculadora usa a do IBGE (SIDRA, tabela 1737). O cliente também pode digitar o IPCA à mão.

## Publicar no GitHub Pages (link público, sem login)

1. Entre em <https://github.com> e clique em **New repository**.
2. Dê um nome, por exemplo `calculadora`, e marque **Public**. Clique em **Create repository**.
3. Na página do repositório, clique em **uploading an existing file** e arraste `index.html` e `README.md`. Clique em **Commit changes**.
4. Vá em **Settings → Pages**. Em *Build and deployment*, escolha **Deploy from a branch**, depois a branch **main** e a pasta **/ (root)**. Clique em **Save**.
5. Em 1 ou 2 minutos o link aparece no topo da mesma página:
   `https://SEU-USUARIO.github.io/calculadora/`

Qualquer pessoa com o link consegue usar, sem login.

**Domínio próprio (opcional):** em Settings → Pages → *Custom domain*, informe por exemplo `calculadora.bepenergia.com.br` e crie um registro CNAME no DNS apontando para `SEU-USUARIO.github.io`.

## Personalizar

No `index.html`, procure o bloco `CONFIG` (no início do `<script>`):

```js
const CONFIG = {
  empresa: "BEP Energia",
  sigla: "BEP",
  contato: "comercial@bepenergia.com.br",
  pisPadrao: 1.65,
  cofinsPadrao: 7.60,
  icmsPadrao: 18.00,
  casasPreco: 2
};
```

Para trocar a cor da marca, altere `--brand` no início do `<style>`.

## Enviar uma simulação pronta para o cliente

Preencha a calculadora e clique em **Copiar link desta simulação**. O link guarda todos os valores. Quem abrir já vê o cálculo preenchido.

---
*Simulação para conferência. Os valores oficiais são os da nota fiscal.*
