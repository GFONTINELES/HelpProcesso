# 📋 Central de Processos e Riscos — Ferreira Supermercados

Sistema web em Python/Streamlit para visualização do repositório de processos corporativos.

---

## 🚀 Como instalar e rodar

### 1. Pré-requisitos
- Python 3.10 ou superior instalado
- Acesso à internet

### 2. Clone ou baixe os arquivos
Coloque todos os arquivos numa pasta, ex: `fff_processos/`

### 3. Instale as dependências
Abra o terminal na pasta do projeto e execute:
```bash
pip install -r requirements.txt
```

### 4. Configure a API Key do Google (obrigatório para ler a planilha)

#### Passo a passo para criar a API Key:

1. Acesse: https://console.cloud.google.com/
2. Crie um novo projeto (ou use um existente)
3. No menu lateral, vá em **"APIs e Serviços"** → **"Biblioteca"**
4. Busque por **"Google Sheets API"** e clique em **"Ativar"**
5. Vá em **"APIs e Serviços"** → **"Credenciais"**
6. Clique em **"+ Criar Credenciais"** → **"Chave de API"**
7. Copie a chave gerada (começa com `AIzaSy...`)

> ⚠️ **Importante:** A planilha do Google Sheets deve estar com visibilidade
> **"Qualquer pessoa com o link pode visualizar"** (já está configurado assim).

### 5. Execute o sistema
```bash
streamlit run app.py
```

O sistema abrirá no navegador em `http://localhost:8501`

### 6. Insira a API Key
Na tela do sistema, no campo **"🔑 Google API Key"** na barra lateral,
cole a chave criada no passo 4.


## 📊 Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| **Filtros** | Objetivo Estratégico, Macroprocessos, Processos, Status, Criticidade, Tipo de Atividade, Tipo de Critério |
| **Busca** | Texto livre em todos os campos |
| **Cards** | Total de processos, Ativos, Em Atualização, Pendentes |
| **Badges** | Status e Criticidade com cores visuais |
| **Links PDF** | Botão clicável direto para o documento PDF no Google Drive |
| **Cache** | Dados em cache por 5 minutos (evita requisições desnecessárias) |
| **Atualização** | Botão "Atualizar dados" para forçar recarga |

---

## 📁 Estrutura dos arquivos

```
fff_processos/
├── app.py              # Aplicação principal Streamlit
├── sheets_reader.py    # Conector Google Sheets API v4
├── requirements.txt    # Dependências Python
└── README.md           # Este arquivo
```

---

## 🔒 Segurança

- A API Key é inserida no campo de senha (não fica visível na tela)
- Para ambientes de produção (servidor), crie um arquivo `.streamlit/secrets.toml`:

```toml
GOOGLE_API_KEY = "AIzaSy..."
```

E no `app.py`, substitua o `st.text_input` por:
```python
api_key = st.secrets["GOOGLE_API_KEY"]
```

---

## 🛠️ Personalização

### Alterar a planilha
No arquivo `sheets_reader.py`, edite:
```python
SPREADSHEET_ID = "seu_id_aqui"
SHEET_GID = "seu_gid_aqui"
```

O ID e GID estão na URL da planilha:
`https://docs.google.com/spreadsheets/d/`**[ID]**`/edit?gid=`**[GID]**

### Mapeamento de colunas
O sistema detecta as colunas automaticamente por nome.
Se alguma coluna não for detectada corretamente, edite a função
`detect_columns()` em `sheets_reader.py` adicionando os nomes das suas colunas.

---

## ❓ Problemas comuns

| Erro | Solução |
|---|---|
| `403 Forbidden` | API Key inválida ou Google Sheets API não ativada |
| `Planilha retornou vazia` | Verifique se o GID da aba está correto |
| `Aba não encontrada` | Confira se o GID corresponde à aba correta |
| Colunas incorretas | Ajuste `detect_columns()` com os nomes exatos das colunas |

---

*Central de Processos e Riscos · Ferreira Supermercados*
