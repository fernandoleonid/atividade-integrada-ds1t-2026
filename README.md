
# Projeto Integrado: Sistema de Gestão de Delivery Local

## 1. Contexto do Problema
Uma empresa de delivery precisa de uma ferramenta para gerenciar suas operações (pedidos, produtos e motoboys). Por políticas de segurança e restrições de permissão nas máquinas dos colaboradores, **não é permitido instalar softwares de terceiros ou bancos de dados pesados**.

A solução deve ser uma aplicação leve, desenvolvida internamente, que rode diretamente pelo interpretador Python e utilize apenas recursos nativos (como o banco de dados SQLite). Cada grupo escolherá um **nicho de mercado específico** (ex: Pizzaria, Comida Árabe, Sushi, Hamburgueria), o que definirá a identidade visual, o cardápio e as regras de negócio do sistema.

## 2. O Foco
O objetivo central é a **construção do sistema em Python**. As demais disciplinas atuarão como suporte para viabilizar, documentar, hospedar e distribuir esse produto final.

## 3. Papéis das Disciplinas

- **LOPAL (O Produto):** Desenvolver a lógica do sistema em Python utilizando **SQLite** (biblioteca nativa `sqlite3`, sem instalação extra). O sistema deve ser executado diretamente via terminal ou interface gráfica básica (`tkinter`), sem necessidade de instaladores.
- **LER (O Planejamento):** Levantar e documentar os requisitos funcionais e não funcionais específicos do nicho escolhido e da infraestrutura de suporte.
- **ARI e SOP (A Infraestrutura):** Montar a topologia de rede local (AP/roteador (wifi), DHCP, IPs), **configurando o DHCP do AP**, e provisionar os serviços no PC Servidor (a máquina hospedeira): **um contêiner para cada serviço, todos na mesma máquina**, sendo um contêiner de DNS para resolução de nomes e um de Web para hospedar a landing page e o arquivo do código-fonte. Os requisitos da infraestrutura são levantados pelo grupo e entram na Matriz de Requisitos do LER.
- **LIMA (A Divulgação):** Desenvolver a *Landing Page* (HTML/CSS) com a identidade visual do nicho escolhido, apresentando o projeto e fornecendo o link para download do código-fonte.

### Topologia de referência

<img width="2560" height="1400" alt="topologia-ari" src="https://github.com/user-attachments/assets/d178f502-5fe0-4e08-b643-3abba9da59aa" />


### Pontos de atenção para a infraestrutura (ARI)

Estas perguntas orientam o levantamento de requisitos de infraestrutura. As respostas e a forma de comprovar cada uma entram na Matriz de Requisitos e no Relatório de Infraestrutura, e a pesquisa faz parte do desafio.

- **Endereços:** como os clientes recebem IP? Se o IP do PC Servidor mudar, o que acontece com o domínio, e como evitar isso?
- **Nomes:** quem traduz o domínio em IP? O endereço registrado deve ser o do contêiner ou o do computador que o hospeda, e por quê? Como cada cliente descobre qual é o servidor de nomes?
- **Portas:** com DNS e Web no mesmo computador, como os clientes distinguem um serviço do outro? Quais protocolos e portas cada um usa?
- **Domínio:** que terminação é segura para um teste local, sem conflito com domínios reais?
- **Ambiente:** a rede não tem internet e os computadores não dão acesso de administrador. O que isso muda na escolha das imagens e na configuração? Se algum passo exigir administrador, registrem e avisem o professor.
- **Prova:** como mostrar, a partir de um cliente, que cada parte funciona (e não só que o servidor está de pé)?

## 4. Entregáveis por Disciplina

- **LER:** Documento de Visão, Cronograma detalhado e Matriz de Requisitos, **incluindo os requisitos da infraestrutura (ARI)** (Formato: PDF).
- **LOPAL:** Link do wireframe e repositório com o código-fonte Python (incluindo o script de criação do banco SQLite).
- **LIMA:** Link do protótipo e repositório com o código-fonte HTML/CSS.
- **SOP / ARI:** Relatório de Infraestrutura contendo registro (fotos e prints) dos procedimentos de configuração de rede e contêineres (Formato: PDF).
- **Vídeo Pitch:** Um único vídeo editado e formatado, demonstrando o projeto em funcionamento. **Regra:** máximo de 1 minuto de fala por integrante.
- **Repositório Central (GitHub/GitLab):** Deve conter um `README.md` estruturado com:
  1. Nome e link (perfil) de todos os integrantes.
  2. Breve resumo da principal contribuição técnica de cada membro.
  3. Links diretos e organizados para todos os artefatos (PDFs, códigos, protótipos e vídeo).

## 5. Cronograma

| Período | Entrega / Marco | Disciplinas |
| :--- | :--- | :--- |
| **16/11** | **Ideia do Sistema:** Definição do nicho de mercado e escopo escolhido pelo grupo. | LOPAL, LER |
| **16/11 a 19/11** | **Documento de Visão e Cronograma:** Detalhamento do objetivo, público e planejamento. | LER |
| **19/11 a 20/11** | **Wireframe e Matriz de Requisitos:** Esboço da Landing Page e requisitos do sistema Python **e da infraestrutura (ARI)**. | LIMA, LER, LOPAL, ARI |
| **23/11 a 03/12** | **Execução do Projeto:** Configuração de rede/contêineres, desenvolvimento Python/HTML e testes de integração. | ARI, SOP, LOPAL, LIMA |
| **11/12** | **Defesa Técnica:** Demonstração do fluxo completo e apresentação dos artefatos. | Todas |

## 6. Critério (Integração)

O grupo deve demonstrar o fluxo completo em tempo real:
1. O Cliente, ligado ao AP e com o IP recebido por DHCP, acessa o domínio local (ex: `http://www.pizzaria.test` ou `http://www.arabe.test`) via navegador.
2. A página carrega corretamente com a identidade visual do grupo (LIMA/SOP/ARI).
3. O código-fonte é baixado a partir da própria página (servido pelo Web em contêiner) e a aplicação Python é executada, conectando-se ao banco SQLite local e operando conforme o escopo definido pelo grupo (LOPAL/LER).
