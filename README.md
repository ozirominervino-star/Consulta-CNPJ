# Ficha Cadastral Comercial - CNPJ

Aplicativo de página única para consultar CNPJ usando a API pública do ReceitaWS e transformar o retorno em uma ficha comercial.

## Recursos

- Consulta pelo ReceitaWS via JSONP, compatível com uso direto no navegador.
- Resumo no topo com situação cadastral, Simples Nacional, porte, UF e última atualização.
- Campo de Inscrição Estadual quando a informação vier disponível no retorno.
- Alertas básicos de risco cadastral, como empresa não ativa, cadastro recente, ausência de telefone/e-mail e capital social baixo.
- Recomendação interna salva no navegador: liberado, PIX à vista, analisar crédito, não vender no prazo ou cadastro incompleto.
- Botão para copiar um resumo pronto para WhatsApp, cadastro ou análise interna.
- Botão para imprimir ou salvar a ficha em PDF pelo navegador.
- Histórico local das últimas consultas.
- Dados técnicos do ReceitaWS agrupados em uma área recolhida.

## Como usar

Abra o arquivo `index.html`, digite o CNPJ e clique em `Consultar`.

Observação: a API pública do ReceitaWS tem limite de consultas por minuto e pode retornar dados de cache.
