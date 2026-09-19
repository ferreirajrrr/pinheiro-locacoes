# Pinheiro Locações

Sistema de gestão para locação de equipamentos de construção (andaimes, escoras, plataformas, misturador de tinta, betoneira), feito para a **Pinheiro Locações**, de Caucaia-CE.

> Versão **0.1.0-beta**, um protótipo navegável para validar o fluxo com o cliente. Os dados são fictícios e ficam apenas na aba aberta.

## Por que este projeto existe

Hoje o controle da locadora é uma planilha de estoque e preços. Ela não responde às perguntas do dia a dia:

- Quanto tenho disponível **agora** e em uma data futura?
- Quem está com o equipamento, onde a obra fica e quando ele volta?
- Quem está atrasado e quanto devo cobrar (multa, acréscimos, desconto)?
- O equipamento que comprei está se pagando? Qual fornecedor vale mais a pena?
- Quanto entrou, quanto saiu e qual foi o resultado do mês?
- Como guardar os dados dos clientes sem descumprir a LGPD?

O sistema reúne tudo isso em um só lugar, pensado primeiro para o celular, porque o dono trabalha na rua e não na frente de um computador.

## O que faz

| Área | Conteúdo |
|---|---|
| **Painel** | Alertas, disponibilidade, devoluções próximas, mapa das obras, botões rápidos "Receber equipamento" e "Receber pagamento" |
| **Agenda e Locações** | Reservas por data, checklist de saída e devolução com fotos, caução, logística de entrega e coleta |
| **Orçamentos** | Criação, validade e conversão em locação |
| **Clientes** | Máscaras e validação de CPF/CNPJ/telefone, CEP automático, consentimento LGPD, exportação e anonimização, análise de risco |
| **Equipamentos** | Tabela de preços por período (1/7/15/30 dias), novo equipamento com dados de compra, ocupação, depreciação, retorno do investimento, manutenção, inspeção e baixa |
| **Fornecedores** | Cadastro, compras, cotações e comparação de preços |
| **Cobranças** | Registro de pagamento com acréscimos, multa e desconto, recibos, histórico e mensagem por WhatsApp ou e-mail |
| **Financeiro** | Caixa, DRE, contas a pagar e a receber, despesas, extrato e exportação em CSV |
| **Venda de equipamento** | Venda com dados fiscais e registro da nota, **desativada por padrão** (o sistema roda sem nota fiscal) |
| **Configurações** | Dados da empresa (saem nos documentos), usuários administradores e operadores, senha |

## Como foi feito

- Um único arquivo, [`index.html`](index.html), em HTML, CSS e JavaScript puro, sem build e sem dependências para instalar.
- Mobile-first: a base é o celular, com ajustes para tablet e computador.
- Senhas com PBKDF2-SHA256 (100 mil iterações) via `crypto.subtle`, bloqueio após 5 tentativas.
- Mapa com Leaflet e OpenStreetMap, endereços localizados pelo Nominatim, CEP pelo ViaCEP.

## Como usar

Abra pelo GitHub Pages do repositório, ou localmente:

```bash
python -m http.server 5180
```

Depois acesse `http://localhost:5180`. O mapa precisa de `http` ou `https`; abrindo o arquivo direto (`file://`) ele não carrega.

### Dados de demonstração

O sistema abre com dados fictícios para a apresentação. Para começar zerado, troque `const DEMO = true` por `false` no fim do script de `index.html`.

## Limites atuais

Este é um protótipo, não um sistema de produção:

- **Sem banco de dados.** Tudo fica na memória da aba; recarregar a página apaga o que foi digitado.
- **Login apenas no navegador.** Serve para demonstrar o fluxo, não protege dados reais. A versão de produção precisa de servidor, criptografia dos dados sensíveis, limite real de tentativas e log de auditoria.
- **Sem emissão automática de nota fiscal.** Exigiria contrato com um emissor, certificado digital e chave guardada no servidor.
- **Sem consulta automática a Serasa/SPC ou a bancos de segurança pública.** A análise de risco usa o histórico interno e consultas registradas manualmente; integrar exige contrato com um provedor e revisão jurídica.
- **Cobrança automática por WhatsApp** depende da API oficial da Meta (número verificado, modelos aprovados e custo por mensagem). Hoje o sistema abre a mensagem pronta.

## Próximos passos

1. Backend com banco de dados e isolamento por cliente (multi-tenant) desde o início.
2. Cobrança automática por WhatsApp Cloud API e e-mail.
3. Emissão de nota fiscal por um emissor integrado, quando o cliente decidir usá-la.
4. Integração com bureau de crédito.

---

Desenvolvido por [AURA](https://auralandingpages.com.br/).
