UsuarioController, TokenGenerator, ProdutoController e RestauranteController. Esses controllers lidam com operações CRUD para produtos e restaurantes, permitindo a manipulação de dados como nome, descrição, imagens, e mais. As classes de mapeamento (ProdutoMap e RestauranteMap) definem as configurações do banco de dados, enquanto as interfaces repositório abstraem as operações de dados
#### UsuarioController

- **BuscarTodosUsuarios**: Retorna uma lista de todos os usuarios.
- **BuscarPorId**: Retorna os detalhes de um usuario específico pelo `email`.
- **Cadastrar**: Adiciona um novo usuario.
- **Atualizar**: Atualiza as informações de um usuario existente.
- **Apagar**: Remove um usuario do sistema pelo `email`.

#### TokenGenerator
  - `GenerateToken(string username, string secretKey)
  - `Gera um token JWT com base no nome de usuário fornecido e na chave secreta especificada.

#### ProdutoController

- **ObterImagemRestaurante**: Retorna a imagem de um produto em formato Base64, utilizando o `idproduto`.
- **BuscarTodosProdutos**: Retorna uma lista de todos os produtos.
- **BuscarPorIdProduto**: Retorna os detalhes de um produto específico pelo `idproduto`.
- **Cadastrar**: Adiciona um novo produto, permitindo o upload de uma imagem.
- **Atualizar**: Atualiza as informações de um produto existente, incluindo a imagem.
- **Apagar**: Remove um produto do sistema pelo `idproduto`.

#### RestauranteController

- **BuscarTodosRestaurantes**: Retorna uma lista de todos os restaurantes.
- **BuscarPorCNPJ**: Retorna os detalhes de um restaurante específico pelo CNPJ.
- **ObterImagemRestaurante**: Retorna a imagem de um restaurante em formato Base64.
- **Login**: Autentica um restaurante pelo CNPJ e senha, gerando um token.
- **Cadastrar**: Adiciona um novo restaurante, permitindo o upload de uma imagem.
- **Atualizar**: Atualiza as informações de um restaurante existente, incluindo a imagem.
- **Apagar**: Remove um restaurante do sistema pelo CNPJ.

### Data/Map

### SistemaTarefasDBContex
- Propósito
  - `Representa o contexto do banco de dados para o sistema de tarefas, permitindo o acesso e manipulação das entidades definidas.

- Propriedades Principais
  - `Produto: DbSet que permite o acesso e manipulação dos produtos no banco de dados.

  - `Restaurante: DbSet que permite o acesso e manipulação dos restaurantes no banco de dados.

  - `Usuarios: DbSet que permite o acesso e manipulação dos usuários no banco de dados.

- Métodos Principais
  - `OnModelCreating(ModelBuilder modelBuilder)

  - `Sobrescreve o comportamento padrão do Entity Framework Core para configurar o modelo de dados. Aplica os mapeamentos definidos para ProdutoModel, RestauranteModel, e UsuarioModel usando as respectivas classes de mapeamento (ProdutoMap, RestauranteMap, UsuarioMap).

- Funcionalidades Adicionais
  - `Utiliza o Entity Framework Core (Microsoft.EntityFrameworkCore) para gerenciar as interações com o banco de dados.
  - `Importa mapeamentos de entidades (SistemaDeTarefas.Data.Map) para configurar o modelo de banco de dados de forma específica.

#### UsuarioMap

- Configuração do modelo `UsuarioModel` no banco de dados.
- Define as propriedades como chave primária obrigatórias.


#### ProdutoMap

- Configuração do modelo `ProdutoModel` no banco de dados.
- Define as propriedades como chave primária, obrigatórias e o tipo de dado para a imagem.

#### RestauranteMap

- Configuração do modelo `RestauranteModel` no banco de dados.
- Define as propriedades como chave primária, obrigatórias e o tipo de dado para a imagem.

### Models

#### ResponseLoginModel

- Propriedades do Login, incluindo `Response`, e `Key`.

#### UsuarioModel

- Propriedades do usuario, incluindo `Id`, `Nome`, `Telefone`, `Email`, `Restricao`, `CEP`, `SENHA`, `Tipo`, `GoogleLogin`.

#### ProdutoModel

- Propriedades do produto, incluindo `Id`, `IdProduto`, `Nome`, `Descricao`, `Valor`, `Restricao`, e `Foto`.

#### RestauranteModel

- Propriedades do restaurante, incluindo `Id`, `Nome`, `Cnpj`, `Intolerancia`, `Senha`, `Telefone`, `Cep`, `Email`, `Culinaria`, e `Imagem`.

#### Interfaces

#### IUsuarioRepositorio

