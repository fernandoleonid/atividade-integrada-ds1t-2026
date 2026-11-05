# Projeto Integrado: Sistema de Gestão de Delivery Local

## 1. Contexto do Problema
Uma empresa de delivery precisa de uma ferramenta para gerenciar suas operações (pedidos, produtos e motoboys). Por políticas de segurança e restrições de permissão nas máquinas dos colaboradores, **não é permitido instalar softwares de terceiros ou bancos de dados pesados**.

A solução deve ser uma aplicação leve, desenvolvida internamente, que rode diretamente pelo interpretador Python e utilize apenas recursos nativos (como o banco de dados SQLite). Cada grupo escolherá um **nicho de mercado específico** (ex: Pizzaria, Comida Árabe, Sushi, Hamburgueria), o que definirá a identidade visual, o cardápio e as regras de negócio do sistema.

## 2. O Foco
O objetivo central é a **construção do sistema em Python**. As demais disciplinas atuarão como suporte para viabilizar, documentar, hospedar e distribuir esse produto final.

## 3. Papéis das Disciplinas

- **LOPAL (O Produto):** Desenvolver a lógica do sistema em Python utilizando **SQLite** (biblioteca nativa `sqlite3`, sem instalação extra). O sistema deve ser executado diretamente via terminal ou interface gráfica básica (`tkinter`), sem necessidade de instaladores.
- **LER (O Planejamento):** Levantar e documentar os requisitos funcionais e não funcionais específicos do nicho escolhido e da infraestrutura de suporte, **incluindo os requisitos de ARI (seção 6)**.
- **ARI e SOP (A Infraestrutura):** Montar a topologia de rede local (AP/roteador (wifi), DHCP, IPs), **configurando o DHCP do AP**, e provisionar os contêineres no PC Servidor (DNS para resolução de nomes e Web para hospedar a landing page e o arquivo do código-fonte). Os requisitos de ARI entram na Matriz de Requisitos do LER.
- **LIMA (A Divulgação):** Desenvolver a *Landing Page* (HTML/CSS) com a identidade visual do nicho escolhido, apresentando o projeto e fornecendo o link para download do código-fonte.

## 4. Entregáveis por Disciplina

- **LER:** Documento de Visão, Cronograma detalhado e Matriz de Requisitos, **incluindo os requisitos de ARI (seção 6)** (Formato: PDF).
- **LOPAL:** Link do wireframe e repositório com o código-fonte Python (incluindo o script de criação do banco SQLite).
- **LIMA:** Link do protótipo e repositório com o código-fonte HTML/CSS.
- **SOP / ARI:** Relatório de Infraestrutura contendo registro (fotos e prints) dos procedimentos de configuração de rede e contêineres, com o conteúdo mínimo da seção 6.3 (Formato: PDF).
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
| **19/11 a 20/11** | **Wireframe e Matriz de Requisitos:** Esboço da Landing Page e requisitos do sistema Python **e da infraestrutura (ARI, seção 6)**. | LIMA, LER, LOPAL, ARI |
| **23/11 a 03/12** | **Execução do Projeto:** Configuração de rede/contêineres, desenvolvimento Python/HTML e testes de integração. | ARI, SOP, LOPAL, LIMA |
| **11/12** | **Defesa Técnica:** Demonstração do fluxo completo e apresentação dos artefatos. | Todas |

## 6. Requisitos de Infraestrutura (ARI)

Esta seção é o insumo de ARI para a **Matriz de Requisitos do LER**. Cada requisito tem um critério de aceitação: ele é **atingido** ou **não atingido**, conforme o que a demonstração e o Relatório de Infraestrutura mostram.

### 6.1 Plano de rede do grupo

O grupo define e registra estes dados no Relatório de Infraestrutura:

| Item | Valor do grupo |
| :--- | :--- |
| Nicho e nome da empresa | |
| Domínio (terminado em `.test`) | |
| Prefixo e máscara da rede | |
| IP do AP (gateway) | |
| Faixa de endereços entregue pelo DHCP | |
| IP do PC Servidor | |
| Serviços e portas | DNS: 53 (UDP e TCP) · Web: 80 (TCP) |
| Nomes registrados no DNS | `www.<domínio>` e `<domínio>` |

### 6.2 Requisitos (para a Matriz de Requisitos)

