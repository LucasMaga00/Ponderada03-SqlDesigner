### Ponderada Programação - Semana 03
**Aluno:** Lucas Magalhães Castro Rodrigues

O SQL Desiger que imaginei, possui as seguintes tables:

1. **Users**
2. **Manuals**
3. **Materials**
4. **Favorites**
5. **ToDo**
6. **Teams**
7. **TeamUsers**
8. **Notifications**
9. **AssemblersProgress**

### Tabelas e Relacionamentos

## 1. **Users**
Armazena informações sobre cada usuário, incluindo seu nome, email, senha e etc.
- **Primary key**: `id` - Identifica unicamente cada usuário.
- **Relacionamentos**:
  - **1:N (um para muitos)**: Um usuário/admin pode criar várias notificações (tabela `Notifications`).
  - **1:N (um para muitos)**: Usuários podem estar vinculados a múltiplos manuais por meio de favoritos e listas de tarefas.
  - **N:N (muitos para muitos)**: Usuários podem pertencer a várias equipes através da tabela de junção `TeamUsers`.

## 2. **Manuals**
Contém dados sobre manuais, como título, descrição e data de criação.
- **Primary key**: `id` - Identifica unicamente cada manual.
- **Relacionamentos**:
  - **1:N (um para muitos)**: Cada manual pode ter vários materiais associados a ele (tabela `Materials`).

## 3. **Materials**
Mantém informações sobre os materiais relacionados aos manuais, incluindo o tipo de material e a URL para acesso.
- **Primary key**: `id` - Identifica unicamente cada material. (EX: Pdf, imagem, vídeo...)
- **Foreign key**: `manual_id` - Liga cada material ao seu manual correspondente.
- **Relacionamento**:
  - **N:1 (um para muitos)**: Múltiplos materiais podem estar associados a um único manual.

## 4. **Favorites**
Registra os manuais favoritos de cada usuário.
- **Primary keys**: `user_id`, `manual_id` - Um par que identifica unicamente cada favorito.
- **Foreign keys**:
  - `user_id` - Vincula os favoritos ao usuário correspondente.
  - `manual_id` - Vincula os favoritos ao manual correspondente.
- **Relacionamento**:
  - **N:N (muitos para muitos)**: Implementado pela combinação das chaves, permitindo que um usuário tenha vários manuais favoritos e vice-versa.

## 5. **ToDo**
Mantém uma lista de tarefas ou manuais que cada usuário precisa abordar.
- **Chaves Primárias Compostas**: `user_id`, `manual_id` - Identifica unicamente cada item na lista de tarefas.
- **Relacionamento**:
  - **N:N (muitos para muitos)**: Semelhante aos favoritos, cada usuário pode ter vários manuais em sua lista de tarefas e vice-versa.

## 6. **Teams**
Armazena informações sobre equipes dentro da organização.
- **Primary key**: `id` - Identifica unicamente cada equipe.
- **Relacionamento**:
  - **N:N (muitos para muitos)**: Equipes podem ter muitos usuários associados através da tabela `TeamUsers`.

## 7. **TeamUsers**
Tabela de junção que implementa o relacionamento muitos para muitos entre usuários e equipes.
- **Chaves Primárias Compostas**: `team_id`, `user_id` - Um par que identifica unicamente cada associação de usuário a uma equipe.
- **Relacionamento**:
  - **N:N (muitos para muitos)**: Permite que múltiplos usuários pertençam a múltiplas equipes.

## 8. **Notifications**
Registra notificações enviadas aos usuários.
- **Primary key**: `id` - Identifica unicamente cada notificação.
- **Foreign key**: `user_id` - Vincula cada notificação ao usuário destinatário.
- **Relacionamento**:
  - **1:N (um para muitos)**: Um usuário pode receber várias notificações.

## 9. **AssemblersProgress**
Rastreia o progresso dos usuários (montadores) em relação a manuais específicos.
- **Chaves Primárias Compostas**: `user_id`, `manual_id` - Identifica unicamente o progresso de um usuário em um manual.
- **Relacionamento**:
  - **N:N (muitos para muitos)**: Permite rastrear o progresso de vários usuários em vários manuais.