- Interface para operações CRUD dos usuarios.
  - `BuscarTodosUsuarios`
  - `BuscarPorId`
  - `Adicionar`
  - `Atualizar`
  - `Apagar

#### IProdutoRepositorio

- Interface para operações CRUD dos produtos.
  - `BuscarTodosProdutos`
  - `BuscarPorIdProduto`
  - `Adicionar`
  - `Atualizar`
  - `Apagar`

#### IRestauranteRepositorio

- Interface para operações CRUD dos restaurantes.
  - `BuscarTodosRestaurantes`
  - `BuscarPorCNPJ`
  - `Adicionar`
  - `Atualizar`
  - `Apagar`

### Repositórios

#### ProdutoRepositorio

- Propósito
  - `Gerencia operações de acesso ao banco de dados para a entidade ProdutoModel no contexto do sistema de tarefas.

- Métodos Principais
  - `BuscarPorIdProduto(string idproduto): Retorna um produto específico com base no ID fornecido.

  - `BuscarTodosProdutos(): Retorna todos os produtos armazenados no banco de dados.

  - `Adicionar(ProdutoModel produto): Adiciona um novo produto ao banco de dados.

  - `Atualizar(ProdutoModel produto, string idproduto): Atualiza informações de um produto existente com base no ID fornecido.

  - `Apagar(string idproduto): Remove um produto do banco de dados com base no ID fornecido.

- Funcionalidades Adicionais
  - `Utiliza o Entity Framework Core para operações de banco de dados.
  - `Implementa operações assíncronas para melhor performance e escalabilidade.
  - `Lida com exceções caso o produto não seja encontrado durante operações de atualização ou exclusão.

#### RestauranteRepositorio

- Propósito
  - `Gerencia operações de acesso ao banco de dados para a entidade RestauranteModel no contexto do sistema de tarefas.

- Métodos Principais
  - `BuscarPorCNPJ(string cnpj): Retorna um restaurante específico com base no CNPJ fornecido.

  - `BuscarTodosRestaurantes(): Retorna todos os restaurantes armazenados no banco de dados.

  - `Adicionar(RestauranteModel rest): Adiciona um novo restaurante ao banco de dados.

  - `Atualizar(RestauranteModel rest, string cnpj): Atualiza informações de um restaurante existente com base no CNPJ fornecido.

  - `Apagar(string cnpj): Remove um restaurante do banco de dados com base no CNPJ fornecido.

- Funcionalidades Adicionais
  - `Utiliza o Entity Framework Core para operações de banco de dados.
  - `Implementa operações assíncronas para melhor performance e escalabilidade.
  - `Lida com exceções caso o restaurante não seja encontrado durante operações de atualização ou exclusão.

#### UsuarioRepositorio

- Propósito
  - `Gerencia operações de acesso ao banco de dados para a entidade UsuarioModel no contexto do sistema de tarefas.

- Métodos Principais
  - `BuscarPorId(string email): Retorna um usuário específico com base no email fornecido.

  - `BuscarTodosUsuarios(): Retorna todos os usuários armazenados no banco de dados.

  - `Adicionar(UsuarioModel usuario): Adiciona um novo usuário ao banco de dados.

  - `Atualizar(UsuarioModel usuario, string email): Atualiza informações de um usuário existente com base no email fornecido.

  - `Apagar(string email): Remove um usuário do banco de dados com base no email fornecido.

- Funcionalidades Adicionais
  - `Utiliza o Entity Framework Core para operações de banco de dados.
  - `Implementa operações assíncronas para melhor performance e escalabilidade.
  - `Lida com exceções caso o usuário não seja encontrado durante operações de atualização ou exclusão.

#### Migration

#### SistemaTarefasDBContexModelSnapshot
- Propósito
  - `Representa um snapshot do modelo de banco de dados gerado automaticamente para o contexto SistemaTarefasDBContex, definindo as configurações das entidades ProdutoModel, RestauranteModel e UsuarioModel.

- Funcionalidades Principais
  - `Configurações para a entidade ProdutoModel:

  - `Define propriedades como Id, Descricao, Foto, IdProduto, Nome, Restricao e Valor.
  - `Especifica tipos de dados, tamanhos máximos e configurações de coluna para cada propriedade.
  - `Configura a chave primária para a entidade como Id.
  - `Define o nome da tabela como Produto.
- Configurações para a entidade RestauranteModel:

  - `Define propriedades como Id, Cep, Cnpj, Culinaria, Email, Imagem, Intolerancia, Nome, Senha e Telefone.
  - `Especifica tipos de dados, tamanhos máximos e configurações de coluna para cada propriedade.
  - `Configura a chave primária para a entidade como Id.
  - `Define o nome da tabela como Restaurante.
- Configurações para a entidade UsuarioModel:

  - `Define propriedades como ID_Cliente, CEP, Email, GoogleLogin, Nome, Restricao, SENHA, Telefone e Tipo.
  - `Especifica tipos de dados, tamanhos máximos e configurações de coluna para cada propriedade.
  - `Configura a chave primária para a entidade como ID_Cliente.
  - `Define o nome da tabela como Usuarios.
- Observações
  - `Utiliza o Entity Framework Core para definir o modelo de banco de dados.
  - `Aplica as configurações necessárias para cada entidade através do ModelBuilder.
  - `Esta classe é auto-gerada pelo EF Core para representar o modelo atual do banco de dados no momento da criação do snapshot.