# Qualidade:

### 1. Introdução

Este documento tem como objetivo apresentar os aspectos de arquitetura e qualidade do sistema Agenda UnB, servindo como um artefato crucial para garantir que o desenvolvimento do software atenda aos requisitos funcionais e não funcionais estabelecidos. A qualidade do software é um fator determinante para o sucesso de qualquer projeto, impactando diretamente a satisfação do usuário, a eficiência operacional e a sustentabilidade a longo prazo.

<!-- Abordaremos a estrutura do sistema através de suas visualizações de componentes e de dados, e discutiremos os atributos de qualidade que guiam o desenvolvimento, tanto do ponto de vista externo (percebido pelo usuário) quanto interno (relacionado à manutenibilidade e escalabilidade do código). A análise contínua desses aspectos garante a entrega de um produto robusto, confiável e fácil de manter para a **Agenda UnB**. -->

### 2. Definição de Qualidade no Projeto

A qualidade do projeto Agenda UnB é entendida como a conformidade do sistema com os requisitos e expectativas dos usuários, além de sua aderência a padrões técnicos e boas práticas de desenvolvimento. Sendo um sistema de gestão de eventos, a qualidade abrange desde a experiência intuitiva do usuário até a robustez da infraestrutura e a facilidade de manutenção e evolução do código.

### 3. Qualidade do Produto

A qualidade do produto pode ser categorizada em qualidades externas e internas.

#### 3.1. Qualidade Externa (Percebida pelo Usuário)

 Atributos de qualidade que são diretamente perceptíveis pelos usuários finais durante a interação com o sistema.

* **Usabilidade:** O sistema deve ser fácil de aprender e de usar, permitindo que participantes, organizadores e administradores realizem suas tarefas (como inscrever-se em eventos, cadastrar novos eventos, visualizar agendas e gerenciar notificações) de forma intuitiva e eficiente. A interface web, desenvolvida com React, deve proporcionar uma experiência fluida tanto em PCs quanto em dispositivos móveis.
* **Confiabilidade:** O sistema deve operar de forma consistente e correta, minimizando falhas e garantindo a integridade dos dados. Isso inclui a disponibilidade do serviço (Backend API e Banco de Dados) e a precisão das informações apresentadas (dados de eventos, usuários, notificações).
* **Desempenho:** O sistema deve responder rapidamente às interações do usuário, garantindo um carregamento ágil das páginas e uma execução eficiente das operações, mesmo com um grande volume de dados ou usuários simultâneos. A comunicação via HTTPS e a otimização do backend (Django com Gunicorn) são cruciais para isso.
* **Segurança:** A confidencialidade, integridade e disponibilidade dos dados devem ser asseguradas. Isso inclui a proteção das informações de usuário (senhas, emails), a segurança das transações (inscrições, cadastros) e a prevenção contra acessos não autorizados. A comunicação HTTPS entre o Frontend e o Backend é um pilar fundamental.

#### 3.2. Qualidade Interna (Relacionada ao Código e Arquitetura)

Atributos de qualidade que não são diretamente percebidos pelos usuários, mas que são muito importantes para os desenvolvedores e para a manutenção do sistema a longo prazo.

* **Manutenibilidade:** O código-fonte deve ser compreensível, modificável e testável. A arquitetura modular (Frontend, Backend, Banco de Dados em MySQL) e a utilização de frameworks como React e Django contribuem para um código mais organizado e fácil de manter.
* **Testabilidade:** O sistema deve ser projetado de forma a permitir a criação e execução de testes automatizados (unitários, de integração, de sistema) de maneira eficiente, garantindo a detecção precoce de bugs e a validação do comportamento esperado das funcionalidades.
* **Flexibilidade/Extensibilidade:** A arquitetura deve permitir que novas funcionalidades sejam adicionadas e que as existentes sejam modificadas com o mínimo impacto possível no restante do sistema. O modelo de dados deve ser flexível o suficiente para acomodar futuras expansões nas entidades de eventos, usuários, etc.
* **Reusabilidade:** Componentes e módulos devem ser projetados de forma a poderem ser reutilizados em diferentes partes do sistema ou em outros projetos, reduzindo o esforço de desenvolvimento e aumentando a consistência.


# Referências

>  [<a id="ref1">1</a>] Bass, L., Clements, P., & Kazman, R. (2012). Software Architecture in Practice. 3rd ed. Addison-Wesley.
>
> [<a id="ref2">2</a>] Rozanski, A., & Woods, E. (2011). Software Systems Architecture: Working With Stakeholders Using Viewpoints and Perspectives. 2nd ed. Addison-Wesley.
>
> [<a id="ref3">3</a>] ISO/IEC 25010. (2011). Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — System and software quality models. International Organization for Standardization.


# Histórico de Versões

| Versão | Data | Descrição | Autor | Revisor | Comentário do Revisor |
| -- | -- | -- | -- | -- | -- |
| `1.0`  | 23/06/2025  | Criação do Documento Inicial e elaboração do conteúdo| [Pedro Lopes](https://github.com/pLopess) e [Alexandre Júnior](https://github.com/AlexandreLJr) |  |  |
