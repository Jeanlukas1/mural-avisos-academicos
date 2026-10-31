# Mural de Avisos Acadêmicos

Atividade prática extra dos Encontros 1 e 2 da disciplina **Laboratório de Programação Full Stack**.

O projeto é uma API em FastAPI para um front-end já fornecido, que permite publicar e listar avisos acadêmicos. Os avisos ficam em uma lista Python, em memória, e são perdidos quando o servidor é reiniciado.

## Tecnologias

- **Back-end:** Python, FastAPI, Pydantic e Uvicorn
- **Front-end (fornecido):** HTML, CSS e JavaScript com Fetch API

## Estrutura

```text
Frontend_Mural_Avisos/
├── backend/
│   ├── main.py            # aplicação, CORS e rotas
│   ├── models.py          # modelos Pydantic de entrada e saída
│   └── requirements.txt
├── frontend/
│   ├── index.html
│   ├── styles.css
│   └── app.js
└── evidencias/            # capturas de tela da execução
```

## Como executar

São necessários dois terminais, e os comandos abaixo são para o PowerShell no Windows.

**Terminal 1: back-end (porta 8000)**

```powershell
cd Frontend_Mural_Avisos\backend
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn main:app --reload
```

**Terminal 2: front-end (porta 5500)**

```powershell
cd Frontend_Mural_Avisos\frontend
python -m http.server 5500
```

Depois, acesse:

- Aplicação: <http://localhost:5500>
- Swagger: <http://127.0.0.1:8000/docs>

## API

| Operação | Rota | Resposta |
| --- | --- | --- |
| Listar avisos | `GET /api/avisos` | `200` e lista JSON |
| Publicar aviso | `POST /api/avisos` | `201` e o aviso criado |

Exemplo de corpo do `POST`:

```json
{
  "titulo": "Monitoria de programação",
  "mensagem": "A monitoria ocorrerá no laboratório 3 às 18 horas.",
  "autor": "Coordenação",
  "prioridade": "importante"
}
```

A API acrescenta `id` e `publicado_em` à resposta.

### Validação

| Campo | Regra |
| --- | --- |
| `titulo` | 4 a 60 caracteres |
| `mensagem` | 10 a 300 caracteres |
| `autor` | 3 a 50 caracteres |
| `prioridade` | `normal` ou `importante` |

Dados fora dessas regras retornam `422`.

## Evidências

**Interface exibindo um aviso**

![Interface exibindo um aviso](Frontend_Mural_Avisos/evidencias/Captura%20de%20tela%202026-10-31%20175014.png)

**Swagger: rota GET**

![Rota GET no Swagger](Frontend_Mural_Avisos/evidencias/Captura%20de%20tela%202026-10-31%20175200.png)

**Swagger: rota POST**

![Rota POST no Swagger](Frontend_Mural_Avisos/evidencias/Captura%20de%20tela%202026-10-31%20175221.png)

**Network: GET 200 e POST 201**

![Aba Network com GET 200 e POST 201](Frontend_Mural_Avisos/evidencias/Captura%20de%20tela%202026-10-31%20192745.png)

**Resposta 422 provocada pelo Swagger**

![Resposta 422 no Swagger](Frontend_Mural_Avisos/evidencias/Captura%20de%20tela%202026-10-31%20193007.png)
