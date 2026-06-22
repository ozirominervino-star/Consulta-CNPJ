# Consulta CNPJ + Sintegra

Aplicativo de página única para consultar CNPJ usando a API pública do ReceitaWS e, se o CNPJ existir, usar a UF retornada para orientar a consulta no Sintegra oficial.

## Recursos

- Consulta pelo ReceitaWS via JSONP, compatível com uso direto no navegador.
- Resumo no topo com situação cadastral, Inscrição Estadual, Simples Nacional, porte, UF, última atualização, status comercial e anexo SERASA.
- Etapa Sintegra: confirma o CNPJ, identifica a UF e abre o portal oficial do Sintegra para selecionar o estado correto.
- Botão para copiar o CNPJ sem pontuação para colar no Sintegra.
- Campo para inserir e salvar manualmente a Inscrição Estadual encontrada no Sintegra.
- Anexo de PDF da consulta SERASA vinculado ao CNPJ consultado, com indicação no resumo e no histórico.
- Botão `Enviar PDF para nuvem` para sincronizar manualmente um PDF que ficou apenas no dispositivo original.
- Registro automático das consultas realizadas.
- Botão `Consultar histórico` para visualizar os registros salvos.
- Botão `Sincronizar histórico` para enviar ao Firebase os registros que estavam salvos apenas no dispositivo atual.
- Botão `Alterar selecionado` para reabrir um CNPJ do histórico e atualizar a ficha/decisão.
- Botão `Excluir selecionado` para apagar um registro do histórico local e, se conectado, também do Firebase.
- Campo de Inscrição Estadual quando a informação vier disponível no retorno.
- Alertas básicos de risco cadastral, como empresa não ativa, cadastro recente, ausência de telefone/e-mail e capital social baixo.
- Recomendação interna salva no navegador: liberado, faturado, PIX à vista, analisar crédito, não vender no prazo ou cadastro incompleto.
- Sincronização opcional com Firebase/Firestore para acessar decisões e histórico em mais de um dispositivo.
- Sincronização opcional do PDF SERASA via Firebase Storage, quando as regras do Storage estiverem liberadas.
- Login opcional via Firebase Authentication por e-mail/senha.
- Histórico em tabela pesquisável por CNPJ, razão social, UF, situação, status comercial, Serasa ou responsável.
- Salvamento da ficha completa no Firebase, incluindo retorno ReceitaWS, alertas, validações, decisão interna e metadados do PDF SERASA.
- Status de validação para Receita, Sintegra e Crédito.
- Botão para copiar um resumo pronto para WhatsApp, cadastro ou análise interna.
- Botão para gerar ficha/PDF pelo navegador.
- Histórico local das últimas consultas.
- Dados técnicos do ReceitaWS agrupados em uma área recolhida.

## Como usar

Abra o arquivo `index.html`, digite o CNPJ e clique em `Consultar`. Se o CNPJ existir, use o botão `Abrir Sintegra oficial`, selecione a UF indicada e cole o CNPJ quando o portal solicitar.

Depois de consultar o Sintegra, informe a Inscrição Estadual no campo `Inscrição Estadual encontrada no Sintegra` e clique em `Salvar IE`. A informação ficará salva na ficha, no resumo, no histórico local e, se o Firebase estiver ativo, também será sincronizada.

Após consultar o SERASA, use o botão `Anexar PDF SERASA` para selecionar o relatório em PDF. O arquivo fica vinculado ao CNPJ consultado, entra no histórico e pode ser aberto ou removido pela própria ficha. Localmente, o arquivo é salvo no navegador por IndexedDB. Para abrir em outro dispositivo, ele precisa aparecer como `PDF na nuvem`. Se aparecer como `PDF local` ou `Pendente`, abra o app no dispositivo onde o arquivo foi anexado e clique em `Enviar PDF para nuvem`.

Se consultas antigas não aparecerem em outro dispositivo, abra o app no dispositivo onde elas aparecem e clique em `Sincronizar histórico`. Para PDFs, o histórico sozinho não leva o arquivo; é necessário usar `Enviar PDF para nuvem` ou anexar novamente o PDF no novo dispositivo.

Observação: a API pública do ReceitaWS tem limite de consultas por minuto e pode retornar dados de cache.

## Como testar com Firebase

O app já está com o `firebaseConfig` preenchido no arquivo `index.html`.

1. Verifique se o Cloud Firestore está ativo no Firebase.
2. Para sincronizar PDFs SERASA entre dispositivos, verifique também se o Firebase Storage está ativo.
3. Abra o app e clique em `Testar Firebase`.
4. O teste agora precisa gravar e ler. Se falhar, o app mostra o diagnóstico do Firebase na tela.
5. Se precisar testar regras abertas temporariamente, clique em `Copiar regras de teste`. O texto copiado inclui regras separadas para Cloud Firestore e Firebase Storage. Cole cada bloco no local correto do Firebase.
6. Se o teste gravar corretamente, use `Sincronizar histórico` no dispositivo onde as consultas antigas aparecem.
7. Para PDFs que aparecem como `PDF local`, abra a ficha no dispositivo original e clique em `Enviar PDF para nuvem`.
8. No outro dispositivo/usuário, clique em `Consultar histórico` e depois abra a ficha do CNPJ.

Para teste inicial, as regras do Firestore precisam permitir leitura e gravação. Para anexos SERASA sincronizados, as regras do Storage também precisam permitir leitura e gravação na pasta `serasa_pdfs`. Em produção, use autenticação e regras restritas.

## Login e segurança

Para usar regras seguras:

1. No Firebase, ative `Authentication`.
2. Em `Sign-in method`, habilite `Email/senha`.
3. Crie o primeiro acesso pelo próprio app, no painel `Acesso`.
4. Depois troque as regras abertas pelas regras de produção copiadas no botão `Copiar regras de teste`.


## Observação sobre anexos SERASA

O PDF pode conter informações sensíveis de crédito. Mantenha o acesso ao app e ao Firebase restrito aos usuários autorizados. Sem Firebase Storage, o anexo fica disponível apenas no navegador onde foi anexado. O histórico pode indicar `PDF local` ou `Pendente`, mas outro dispositivo só conseguirá abrir o arquivo quando ele for enviado ao Firebase Storage ou anexado novamente nesse novo dispositivo.
