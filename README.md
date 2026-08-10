## Gustavo Henrique — Desenvolvedor Backend .NET / C# e Python

Backend é onde eu quero estar, mas não é só o que eu faço. Trabalho com integrações fiscais
e bancárias no Brasil — boleto, CNAB, PIX e NFS-e — quase sempre em cima das bibliotecas
nativas do ACBr. A parte que me interessa de verdade é o que acontece quando várias empresas
usam o mesmo processo ao mesmo tempo: concorrência, isolamento de estado e as garantias que
você precisa provar com teste, não com comentário no código.

Também entrego as pontas. Instalo e opero Kubernetes bare-metal sobre Linux, automatizo
deploy combinando Helm com Bash, e construo o frontend quando o projeto pede. Já lidei com
RHEL, Ubuntu e Debian no mesmo cluster, cada um no papel que fazia sentido.

Aberto a oportunidades backend .NET ou Python, remoto ou híbrido em São Paulo.

### O que dá pra verificar por aqui

**Concorrência sobre biblioteca nativa.** Um handle da ACBrLib carrega estado mutável e não
é thread-safe, mas o mesmo processo emite boletos para centenas de empresas. O pool em
[`acbr-boleto-dotnet`](https://github.com/guustaaa/acbr-boleto-dotnet) é dimensionado por
concorrência em vez de por empresa: cada handle fica preso ao hash da configuração que o
inicializou, e não existe caminho de código que reconfigure um handle vivo para outra
empresa. 113 testes determinísticos rodam em CI sem a biblioteca nativa presente.

**Defeito de fornecedor diagnosticado em produção.** O motor de relatório nativo corrompia
PDFs ao reutilizar um handle e não expõe API de reset. A mitigação foi descartar o handle
depois de cada geração — com teste de regressão, e com a limitação documentada no README em
vez de escondida.

**Modelos que não fingem funcionar.** Em [`colab-finance`](https://github.com/guustaaa/colab-finance)
a validação é walk-forward justamente para não me enganar com look-ahead bias, e o
dimensionamento de posição sai por critério de Kelly em vez de chute. É um sistema de
pesquisa, não uma promessa de acurácia.

### Projetos

| Projeto | Problema que resolve | Stack |
|---|---|---|
| [acbr-boleto-dotnet](https://github.com/guustaaa/acbr-boleto-dotnet) | Emissão concorrente de boletos multiempresa sem vazamento de estado entre elas | C#, .NET 8, xUnit, GitHub Actions |
| [colab-finance](https://github.com/guustaaa/colab-finance) | Pesquisa de estratégias de câmbio com regime de mercado e validação sem look-ahead | Python, XGBoost, LightGBM, hmmlearn |
| [th-parfums-storefront](https://github.com/guustaaa/th-parfums-storefront) | Vitrine e painel administrativo entregues ponta a ponta, em deploy serverless | Next.js, TypeScript, Supabase, Vercel |
| [acbr-nfse-version-harness](https://github.com/guustaaa/acbr-nfse-version-harness) | Comparar processamento entre versões de layout de NFS-e antes do deploy | Object Pascal, Lazarus |

A edição pública do ACBr Boleto é autorizada pela Strategix e não contém credenciais,
certificados ou dados de clientes.

### Stack

**Backend** `C#` · `.NET 8` · `Python` · `FastAPI` · `APIs REST` · `microsserviços`
**Domínio** `ACBr` · `boleto` · `CNAB` · `PIX` · `NFS-e` · `P/Invoke` · `concorrência`
**Dados** `PostgreSQL` · `SQL Server`
**Infra** `Kubernetes bare-metal` · `Helm` · `Docker` · `RHEL` · `Ubuntu` · `Debian` · `Bash` · `GitHub Actions`
**Frontend** `TypeScript` · `React` · `Next.js`

### Construindo agora

Uma API de registro de boleto em ASP.NET Core — idempotência, reconciliação de webhook
bancário e outbox, contra um banco simulado que responde duas vezes, responde tarde e às
vezes não responde. É o problema real de quem integra com banco, e é o que estou usando para
fechar as lacunas que ainda não tenho evidência pública: EF Core, mensageria e teste de
integração com container.

### Contato

gustavo.criser@gmail.com · São Paulo, SP

<!-- PENDING: add LinkedIn here once the profile URL exists -->

