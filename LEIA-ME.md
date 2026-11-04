# Consulta às Câmaras Técnicas · Desafios e Diretrizes · Plano Maranhão 2050

Formulário público (GitHub Pages) que grava as respostas numa planilha Google da SEPLAN.

```
Respondente → index.html (GitHub Pages) → Apps Script (Codigo.gs) → Planilha Google (abas Respostas e Itens)
```

Ninguém precisa de conta para responder. Só quem tem acesso à planilha vê as respostas.

## Parte 1 · Planilha e script (receber as respostas)

1. Com a conta Google da SEPLAN, crie uma planilha em branco, por exemplo *Consulta Desafios e Diretrizes MA 2050 – Respostas*.
2. Menu **Extensões → Apps Script**.
3. Apague o conteúdo do arquivo `Código.gs`, cole todo o conteúdo de `Codigo.gs` e salve (ícone de disquete).
4. Na barra superior, selecione a função **configurar** e clique em **Executar**. Na primeira vez o Google pede autorização: escolha a conta, clique em *Avançado → Acessar (não seguro)* e em *Permitir*. Esse aviso aparece em todo script próprio que ainda não foi verificado pelo Google. Na planilha surgem as abas **Respostas** e **Itens**.
5. Clique em **Implantar → Nova implantação**. Na engrenagem, escolha **App da Web**.
   - Descrição: `consulta v1`
   - Executar como: **Eu**
   - Quem pode acessar: **Qualquer pessoa**
6. Clique em **Implantar** e copie a **URL do app da Web** (termina em `/exec`).
7. Teste: abra a URL no navegador. Deve aparecer `{"ok":true,"servico":"consulta-ma2050"}`.

> "Qualquer pessoa" se refere a quem pode **enviar** dados para o script. A planilha continua privada.

## Parte 2 · Página no GitHub (publicar o formulário)

1. Abra `index.html` num editor de texto (Bloco de Notas ou VS Code) e procure:
   `const ENDPOINT = 'COLE_AQUI_A_URL_DO_APPS_SCRIPT';`
   Troque o texto entre aspas pela URL copiada na Parte 1 e salve.
2. No GitHub da organização (`suprogseplan`), clique em **New repository**. Nome sugerido: `consulta-desafios-ma2050`, **Public**. Clique em **Create repository**.
3. No repositório, clique em **Add file → Upload files**, arraste o `index.html` (e este LEIA-ME, se quiser) e clique em **Commit changes**.
4. Vá em **Settings → Pages**. Em *Build and deployment*: Source **Deploy from a branch**, Branch **main**, pasta **/(root)**. Clique em **Save**.
5. Depois de 1 a 2 minutos o endereço aparece no topo da página de Pages:
   `https://suprogseplan.github.io/consulta-desafios-ma2050/`
   Esse é o link que vai para as Câmaras Técnicas.

> Repositórios públicos deixam o código visível, mas não as respostas: elas ficam só na planilha. A URL do script aparece no código, por isso o script tem proteções (campo oculto contra robôs, limite de tamanho e bloqueio de fórmulas).

## Parte 3 · Testar antes de divulgar

1. Abra o link, preencha a identificação e avalie um ou dois desafios.
2. Em **Revisar e enviar**, clique em **Enviar respostas**. Deve aparecer "Respostas enviadas em…".
3. Confira na planilha: uma linha em **Respostas** e uma linha por item em **Itens**.
4. Apague as linhas de teste na planilha.

## Como ficam os dados

**Aba Respostas**: uma linha por respondente.
`data_envio | id_resposta | nome | instituicao | camara | cargo | email | desafios_avaliados | diretrizes_avaliadas | novos_desafios | json_1…json_5`
As colunas `json_*` guardam a resposta completa (usada para reconstruir tudo depois). Não edite essas colunas.

**Aba Itens**: uma linha por item avaliado, pronta para tabela dinâmica.
`data_envio | id_resposta | nome | instituicao | camara | tipo | codigo | descricao | avaliacao | texto | relevancia | ativos`

| tipo | codigo | avaliacao | texto |
|---|---|---|---|
| desafio | D1…D22 | Manter / Ajustar redação / Fundir com outro / Excluir | justificativa e nova redação |
| diretriz | D1.1… | Manter / Ajustar / Excluir | nova redação ou justificativa |
| nova_diretriz | D1… | | diretriz proposta (ativos na coluna *ativos*) |
| lacuna | L1…L13 | Criar novo desafio / Nova diretriz / Já contemplado | redação sugerida |
| novo_desafio | N1-área | passivos (P1…P18) | diretrizes, evidência, instituições |
| geral | | | considerações gerais |

**Reenvio**: o respondente pode voltar no **mesmo navegador**, corrigir e reenviar. As linhas anteriores dele são substituídas. Se responder de outro computador, gera uma nova resposta.

## Parte 4 · Encerrar e consolidar

1. Para encerrar a consulta: no Apps Script, **Implantar → Gerenciar implantações → Arquivar**. O formulário passa a avisar que não conseguiu enviar.
2. Baixe a planilha em **Arquivo → Fazer download → Microsoft Excel (.xlsx)** e envie ao Claude. As respostas são carregadas na versão interativa no claude.ai, com a aba **Consolidação** (visível só para a proprietária), e é possível gerar o relatório de sistematização.

## Se precisar alterar o script depois

Edite o código, salve e vá em **Implantar → Gerenciar implantações → lápis (Editar) → Versão: Nova versão → Implantar**. Assim a URL continua a mesma. Uma *Nova implantação* gera outra URL, que precisaria ser trocada no `index.html`.
