## Gustavo Henrique — Desenvolvedor Backend .NET / C#

Trabalho com integrações fiscais e bancárias no Brasil: boleto, CNAB, PIX e NFS-e, quase
sempre em cima das bibliotecas nativas do ACBr. A parte que me interessa de verdade é o
que acontece quando várias empresas usam o mesmo processo ao mesmo tempo — concorrência,
isolamento de estado e as garantias que você precisa provar com teste, não com comentário
no código.

Também opero em produção o que escrevo: Kubernetes com Helm, deploy automatizado e
diagnóstico de incidente quando alguma coisa quebra às sete da manhã.

Aberto a oportunidades backend .NET, remoto ou híbrido em São Paulo.

### O que dá pra verificar por aqui

**Concorrência sobre biblioteca nativa.** Um handle da ACBrLib carrega estado mutável e
não é thread-safe, mas o mesmo processo emite boletos para centenas de empresas. O pool em
[`acbr-boleto-dotnet`](https://github.com/guustaaa/acbr-boleto-dotnet) é dimensionado por
concorrência em vez de por empresa: cada handle fica preso ao hash da configuração que o
inicializou, e não existe caminho de código que reconfigure um handle vivo para outra
empresa. 113 testes determinísticos rodam em CI sem a biblioteca nativa presente.

**Defeito de fornecedor diagnosticado em produção.** O motor de relatório nativo corrompia
PDFs ao reutilizar um handle e não expõe API de reset. A mitigação foi descartar o handle
depois de cada geração — com teste de regressão, e com a limitação documentada no README
em vez de escondida.

**Versionamento de layout fiscal.** Mudança de versão de NFS-e quebra emissão de formas
difíceis de prever. O
[harness](https://github.com/guustaaa/acbr-nfse-version-harness) processa as mesmas
entradas em versões diferentes e compara requisição, resposta e XML, isolando a diferença
antes de chegar em produção.

### Projetos

| Projeto | Problema que resolve | Stack |
|---|---|---|
| [acbr-boleto-dotnet](https://github.com/guustaaa/acbr-boleto-dotnet) | Emissão concorrente de boletos multiempresa sem vazamento de estado entre elas | C#, .NET 8, xUnit, GitHub Actions |
| [acbr-nfse-version-harness](https://github.com/guustaaa/acbr-nfse-version-harness) | Comparar processamento entre versões de layout de NFS-e antes do deploy | Object Pascal, Lazarus |
| [th-parfums-storefront](https://github.com/guustaaa/th-parfums-storefront) | Vitrine e painel administrativo entregues ponta a ponta | Next.js, TypeScript, Supabase |
| [linux-vm-stall-monitor](https://github.com/guustaaa/linux-vm-stall-monitor) | Detectar travamentos de VM Linux por lacuna no journal | Bash, PowerShell |

A edição pública do ACBr Boleto é autorizada pela Strategix e não contém credenciais,
certificados ou dados de clientes.

### Stack

`C#` · `.NET 8` · `PostgreSQL` · `SQL Server` · `xUnit` · `Docker` · `Kubernetes` ·
`Helm` · `Linux` · `GitHub Actions` · `Python` · `TypeScript`

Domínio: `ACBr` · `boleto` · `CNAB` · `PIX` · `NFS-e` · `P/Invoke` · `concorrência`

### Construindo agora

Uma API de registro de boleto em ASP.NET Core — idempotência, reconciliação de webhook
bancário e outbox, contra um banco simulado que responde duas vezes, responde tarde e às
vezes não responde. É o problema real de quem integra com banco, e é o que estou usando
para fechar as lacunas que eu ainda não tenho evidência pública: EF Core, mensageria e
teste de integração com container.

### Contato

[LinkedIn](LINKEDIN_URL) · gustavo.criser@gmail.com · São Paulo, SP
