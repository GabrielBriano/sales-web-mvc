# Sales Management — ASP.NET Core MVC (SalesWebMvc)

Aplicação web de **gestão de vendedores, departamentos e vendas**, construída com **ASP.NET Core MVC (.NET 8)**, **Entity Framework Core** e **MySQL**.

> Projeto desenvolvido a partir do curso de C# / ASP.NET Core MVC do Prof. Nelio Alves (Educandoweb / Udemy).

## Funcionalidades

- **Departamentos** — CRUD completo.
- **Vendedores** — CRUD com nome, e-mail, data de nascimento, salário base e departamento; impede excluir vendedor que já tem vendas.
- **Vendas** — listagem, **busca simples** por período e **busca agrupada por departamento**; cada venda tem status (`Pending`, `Billed`, `Cancelled`).
- **Seed automático** — na primeira execução, se o banco estiver vazio, é populado com departamentos, vendedores e vendas de exemplo.

## Tecnologias

- C# / .NET 8 / ASP.NET Core MVC (Razor)
- Entity Framework Core 8 + migrations
- MySQL 8 (provider Pomelo)
- Bootstrap e jQuery Validation

## Arquitetura

```
SalesWebMvc/
├── Controllers/   # recebem as requisições e devolvem as views
├── Services/      # regras de acesso a dados (SellerService, DepartmentService, SalesRecordService)
│   └── Exceptions/  # NotFound, Integrity, DbConcurrency
├── Models/        # entidades (Seller, Department, SalesRecord), enums e ViewModels
├── Data/          # DbContext e SeedingService
├── Migrations/    # histórico do esquema do banco
└── Views/         # telas Razor
```

## Como executar

Pré-requisitos: [.NET 8 SDK](https://dotnet.microsoft.com/download), MySQL 8 em execução e a ferramenta do EF:

```bash
dotnet tool install --global dotnet-ef
```

```bash
cd SalesWebMvc

# 1. guardar a connection string fora do repositório (user-secrets)
dotnet user-secrets init
dotnet user-secrets set "ConnectionStrings:SalesWebMvcContext" "server=localhost;userid=SEU_USUARIO;password=SUA_SENHA;database=saleswebmvcappdb"

# 2. criar o banco / aplicar as migrations
dotnet ef database update

# 3. rodar
dotnet run
```

Alternativa aos user-secrets: definir a variável de ambiente `ConnectionStrings__SalesWebMvcContext`.

O `appsettings.json` contém apenas valores de exemplo (`SEU_USUARIO` / `SUA_SENHA`); **nunca** coloque credenciais reais nele.

## Próximos passos

- Autenticação e autorização.
- Reativar a validação de servidor no cadastro de vendedores (trecho comentado em `SellersController.Create`).
- Testes automatizados dos serviços.
- `docker-compose` com MySQL para subir tudo com um comando.
- Paginação nas listagens.
