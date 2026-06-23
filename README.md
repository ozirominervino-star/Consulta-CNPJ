# Consulta CNPJ + Sintegra

Aplicativo de página única para consultar CNPJ usando a API pública do ReceitaWS e, se o CNPJ existir, usar a UF retornada para orientar a consulta no Sintegra oficial.

## Recursos

- Consulta pelo ReceitaWS via JSONP, compatível com uso direto no navegador.
- Resumo no topo com situação cadastral, Inscrição Estadual, Simples Nacional, porte, UF, última atualização, status comercial e anexo SERASA.
- Etapa Sintegra: confirma o CNPJ, identifica a UF e abre o portal oficial do Sintegra para selecionar o estado correto.
- Campo para inserir e salvar manualmente a Inscrição Estadual encontrada no Sintegra.
- Anexo de PDF da consulta SERASA vinculado ao CNPJ consultado, com indicação no resumo e no histórico.
- Botão `Enviar PDF para nuvem` para sincronizar manualmente um PDF que ficou apenas no dispositivo original.
- Sincronização do PDF SERASA em blocos pelo Cloud Firestore, sem depender do Firebase Storage.
- Recuperação do PDF em outro dispositivo mesmo quando a referência principal da ficha não foi gravada corretamente, desde que os blocos estejam no Firestore.
- Registro automático das consultas realizadas e histórico pesquisável.
- Recomendação interna salva no navegador e, se conectado, no Firebase.
- Status de validação para Receita, Sintegra e Crédito.
- Botões para copiar CNPJ, copiar ficha e gerar ficha/PDF pelo navegador.
- Dados técnicos do ReceitaWS agrupados em área recolhida.

## Como usar

Abra o arquivo `index.html`, digite o CNPJ e clique em `Consultar`. Se o CNPJ existir, use o botão `Abrir Sintegra oficial`, selecione a UF indicada e cole o CNPJ quando o portal solicitar.

Depois de consultar o Sintegra, informe a Inscrição Estadual no campo `Inscrição Estadual encontrada no Sintegra` e clique em `Salvar IE`.

Após consultar o SERASA, use o botão `Anexar PDF SERASA` para selecionar o relatório em PDF. O arquivo fica salvo localmente no navegador por IndexedDB. Depois clique em `Enviar PDF para nuvem`. Quando aparecer `PDF na nuvem`, outros dispositivos autorizados deverão conseguir abrir o arquivo pela ficha do mesmo CNPJ.

Nesta versão, ao abrir a ficha em outro dispositivo, o app procura o PDF em dois lugares: primeiro na referência principal da ficha e, se ela estiver ausente, diretamente na subcoleção de blocos do Firestore. Isso corrige o caso em que o PDF aparece no Firebase, mas o outro dispositivo não encontra o anexo.

## Como testar com Firebase

O app já está com o `firebaseConfig` preenchido no arquivo `index.html`.

1. Verifique se o Cloud Firestore está ativo no Firebase.
2. Abra o app e clique em `Testar Firebase`.
3. O teste precisa gravar e ler no Firestore, inclusive um pequeno teste de PDF em blocos.
4. Se precisar testar regras abertas temporariamente, clique em `Copiar regras de teste` e cole o texto nas regras do Cloud Firestore.
5. No dispositivo onde o PDF foi anexado, consulte o CNPJ e clique em `Enviar PDF para nuvem`.
6. No outro dispositivo, entre com o mesmo acesso do Firebase ou use regras que permitam leitura, consulte o mesmo CNPJ e clique em `Abrir PDF`.

Para teste inicial, as regras do Firestore precisam permitir leitura e gravação em `fichas_cnpj/{document=**}` e `testes/{document=**}`. Como os PDFs SERASA são gravados em subcoleções dentro de `fichas_cnpj`, a regra recursiva cobre também os blocos do arquivo.

## Login e segurança

Para usar regras seguras:

1. No Firebase, ative `Authentication`.
2. Em `Sign-in method`, habilite `Email/senha`.
3. Crie o primeiro acesso pelo próprio app, no painel `Acesso`.
4. Depois troque as regras abertas pelas regras de produção copiadas no botão `Copiar regras de teste`.

## Observação sobre anexos SERASA

O PDF pode conter informações sensíveis de crédito. Mantenha o acesso ao app e ao Firebase restrito aos usuários autorizados. O anexo fica apenas no navegador enquanto aparecer como `PDF local` ou `Pendente`. Depois de clicar em `Enviar PDF para nuvem` e aparecer `PDF na nuvem`, outros dispositivos autorizados conseguem abrir o arquivo pela ficha do CNPJ.
