# Consulta Cadastral Avançada (CNPJ + Sintegra IE)

Este é um sistema web leve e de página única (SPA) para consulta automatizada de dados cadastrais de CNPJ e validação de Inscrições Estaduais (Sintegra).

## 📂 Estrutura do Pacote
* `index.html` - Arquivo principal contendo a interface, estilização moderna e lógica de integração com APIs.
* `image_b77415.png` - Logotipo do aplicativo configurado como Favicon (ícone de identificação no navegador).

## 🚀 Como Executar Localmente
Para garantir que o ícone do navegador (Favicon) e as requisições funcionem perfeitamente sem bloqueios de segurança dos navegadores (`file:///`), siga um dos métodos abaixo:

### Método 1: GitHub Pages (Recomendado)
1. Suba esta pasta para um repositório público no GitHub.
2. Acesse as configurações (**Settings**) > **Pages**.
3. Ative a publicação apontando para a branch principal (`main`/`root`).
4. Seu app estará online com o ícone funcionando perfeitamente!

### Método 2: Extensão Live Server (VS Code)
1. Abra esta pasta no VS Code.
2. Instale a extensão **Live Server**.
3. Clique em **Go Live** no canto inferior direito para rodar o app sob um servidor local estável (`http://127.0.0.1:5500`).

## 🛠️ Recursos Integrados
* Consumo primário via **BrasilAPI** (com espelhamento em lote das Inscrições Estaduais).
* Fallback de contingência automática via **ReceitaWS** em JSONP.
* Tratamento e formatação dinâmica de moedas, datas e CNAEs.
