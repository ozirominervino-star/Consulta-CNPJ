# Consulta CNPJ + Sintegra

Aplicativo de página única para consultar CNPJ usando a API pública do ReceitaWS e, se o CNPJ existir, usar a UF retornada para orientar a consulta no Sintegra oficial.

## Recursos

- Consulta pelo ReceitaWS via JSONP, compatível com uso direto no navegador.
- Resumo no topo com situação cadastral, Simples Nacional, porte, UF e última atualização.
- Etapa Sintegra: confirma o CNPJ, identifica a UF e abre o portal oficial do Sintegra para selecionar o estado correto.
- Botão para copiar o CNPJ sem pontuação para colar no Sintegra.
- Registro automático das consultas realizadas.
- Botão `Consultar histórico` para visualizar os registros salvos.
- Botão `Sincronizar histórico` para enviar ao Firebase os registros que estavam salvos apenas no dispositivo atual.
- Botão `Alterar selecionado` para reabrir um CNPJ do histórico e atualizar a ficha/decisão.
- Botão `Excluir selecionado` para apagar um registro do histórico local e, se conectado, também do Firebase.
- Campo de Inscrição Estadual quando a informação vier disponível no retorno.
- Alertas básicos de risco cadastral, como empresa não ativa, cadastro recente, ausência de telefone/e-mail e capital social baixo.
- Recomendação interna salva no navegador: liberado, PIX à vista, analisar crédito, não vender no prazo ou cadastro incompleto.
- Sincronização opcional com Firebase/Firestore para acessar decisões e histórico em mais de um dispositivo.
- Botão para copiar um resumo pronto para WhatsApp, cadastro ou análise interna.
- Botão para imprimir ou salvar a ficha em PDF pelo navegador.
- Histórico local das últimas consultas.
- Dados técnicos do ReceitaWS agrupados em uma área recolhida.

## Como usar

Abra o arquivo `index.html`, digite o CNPJ e clique em `Consultar`. Se o CNPJ existir, use o botão `Abrir Sintegra oficial`, selecione a UF indicada e cole o CNPJ quando o portal solicitar.

Se consultas antigas não aparecerem em outro dispositivo, abra o app no dispositivo onde elas aparecem e clique em `Sincronizar histórico`.

Observação: a API pública do ReceitaWS tem limite de consultas por minuto e pode retornar dados de cache.

## Como testar com Firebase

O app já está com o `firebaseConfig` preenchido no arquivo `index.html`.

1. Verifique se o Cloud Firestore está ativo no Firebase.
2. Abra o app e clique em `Testar Firebase`.
3. Se o teste gravar corretamente, use `Sincronizar histórico` no dispositivo onde as consultas antigas aparecem.
4. No outro dispositivo/usuário, clique em `Consultar histórico`.

Para teste inicial, as regras do Firestore precisam permitir leitura e gravação. Em produção, use autenticação e regras restritas.
