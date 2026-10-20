[README.md - FoodRun (clone de delivery de comida).md](https://github.com/user-attachments/files/33737269/README.md.-.FoodRun.clone.de.delivery.de.comida.md)
# 🛵 FoodRun

> Plataforma de delivery de comida que conecta clientes, restaurantes e entregadores, inspirada no iFood.

![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)
![Licença](https://img.shields.io/badge/licen%C3%A7a-MIT-blue)

---

## 📌 Sobre o Projeto

O **FoodRun** é um aplicativo web (com versão mobile no futuro) que permite ao cliente pesquisar restaurantes da sua região, montar um pedido, pagar pelo app e acompanhar a entrega em tempo real.

Para o restaurante, o sistema oferece um painel para gerenciar cardápio, receber pedidos e controlar o status de preparo. Para o entregador, há uma tela para aceitar corridas e informar as etapas da entrega.

### Objetivos

- Permitir o cadastro e login de clientes, restaurantes e entregadores.
- Listar restaurantes com filtro por categoria, avaliação e tempo de entrega.
- Gerenciar carrinho, pedido e pagamento.
- Acompanhar o status do pedido (recebido → em preparo → saiu para entrega → entregue).
- Gerar um histórico de pedidos e avaliações.

### Público-alvo

- Pessoas que pedem comida pelo celular no dia a dia.
- Pequenos e médios restaurantes que não possuem sistema próprio de vendas online.

---

## 🧰 Tecnologias, Ferramentas e Infraestrutura

### Linguagens e frameworks

| Camada | Tecnologia | Motivo da escolha |
|---|---|---|
| Front-end web | React + TypeScript | Componentes reutilizáveis e tipagem para evitar erros |
| Estilização | Tailwind CSS | Agilidade na criação de telas responsivas |
| Back-end | Node.js + Express (TypeScript) | Mesma linguagem do front-end, fácil de aprender em equipe |
| Tempo real | Socket.IO | Atualização do status do pedido sem recarregar a página |
| Autenticação | JWT + bcrypt | Login seguro e senhas criptografadas |

### Banco de dados

- **PostgreSQL**: dados relacionais (usuários, restaurantes, pedidos, itens).
- **Redis**: cache de restaurantes populares e sessões do carrinho.

### Infraestrutura e nuvem (planejada)

- **Docker** e **Docker Compose**: ambiente de desenvolvimento igual para toda a equipe.
- **Amazon Web Services (AWS)**: hospedagem da API (EC2 ou ECS), banco (RDS) e armazenamento de imagens (S3).
- **GitHub Actions**: pipeline de integração contínua (testes e build a cada push).
- **Mapas**: Google Maps API para cálculo de distância e taxa de entrega.
- **Pagamento (simulado)**: integração com API de sandbox do Mercado Pago.

### Ferramentas de apoio

- **Visual Studio Code**: editor de código.
- **Figma**: protótipo de telas.
- **Postman / Insomnia**: teste das rotas da API.
- **Jira ou Trello**: organização das tarefas (backlog e quadro Kanban).
- **Jest** e **Cypress**: testes unitários e de ponta a ponta.

---

## 🧭 Metodologias

### Metodologia escolhida: Espiral (com práticas ágeis)

Escolhemos o **modelo espiral** porque o FoodRun tem muitos pontos de incerteza: regras de entrega, formas de pagamento e necessidades dos restaurantes ainda serão descobertas durante o projeto.

No modelo espiral, o trabalho é dividido em ciclos. Em cada ciclo fazemos:

1. **Planejamento**: definimos as funcionalidades da rodada.
2. **Análise de riscos**: identificamos o que pode dar errado (ex.: integração de pagamento instável).
3. **Desenvolvimento**: construímos e testamos a funcionalidade.
4. **Avaliação**: mostramos o resultado ao professor/cliente e ajustamos o próximo ciclo.

#### Por que não o modelo cascata?

O modelo cascata exige que todos os requisitos sejam definidos antes de programar. Como este é um projeto de aprendizado e os requisitos vão mudar conforme testamos, o cascata seria rígido demais e poderia gerar retrabalho.

### Ciclos previstos

| Ciclo | Entregas | Duração estimada |
|---|---|---|
| 1 | Cadastro, login e protótipo das telas | 2 semanas |
| 2 | Listagem de restaurantes e cardápio | 2 semanas |
| 3 | Carrinho e fechamento do pedido | 2 semanas |
| 4 | Painel do restaurante e status em tempo real | 2 semanas |
| 5 | Testes, deploy e documentação final | 1 semana |

### Organização do time

- **Reuniões rápidas** (15 min) duas vezes por semana, no estilo *daily*.
- **Quadro Kanban** com colunas: *Backlog → A fazer → Em andamento → Revisão → Concluído*.

---

## 🌿 Uso do Git e GitHub

### Estratégia de branches (Git Flow simplificado)

| Branch | Função |
|---|---|
| `main` | Versão estável, pronta para entrega |
| `develop` | Integração das funcionalidades prontas |
| `feature/nome-da-funcionalidade` | Desenvolvimento de cada tarefa |
| `hotfix/descricao` | Correção urgente em produção |

### Padrão de commits

Usamos o padrão **Conventional Commits**:

```text
feat: adiciona tela de carrinho
fix: corrige cálculo da taxa de entrega
docs: atualiza README com telas do projeto
test: adiciona testes do endpoint de login
```

### Fluxo de trabalho

1. Criar uma branch a partir de `develop`:
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/carrinho
   ```
2. Fazer commits pequenos e frequentes.
3. Enviar a branch e abrir um **Pull Request** para `develop`.
4. Outro membro revisa o código e aprova.
5. Após os testes passarem, o merge é feito em `develop`.
6. Ao final de cada ciclo, `develop` é mesclada em `main` e recebe uma **tag** de versão (ex.: `v0.2.0`).

### Regras da equipe

- Nunca fazer commit direto na `main`.
- Todo Pull Request precisa de pelo menos uma aprovação.
- Não subir senhas, chaves de API ou arquivos `.env` (use o `.gitignore`).

---

## 🎨 Projeto de Interface

As telas foram desenhadas no **Figma** a partir de wireframes feitos à mão. Abaixo estão as principais telas do sistema.

### Mapa de navegação

```text
Login ──► Home (restaurantes) ──► Restaurante (cardápio) ──► Carrinho ──► Checkout ──► Acompanhamento
  │                                                                                        │
  └──► Cadastro                                                            Histórico de pedidos
```

### Telas do cliente

| Tela | Descrição |
|---|---|
| Login / Cadastro | Entrada com e-mail e senha |
| Home | Barra de busca, categorias (pizza, lanches, japonesa...) e lista de restaurantes |
| Restaurante | Informações da loja e itens do cardápio organizados por seção |
| Carrinho | Itens, quantidades, observações e total |
| Checkout | Endereço, forma de pagamento e confirmação |
| Acompanhamento | Linha do tempo do pedido com status em tempo real |

### Exemplo de wireframe: tela Home

```text
+-------------------------------------------+
|  FoodRun              [🛒 2]   [👤]       |
+-------------------------------------------+
|  🔍 Buscar restaurante ou prato...        |
+-------------------------------------------+
|  [Pizza] [Lanches] [Japonesa] [Açaí]      |
+-------------------------------------------+
|  ┌──────────────┐  ┌──────────────┐       |
|  │ [imagem]     │  │ [imagem]     │       |
|  │ Pizzaria X   │  │ Hamburgueria │       |
|  │ ⭐ 4.7 • 35min│  │ ⭐ 4.5 • 25min│       |
|  └──────────────┘  └──────────────┘       |
+-------------------------------------------+
```

### Telas do restaurante

| Tela | Descrição |
|---|---|
| Painel de pedidos | Lista de pedidos novos, em preparo e prontos |
| Gerenciar cardápio | Cadastro, edição e pausa de itens |
| Relatórios | Vendas do dia e produtos mais vendidos |

### Protótipos

Adicione as imagens exportadas do Figma (ou desenhos feitos em Paint, Word ou PowerPoint) na pasta `docs/telas/`:

```markdown
![Tela de login](docs/telas/login.png)
![Tela Home](docs/telas/home.png)
![Tela do carrinho](docs/telas/carrinho.png)
```

---

## 🚀 Como Executar o Projeto

> Esta seção será preenchida conforme o projeto avançar.

```bash
git clone https://github.com/seu-usuario/foodrun.git
cd foodrun
docker compose up --build
```

---

## 👥 Equipe

| Nome | Função |
|---|---|
| Nome do integrante 1 | Front-end e design de telas |
| Nome do integrante 2 | Back-end e banco de dados |
| Nome do integrante 3 | Documentação, testes e Git |

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.
