# Radar Comex | Intelligence Desk

> Monitoramento de comércio exterior para pneus e matérias-primas em toda a América do Sul.

| Área | Funcionalidade |
|---|---|
| Visão executiva | Indicadores, manchetes, riscos e distribuição de eventos |
| Central de eventos | Busca, filtros combinados, detalhe da medida, CSV |
| Inteligência fiscal | NCM, SH, NALADI/NALADISA e NANDINA |
| Cobertura e auditoria | 12 países, registro das execuções e lacunas |
| Minha lista | Acompanhamento de eventos no navegador |

## Acesso

- [Interface do portal (código HTML)](index.html)
- [Base histórica de eventos e execuções](radar.json)

O GitHub exibe o código HTML; para o painel funcionar como site, é necessário hospedá-lo via GitHub Pages ou outro servidor HTTP que sirva os dois arquivos. O repositório permanece privado. No GitHub Pages, a disponibilidade para repositórios privados depende do plano, e a privacidade do site deve ser verificada separadamente.

### Publicação

1. Verifique a visibilidade do repositório e as opções em **Settings → Pages**.
2. Se o plano permitir, selecione **Deploy from a branch**, branch **main**, pasta **/(root)**.
3. Após o deploy, verifique a URL apresentada pelo GitHub e se os dados podem ser acessados apenas pelas pessoas pretendidas.
4. Para teste local, baixe ambos os arquivos na mesma pasta e execute `python -m http.server 8000`. Acesse `http://localhost:8000`.

## Operação

A tarefa diária do ChatGPT está configurada para ler e atualizar `radar.json` e enviar o boletim autorizado por e-mail, separadamente. O primeiro ciclo completo de publicação automática ainda precisa ser confirmado. O navegador relê a base a cada cinco minutos.

A interface usa uma base JSON versionada no GitHub, não PostgreSQL. A base inicial contém quatro registros importados do boletim anterior, marcados como **revalidação pendente**. Não há comprovação de cobertura integral dos 12 países.

## Integridade e governança

- Identificador estável e histórico de revisões por evento.
- Não se deve duplicar notícias ou sobrescrever o histórico.
- Risco e verificação são campos independentes; uma medida de alto risco pode estar pendente de confirmação.
- Correlações fiscais pendentes não devem ser aplicadas a declarações aduaneiras.
- A classificação e vigência de cada medida devem ser conferidas no ato oficial.
- Não armazenar e-mails, senhas, tokens ou dados corporativos confidenciais nesta base.

## Estrutura

`index.html`: interface responsiva, JavaScript sem dependências externas, filtros, visualizações e exportação.

`radar.json`: schema_version, updated_at, events, runs. Cada evento contém identificador, assunto, país, tema, risco, datas, códigos fiscais, fonte, status jurídico, ação e histórico. O campo verified indica verificação documental, não autorização para uso aduaneiro.
