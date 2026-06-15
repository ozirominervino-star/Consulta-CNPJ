# Consulta de CNPJ - ReceitaWS

Aplicativo de página única para consultar CNPJ usando a API pública do ReceitaWS.

## O que foi ajustado

- A consulta agora usa somente o ReceitaWS, via JSONP, que é o meio indicado para funcionar direto no navegador.
- A tela mostra os mesmos grupos de informações retornados pelo ReceitaWS: dados da empresa, situação cadastral, endereço, atividades, QSA, Simples Nacional, SIMEI e informações técnicas.
- Foram removidas as tentativas de Inscrição Estadual/Sintegra, porque esses dados não fazem parte do retorno padrão do ReceitaWS.
- O erro visual da tela foi corrigido com uma renderização mais simples e segura.

## Como usar

Abra o arquivo `index.html`, digite o CNPJ e clique em `Consultar`.

Observação: a API pública do ReceitaWS tem limite de consultas por minuto e pode retornar dados de cache.
