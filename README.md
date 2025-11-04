# 🚀 WebApiAzureTable

Projeto de exemplo em ASP.NET Core que demonstra o uso do Azure Table Storage para persistência de contatos.

## 🎯 Objetivo

Este projeto implementa uma Web API simples para gerenciar contatos (`Contato`) utilizando o SDK `Azure.Data.Tables`. Serve como referência para aprender como integrar aplicações .NET com Azure Table Storage (Storage Account / Tables).

## 🏗️ Estrutura do projeto

- `Controllers/ContatoController.cs` — Endpoints REST para CRUD de contatos.
- `Models/Contato.cs` — Modelo que implementa `ITableEntity` para uso com Azure Tables.
- `Program.cs` — Configuração mínima do ASP.NET Core (Controllers, Swagger).
- `appsettings.json` / `appsettings.Development.json` — Configurações (conexões, logging).

## 🧰 Tecnologias

- .NET 9 (SDK)
- C#
- Azure.Data.Tables (SDK do Azure para Table Storage)
- Swagger (OpenAPI) para exploração dos endpoints em desenvolvimento

## ✅ Requisitos

- .NET 9 SDK instalado
- Conta Azure com Storage Account (ou Azurite para desenvolvimento local)

## ☁️ Como criar a instância necessária no Azure

- Acesse o recurso Storage Account -> "Chaves de acesso" -> copie a connection string.
- Em "Tables" (ou usando Storage Explorer) crie a tabela `Contatos`.

## ⚙️ Configuração necessária

O projeto lê duas chaves em `ConnectionStrings` no `appsettings.json`:

- `SAConnectionString` — connection string da Storage Account.
- `AzureTableName` — nome da tabela a ser usada (ex.: `Contatos`).

Exemplo mínimo em `appsettings.json`:

```json
{
  "ConnectionStrings": {
    "SAConnectionString": "<CONNECTION_STRING_AQUI>",
    "AzureTableName": "Contatos"
  }
}
```

IMPORTANTE: nunca comite connection strings ou chaves de acesso em repositórios públicos. Use secrets/local user secrets ou variáveis de ambiente em pipelines.

## 🔌 Endpoints disponíveis

Base URL: `https://localhost:{port}/api/Contato`

- POST `/api/Contato` — Criar contato (body: `Contato`)
- PUT `/api/Contato/{id}` — Atualizar contato (id = RowKey)
- GET `/api/Contato/Listar` — Listar todos os contatos
- GET `/api/Contato/ObterPorNome/{nome}` — Filtrar por nome
- DELETE `/api/Contato/{id}` — Deletar contato (id = RowKey)

O modelo `Contato` (em `Models/Contato.cs`) contém as propriedades: `Nome`, `Telefone`, `Email`, `PartitionKey`, `RowKey`, `Timestamp`, `ETag`.

Observação: no controller atual, `RowKey` e `PartitionKey` são definidos com um GUID ao criar o contato (cada contato fica em sua própria partição).

## ▶️ Como executar localmente

1) Restaure dependências e rode a aplicação:

```powershell
git clone https://github.com/erasmobezerra/WebApiAzureTable.git
cd .\WebApiAzureTable
dotnet restore
dotnet run
```

2) Em ambiente de desenvolvimento o Swagger estará disponível em `/swagger`.

3) Configure `appsettings.json` com a `SAConnectionString` e `AzureTableName` antes de executar, ou use variáveis de ambiente / user secrets.

## 🤝 Como contribuir

1. Crie uma branch com nome descritivo: `feature/minha-mudanca`.  
2. Faça commits pequenos e claros.  
3. Abra Pull Request descrevendo o que foi alterado e por quê.  

----

🙏 Agradeço profundamente à **Digital Innovation One** por proporcionar este aprendizado gratuito e de qualidade. Um reconhecimento especial ao professor **[Leonardo Buta](https://www.linkedin.com/in/leonardo-buta/)** pela excelente didática e orientação durante todo o processo.

<div align="center">
  <p>⭐ Se este projeto foi útil para você, considere dar uma estrela!</p>
</div>
