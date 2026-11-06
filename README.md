# Calculadora - Preço atualizado com o IPCA

Calculadora online para o cliente conferir o valor faturado: parte do **preço contratado sem tributos**, aplica a **correção do IPCA desde a data-base** e inclui **PIS/Cofins e ICMS "por dentro"**.

## Como o cálculo é feito

Mesma sequência e arredondamento da memória de cálculo do reajuste:

1. **Preço + PIS/Cofins** = Preço do contrato ÷ (1 − PIS − Cofins)
2. **Fator IPCA** = produto de (1 + IPCA mensal), do mês da data-base até o mês de aniversário do suprimento (inclusive)
   - O aniversário é o mês de início do suprimento e, depois, a cada 12 meses.
   - O novo preço vale a partir do mês seguinte ao aniversário, depois que o IPCA do aniversário foi divulgado.
3. **Preço + PIS/Cofins + IPCA** = (1) × Fator IPCA
4. **Preço vigente** = (3) ÷ (1 − ICMS)
5. **Total da fatura** = Preço vigente × Volume (MWh)

Cada etapa é arredondada para 2 casas; o fator IPCA, para 6 casas. PIS (1,65%) e Cofins (7,60%) são fixos; só o ICMS é editável.

O IPCA vem automaticamente da API do Banco Central (série SGS 433). Se ela não responder, a calculadora usa a do IBGE (SIDRA, tabela 1737). Se o IPCA acumulado for negativo, o preço é mantido (nunca há deflação).

## Publicar no GitHub Pages (link público, sem login)

1. Entre em <https://github.com> e clique em **New repository**.
2. Dê um nome, por exemplo `calculadora`, e marque **Public**. Clique em **Create repository**.
3. Na página do repositório, clique em **uploading an existing file** e arraste `index.html` e `README.md`. Clique em **Commit changes**.
4. Vá em **Settings → Pages**. Em *Build and deployment*, escolha **Deploy from a branch**, depois a branch **main** e a pasta **/ (root)**. Clique em **Save**.
5. Em 1 ou 2 minutos o link aparece no topo da mesma página:
   `https://SEU-USUARIO.github.io/calculadora/`

Qualquer pessoa com o link consegue usar, sem login.

**Domínio próprio (opcional):** em Settings → Pages → *Custom domain*, informe por exemplo `calculadora.suaempresa.com.br` e crie um registro CNAME no DNS apontando para `SEU-USUARIO.github.io`.

## Personalizar

No `index.html`, procure o bloco `CONFIG` (no início do `<script>`):

```js
const CONFIG = {
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
