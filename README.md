# 📝 Projeto: Board para Gerenciamento de Tarefas

Este projeto tem como objetivo criar um **board customizável** para acompanhamento de tarefas, inspirado em ferramentas de gerenciamento como Trello e Jira.  
O sistema permite criar boards, adicionar colunas e cards, mover tarefas entre estágios e manter persistência no **banco de dados MySQL**.

---

## 🚀 Funcionalidades Principais

- Criar, selecionar e excluir boards.
- Configurar colunas personalizadas em cada board.
- Criar, mover, cancelar, bloquear e desbloquear cards.
- Navegação dos cards entre colunas respeitando regras pré-definidas.
- Persistência de dados em **MySQL**.
- Relatórios opcionais sobre tempo de execução e bloqueios.

---

## 📋 Requisitos do Sistema

1. **Menu inicial** deve exibir as opções:
   - Criar novo board
   - Selecionar board
   - Excluir boards
   - Sair

2. **Persistência**: todos os dados dos boards, colunas e cards devem ser armazenados no **MySQL**.

---

## 🧩 Regras dos Boards

1. Um **board** deve ter:
   - Nome único.
   - Pelo menos **3 colunas**:
     - **Inicial** (primeira).
     - **Final** (penúltima).
     - **Cancelamento** (última).
     - Colunas adicionais do tipo **pendente** podem ser criadas livremente.

2. **Colunas**:
   - Possuem nome, ordem e tipo (Inicial, Final, Cancelamento, Pendente).
   - Cada board pode ter **somente uma** coluna de cada tipo especial (Inicial, Final, Cancelamento).
   - A ordem deve respeitar: Inicial → Pendentes → Final → Cancelamento.

3. **Cards**:
   - Atributos: título, descrição, data de criação, status de bloqueio.
   - Devem seguir a ordem das colunas (sem pular etapas).
   - Podem ser enviados diretamente para **Cancelamento** (exceto se já estiverem em Final).
   - Podem ser bloqueados, exigindo justificativa.
   - Para desbloquear, é necessário informar o motivo.

---

## 🛠️ Menu de Manipulação do Board Selecionado

Uma vez dentro de um board, o menu deve permitir:

- Criar novo card.
- Mover card para próxima coluna.
- Cancelar card.
- Bloquear card (com motivo).
- Desbloquear card (com motivo).
- Fechar board.

---

## ⭐ Requisitos Opcionais (Extras)

1. **Histórico de movimentação**:
   - Cada card deve registrar a data/hora de entrada e saída em cada coluna.

2. **Relatório de conclusão**:
   - Informar o tempo total para concluir cada tarefa.
   - Detalhar tempo gasto em cada coluna.

3. **Relatório de bloqueios**:
   - Informar quando, por quanto tempo e por qual motivo o card foi bloqueado/desbloqueado.

---

## 🏗️ Estrutura Recomendada

- `src/main/java` → código-fonte do sistema (menu, entidades, serviços).
- `src/main/resources` → configuração de banco e scripts SQL/Liquibase.
- `database/` → scripts de criação e manutenção do banco.
- `reports/` → geração de relatórios opcionais.

---

## 💾 Banco de Dados

- SGBD: **MySQL**.
- Entidades principais:
  - **Board** (id, nome).
  - **Coluna** (id, nome, tipo, ordem, board_id).
  - **Card** (id, título, descrição, data_criacao, bloqueado, coluna_id).
  - **Histórico** (opcional, para movimentação e bloqueios).

---

## ▶️ Como Executar

1. **Clonar o repositório**:
   ```bash
   git clone https://github.com/seu-usuario/board.git
   cd board