| ID | Requisito | Critério de aceitação | Evidência |
| :--- | :--- | :--- | :--- |
| **RF-ARI-01** | **Distribuição automática de endereços (DHCP):** o AP, configurado pelo grupo, entrega aos clientes IP, máscara, gateway e servidor DNS. | Um cliente ligado ao AP recebe IP sem configuração manual, com o DNS do projeto. | Prints do painel do AP e da configuração de rede recebida pelo cliente. |
| **RF-ARI-02** | **Endereço estável do servidor:** o PC Servidor mantém o mesmo IP durante todo o projeto. | O IP registrado no plano de rede é o mesmo depois de reiniciar o servidor. | Print da configuração no AP e do IP antes e depois. |
| **RF-ARI-03** | **Resolução de nomes:** o servidor DNS, em contêiner, responde o IP do PC Servidor para `www.<domínio>` e `<domínio>`. | No cliente, `nslookup www.<domínio>` devolve o IP do PC Servidor, usando o DNS do grupo. | Print do `nslookup` no cliente. |
| **RF-ARI-04** | **Hospedagem da landing page:** o servidor Web, em contêiner, publica a landing page na porta 80. | A página abre no navegador do cliente pelo nome e pelo IP, com a identidade visual do grupo. | Prints do navegador, com a aba Rede aberta. |
| **RF-ARI-05** | **Distribuição do código-fonte:** o servidor Web oferece para download o arquivo com o código-fonte Python. | O link da landing page baixa o arquivo no cliente, e o arquivo abre e executa. | Prints do link, do download e do arquivo no cliente. |
| **RNF-ARI-01** | **Serviços em contêineres:** DNS e Web rodam cada um em seu contêiner Docker, criados com `docker run` a partir de imagens já carregadas no computador. | `docker ps` mostra os dois contêineres de pé, com as portas 53 e 80 publicadas. | Comandos usados e print do `docker ps`. |
| **RNF-ARI-02** | **Rede isolada e sem administrador:** a solução funciona sem internet e sem exigir privilégio de administrador dos alunos. | A demonstração roda na rede do AP, sem internet. Se algum passo exigir administrador, o grupo registra e avisa o professor. | Relatório. |
| **RNF-ARI-03** | **Domínio local de teste:** o domínio é escolhido pelo grupo (conforme o nicho) e termina em `.test`. | O domínio termina em `.test`; nenhum domínio real (`.com`, `.com.br`) nem `.local`. | Plano de rede. |
| **RNF-ARI-04** | **Documentação:** a infraestrutura é registrada no Relatório de Infraestrutura. | O relatório tem o conteúdo mínimo da seção 6.3, e outra pessoa consegue refazer o que está descrito. | Relatório (PDF). |

### 6.3 Relatório de Infraestrutura: conteúdo mínimo (PDF)

1. Diagrama da topologia: AP, PC Servidor com os dois contêineres e o cliente.
2. Plano de rede preenchido (seção 6.1).
3. Configuração do AP: prints do painel (DHCP, faixa, gateway, DNS e reserva do servidor).
4. Contêineres: comandos `docker run` usados, `docker ps` e o arquivo de configuração do DNS.
5. Testes: `nslookup`, a página aberta pelo nome, o download do código-fonte e a configuração de rede do cliente.
6. Problemas encontrados e como foram resolvidos, com as fontes pesquisadas.

## 7. Critério (Integração)

O grupo deve demonstrar o fluxo completo em tempo real:
1. O Cliente, ligado ao AP e com o IP recebido por DHCP, acessa o domínio local (ex: `http://www.pizzaria.test` ou `http://www.arabe.test`) via navegador.
2. A página carrega corretamente com a identidade visual do grupo (LIMA/SOP/ARI).
3. O código-fonte é baixado a partir da própria página (servido pelo Web em contêiner) e a aplicação Python é executada, conectando-se ao banco SQLite local e operando conforme o escopo definido pelo grupo (LOPAL/LER).
4. Verificações de infraestrutura (ARI), feitas pelo avaliador: `docker ps` com DNS e Web de pé (RNF-ARI-01); `nslookup` do domínio no cliente (RF-ARI-03); configuração recebida por DHCP no cliente (RF-ARI-01); IP do servidor igual ao do plano de rede (RF-ARI-02).
