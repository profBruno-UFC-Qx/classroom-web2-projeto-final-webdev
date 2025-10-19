[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/iVa2Dd1Z)
[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=21156497)

# :checkered_flag: LivroSolidário

Uma plataforma de doação de livros que conecta quem tem livros parados em casa a quem quer ler, mas não pode comprar.

## :technologist: Membros da equipe

*   Matrícula: 558377
*   Nome: Tiago Tito Sampaio
*   Curso: Engenharia de Software

## :bulb: Objetivo Geral

O objetivo geral do projeto LivroSolidário é criar uma ponte digital entre doadores e solicitantes de livros, democratizando o acesso à leitura e promovendo a educação, a cultura e a sustentabilidade. A plataforma visa facilitar a troca de livros de forma eficiente e segura, garantindo que exemplares que não estão sendo utilizados encontrem novos leitores.

## :eyes: Público-Alvo

O público-alvo do LivroSolidário é dividido em:

*   **Doador:** Indivíduos que possuem livros e desejam doá-los para pessoas que farão bom uso deles, contribuindo para o acesso à cultura.
*   **Solicitante:** Pessoas que desejam ler, mas possuem dificuldades financeiras para adquirir livros novos, incluindo estudantes, leitores de baixa renda, e membros de comunidades carentes.

## :star2: Impacto Esperado

Espera-se que o LivroSolidário gere os seguintes impactos:

*   **Social:** Redução da desigualdade no acesso à leitura, fomento à educação e à cultura, e fortalecimento de comunidades através da partilha de conhecimento.
*   **Educacional:** Disponibilização de material didático e literário para estudantes e indivíduos em busca de aprimoramento, complementando recursos educacionais existentes.
*   **Ambiental:** Contribuição para a sustentabilidade ao estender a vida útil dos livros, diminuindo o descarte e o consumo de novos exemplares.
*   **Econômico:** Oferecer uma alternativa gratuita para o acesso a livros, aliviando o orçamento de famílias e estudantes.

## :people_holding_hands: Papéis ou tipos de usuário da aplicação

A aplicação LivroSolidário contará com três papéis de usuário distintos, cada um com permissões e funcionalidades específicas:

1.  **Visitante (Não Logado):**
    *   Acessa a página inicial e a página "Sobre".
    *   Visualiza o catálogo completo de livros disponíveis para doação.
    *   Pode pesquisar e filtrar livros por título, autor, categoria, etc.
    *   Não pode solicitar livros.
    *   Não pode cadastrar, editar ou remover livros.
    *   Não tem acesso a nenhuma área restrita.

2.  **Solicitante (Logado):**
    *   Visualiza a lista de livros disponíveis para doação.
    *   Pode solicitar um livro de seu interesse.
    *   Acompanha o status de suas solicitações.
    *   Não pode cadastrar, editar ou remover livros.
    *   Não pode aceitar ou recusar solicitações de doação.

3.  **Doador (Logado):**
    *   Cadastra, edita e remove seus próprios livros disponíveis para doação.
    *   Visualiza as solicitações feitas para seus livros.
    *   Pode aceitar ou recusar solicitações de doação de seus livros.
    *   Pode visualizar a lista de livros disponíveis, mas não pode solicitar (pois seu foco é doar).

## :triangular_flag_on_post: Principais funcionalidades da aplicação

### Funcionalidades acessíveis a todos (incluindo Visitantes - área pública):

*   **Página Inicial (`/`):** Apresenta a missão do projeto e informações sobre como funciona.
*   **Página "Sobre" (`/sobre`):** Detalha os princípios do LivroSolidário, benefícios e processo de doação/solicitação.
*   **Catálogo de Livros (`/livros`):** Visualiza e pesquisa por todos os livros disponíveis, com filtros por categoria, autor, condição, etc.

### Funcionalidades restritas a usuários logados (autenticados via JWT):

**Para Solicitantes:**

*   **Listagem de Livros Disponíveis (`/livros`):** Catálogo interativo, com a opção de clicar em "Solicitar".
*   **Solicitar Livro:** Botão em cada card de livro para iniciar o processo de solicitação.
*   **Minhas Solicitações (`/minhas-solicitacoes`):** Acompanha o status de todas as solicitações feitas, desde "pendente" até "aceita".

**Para Doadores:**

*   **Meus Livros (`/meus-livros`):** Área para gerenciar os livros que o doador cadastrou, incluindo:
    *   **Cadastrar Novo Livro:** Formulário para adicionar um livro com título, autor, descrição, imagem, categoria, condição, etc.
    *   **Editar Livro:** Modificar informações de um livro existente.
    *   **Remover Livro:** Excluir um livro da lista de doação.
*   **Solicitações para Meus Livros (`/solicitacoes`):** Visualiza as solicitações recebidas para seus livros, com opções para:
    *   **Aceitar Solicitação:** Aprova o pedido, alterando o status e notificando o solicitante.
    *   **Recusar Solicitação:** Nega o pedido, alterando o status e notificando o solicitante.

## :spiral_calendar: Entidades ou tabelas do sistema

### 1. `User`
*   `id` (PK, UUID)
*   `name` (String, Not Null)
*   `email` (String, Not Null, Unique)
*   `password` (String, Not Null, Hashed)
*   `role` (Enum: `'solicitante' | 'doador'`, Not Null, Default: `'solicitante'`)

### 2. `Book`
*   `id` (PK, UUID)
*   `title` (String, Not Null)
*   `isbn` (String, Nullable, Unique)
*   `description` (Text, Nullable)
*   `imageUrl` (String, Nullable)
*   `category` (String, Not Null)
*   `condition` (Enum: `'novo' | 'usado' | 'muito_bom' | 'bom'`, Not Null)
*   `isAvailable` (Boolean, Not Null, Default: `true`)
*   `userId` (FK, UUID, Not Null, References `User.id`) - **Doador do livro**

### 3. `DonationRequest`
*   `id` (PK, UUID)
*   `status` (Enum: `'pendente' | 'aceita' | 'recusada'`, Not Null, Default: `'pendente'`)
*   `bookId` (FK, UUID, Not Null, References `Book.id`)
*   `requesterId` (FK, UUID, Not Null, References `User.id`) - **Solicitante do livro**
*   `donorId` (FK, UUID, Nullable, References `User.id`) - **Preenchido quando a solicitação é aceita**