# Minha Quadra --- Sistema de Reserva de Quadras Esportivas

**Disciplina:** Projetos de Sistemas\
**Instituição:** Centro Universitário de Ensino Superior do Amazonas ---
CIESA\
**Trabalho individual:** Requisitos e Arquitetura de um Sistema\
**Aluno*: Icaro César Gois Ribeiro\
**Tema:** Sistema fictício de reserva de quadras esportivas\
**Versão:** 1.0

> **Escopo acadêmico:** este documento apresenta o levantamento de
> requisitos e a proposta conceitual de arquitetura do Minha Quadra.
> Conforme a orientação da atividade, não faz parte do escopo
> implementar ou programar o sistema.

------------------------------------------------------------------------

# PARTE 1 --- LEVANTAMENTO DE REQUISITOS

## 1. Descrição do sistema

O Minha Quadra é um sistema web destinado a facilitar a reserva de quadras
esportivas em estabelecimentos que oferecem espaços para práticas como
futsal, basquete e vôlei. Atualmente, a consulta de horários e a
confirmação de reservas podem depender de contatos por telefone ou
mensagens, o que dificulta a visualização das disponibilidades e o
controle dos agendamentos. O sistema centraliza essas operações em uma
plataforma acessível pelo navegador.

Os principais usuários são **clientes**, que criam uma conta, consultam
quadras e horários, realizam reservas, acompanham pagamentos e cancelam
agendamentos conforme as regras; e **administradores**, responsáveis por
cadastrar quadras, configurar preços e horários, acompanhar reservas e
manter os dados do estabelecimento. O Minha Quadra também se comunica com
um **gateway de pagamento** para processar pagamentos e com um **serviço
de e-mail** para enviar confirmações e avisos.

## 2. Requisitos funcionais (RF)

  -----------------------------------------------------------------------
  Código                  Descrição               Prioridade
  ----------------------- ----------------------- -----------------------
  RF01                    O sistema deve permitir Alta
                          que o cliente crie uma  
                          conta informando nome,  
                          e-mail e senha.         

  RF02                    O sistema deve permitir Alta
                          que o cliente entre na  
                          plataforma usando       
                          e-mail e senha.         

  RF03                    O sistema deve permitir Alta
                          que o cliente consulte  
                          as quadras cadastradas, 
                          visualizando            
                          modalidade, preço e     
                          características.        

  RF04                    O sistema deve permitir Alta
                          que o cliente consulte  
                          os horários disponíveis 
                          de uma quadra em uma    
                          data selecionada.       

  RF05                    O sistema deve permitir Alta
                          que o cliente solicite  
                          a reserva de um horário 
                          disponível.             

  RF06                    O sistema deve permitir Alta
                          que o cliente realize o 
                          pagamento de uma        
                          reserva por meio do     
                          gateway de pagamento    
                          integrado.              

  RF07                    O sistema deve permitir Alta
                          que o cliente consulte  
                          suas reservas e seus    
                          respectivos status.     

  RF08                    O sistema deve permitir Média
                          que o cliente solicite  
                          o cancelamento de uma   
                          reserva, respeitando as 
                          regras de negócio.      

  RF09                    O sistema deve permitir Alta
                          que o administrador     
                          cadastre, edite e       
                          desative quadras        
                          esportivas.             

  RF10                    O sistema deve permitir Alta
                          que o administrador     
                          configure os horários   
                          de funcionamento e os   
                          preços das quadras.     

  RF11                    O sistema deve permitir Média
                          que o administrador     
                          consulte e gerencie as  
                          reservas realizadas.    

  RF12                    O sistema deve enviar   Média
                          ao cliente um e-mail de 
                          confirmação após a      
                          aprovação de uma        
                          reserva e do pagamento. 
  -----------------------------------------------------------------------

## 3. Requisitos não funcionais (RNF)

Os requisitos não funcionais definem critérios de qualidade que o
sistema deverá cumprir. Os valores abaixo são metas propostas para o
projeto.

  ------------------------------------------------------------------------
  Código            Categoria         Descrição          Prioridade
                                      mensurável         
  ----------------- ----------------- ------------------ -----------------
  RNF01             Desempenho        Em condições       Alta
                                      normais de uso e   
                                      até 200 usuários   
                                      simultâneos, 95%   
                                      das consultas de   
                                      quadras e horários 
                                      deverão responder  
                                      em até 2 segundos. 

  RNF02             Desempenho        A confirmação de   Alta
                                      uma reserva,       
                                      desconsiderando o  
                                      tempo de resposta  
                                      do gateway         
                                      externo, deverá    
                                      ser processada     
                                      pelo servidor em   
                                      até 3 segundos em  
                                      95% das            
                                      solicitações.      

  RNF03             Segurança         Todo o tráfego     Alta
                                      entre cliente e    
                                      servidor deverá    
                                      utilizar HTTPS com 
                                      TLS 1.2 ou         
                                      superior.          

  RNF04             Segurança         As senhas não      Alta
                                      poderão ser        
                                      armazenadas em     
                                      texto puro;        
                                      deverão ser        
                                      protegidas por     
                                      algoritmo próprio  
                                      para hash de       
                                      senhas, com salt   
                                      individual.        

  RNF05             Disponibilidade   O sistema deverá   Alta
                                      buscar             
                                      disponibilidade    
                                      mensal mínima de   
                                      99,5%,             
                                      desconsideradas    
                                      janelas de         
                                      manutenção         
                                      previamente        
                                      comunicadas.       

  RNF06             Usabilidade e     As principais      Média
                    acessibilidade    funções ---        
                                      cadastro, login,   
                                      consulta e reserva 
                                      --- deverão ser    
                                      utilizáveis em     
                                      telas a partir de  
                                      360 pixels de      
                                      largura, sem       
                                      rolagem horizontal 
                                      na área principal. 

  RNF07             Compatibilidade   A interface deverá Média
                                      funcionar nas duas 
                                      versões estáveis   
                                      mais recentes dos  
                                      navegadores        
                                      Chrome, Firefox,   
                                      Edge e Safari.     

  RNF08             Integridade       O sistema deverá   Alta
                                      impedir a          
                                      confirmação de     
                                      duas reservas para 
                                      a mesma quadra,    
                                      data e faixa de    
                                      horário, inclusive 
                                      quando as          
                                      solicitações       
                                      ocorrerem          
                                      simultaneamente.   
  ------------------------------------------------------------------------

## 4. Regras de negócio (RN)

As regras de negócio representam restrições do funcionamento do
estabelecimento e continuam válidas independentemente da tecnologia
utilizada.

  -----------------------------------------------------------------------
  Código                  Regra de negócio        Prioridade
  ----------------------- ----------------------- -----------------------
  RN01                    Cada reserva            Alta
                          corresponde a uma única 
                          quadra, uma data e uma  
                          faixa de horário        
                          definida pelo           
                          estabelecimento.        

  RN02                    Uma quadra não pode     Alta
                          possuir duas reservas   
                          confirmadas que ocupem  
                          a mesma faixa de        
                          horário.                

  RN03                    A reserva somente será  Alta
                          considerada confirmada  
                          após a aprovação do     
                          pagamento pelo gateway. 

  RN04                    O cliente poderá        Média
                          solicitar o             
                          cancelamento sem        
                          cobrança até 24 horas   
                          antes do início do      
                          horário reservado.      

  RN05                    Reservas realizadas com Média
                          menos de 24 horas de    
                          antecedência não        
                          poderão ser canceladas  
                          pelo cliente pela       
                          plataforma.             

  RN06                    Somente administradores Alta
                          poderão cadastrar       
                          quadras, alterar preços 
                          e configurar horários   
                          de funcionamento.       

  RN07                    O horário de            Média
                          funcionamento e a       
                          duração dos períodos de 
                          reserva serão definidos 
                          pelo administrador do   
                          estabelecimento.        
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# PARTE 2 --- DOCUMENTO DE ARQUITETURA

## 5. Visão arquitetural

O Minha Quadra utilizará uma arquitetura cliente-servidor. O cliente
acessará uma aplicação web responsiva pelo navegador. A aplicação
enviará requisições HTTPS para uma API REST, responsável pelas regras de
negócio e pela comunicação com o banco de dados PostgreSQL e com
serviços externos.

A proposta separa a apresentação, a lógica de negócio e o acesso aos
dados. Essa divisão facilita a manutenção, a organização dos componentes
e a aplicação dos requisitos de segurança e integridade.

**Tecnologias propostas:**

-   **Cliente:** aplicação web responsiva, desenvolvida com React e
    TypeScript.
-   **Servidor/API:** Java com Spring Boot, disponibilizando uma API
    REST.
-   **Banco de dados:** PostgreSQL.
-   **Comunicação:** HTTPS com TLS 1.2 ou superior e dados em JSON.
-   **Pagamento:** integração com gateway externo por HTTPS.
-   **Notificações:** integração com serviço externo de e-mail por
    HTTPS.

## 6. Diagramas C4

### 6.1. Nível 1 --- Diagrama de contexto

O diagrama apresenta o Minha Quadra como uma única unidade, seus usuários e
os sistemas externos com os quais se comunica. Neste nível, não são
apresentados banco de dados nem módulos internos.

``` mermaid
flowchart LR
    Cliente["Cliente<br/>Consulta quadras e realiza reservas"]
    Admin["Administrador<br/>Gerencia quadras, preços e reservas"]
    Sistema["Minha Quadra<br/>Sistema web de reserva de quadras"]
    Pagamento["Gateway de pagamento<br/>Processa pagamentos"]
    Email["Serviço de e-mail<br/>Envia confirmações e avisos"]

    Cliente -->|"HTTPS: consulta, cadastro e reservas"| Sistema
    Admin -->|"HTTPS: gerenciamento"| Sistema
    Sistema -->|"HTTPS: solicita pagamento"| Pagamento
    Pagamento -->|"HTTPS: resultado do pagamento"| Sistema
    Sistema -->|"HTTPS: solicita envio de e-mail"| Email
    Email -->|"HTTPS: status de envio"| Sistema
```

**Legenda:** - Retângulo azul/identificado como usuário: pessoa que
utiliza o sistema. - Minha Quadra: sistema que está sendo projetado. -
Gateway de pagamento e serviço de e-mail: sistemas externos. - Setas:
comunicação entre os participantes; o texto informa o conteúdo e o
protocolo.

### 6.2. Nível 2 --- Diagrama de contêineres

O diagrama mostra as partes executáveis ou armazenadoras do Minha Quadra.
Cada contêiner apresenta sua tecnologia e o protocolo de comunicação.

``` mermaid
flowchart TB
    Cliente["Cliente<br/>Navegador web"]
    Admin["Administrador<br/>Navegador web"]
    Web["Aplicação Web<br/>React + TypeScript"]
    API["Servidor / API REST<br/>Java + Spring Boot"]
    BD[("Banco de dados<br/>PostgreSQL")]
    Gateway["Gateway de pagamento<br/>Sistema externo"]
    Email["Serviço de e-mail<br/>Sistema externo"]

    Cliente -->|"HTTPS / HTML / CSS / JS"| Web
    Admin -->|"HTTPS / HTML / CSS / JS"| Web
    Web -->|"HTTPS / JSON / REST"| API
    API -->|"SQL / conexão PostgreSQL"| BD
    API -->|"HTTPS / JSON"| Gateway
    Gateway -->|"HTTPS / JSON: retorno"| API
    API -->|"HTTPS / API de e-mail"| Email
```

**Legenda:** - Aplicação Web: apresenta as telas e recebe as ações dos
usuários. - Servidor/API: valida solicitações, executa regras de negócio
e coordena integrações. - Banco PostgreSQL: armazena usuários, quadras,
horários, reservas e pagamentos. - Sistemas externos: processam
pagamentos e enviam e-mails. - Setas: indicam o protocolo e o formato ou
finalidade da comunicação.

### 6.3. Nível 3 --- Diagrama de componentes do servidor

O nível 3 detalha o interior do contêiner **Servidor/API REST**. Os
componentes estão organizados em apresentação, negócio e dados.

``` mermaid
flowchart TB
    subgraph API["Contêiner: Servidor / API REST — Java + Spring Boot"]
        direction TB
        subgraph Apresentacao["Camada de apresentação"]
            Controller["Controllers REST<br/>Recebem requisições HTTP"]
            Auth["Autenticação e autorização<br/>Valida identidade e perfil"]
        end

        subgraph Negocio["Camada de negócio"]
            Usuario["Serviço de usuários"]
            Quadra["Serviço de quadras e horários"]
            Reserva["Serviço de reservas"]
            Pagamento["Serviço de pagamentos"]
            Notificacao["Serviço de notificações"]
        end

        subgraph Dados["Camada de acesso a dados"]
            Repository["Repositórios<br/>Acesso ao PostgreSQL"]
        end

        Controller --> Auth
        Auth --> Usuario
        Auth --> Quadra
        Auth --> Reserva
        Auth --> Pagamento
        Reserva --> Quadra
        Reserva --> Pagamento
        Reserva --> Notificacao
        Usuario --> Repository
        Quadra --> Repository
        Reserva --> Repository
        Pagamento --> Repository
    end

    BD[("PostgreSQL")]
    Gateway["Gateway de pagamento"]
    Email["Serviço de e-mail"]

    Repository -->|"SQL"| BD
    Pagamento -->|"HTTPS / JSON"| Gateway
    Notificacao -->|"HTTPS / API"| Email
```

**Legenda:** - **Apresentação:** recebe as requisições e controla o
acesso. - **Negócio:** concentra as operações de usuários, quadras,
reservas, pagamentos e notificações. - **Dados:** realiza consultas e
gravações no PostgreSQL. - **Integrações externas:** o serviço de
pagamentos conversa com o gateway; o serviço de notificações conversa
com o provedor de e-mail.

------------------------------------------------------------------------

## 7. Registros de decisão arquitetural (ADRs)

Os ADRs registram decisões tomadas durante a definição da arquitetura.
Cada registro apresenta o contexto, as alternativas, a decisão e suas
consequências positivas e negativas.

### ADR-001 --- Aplicação web como cliente

**Status:** Aceita

**Requisitos relacionados:** RF01, RF02, RF03, RF04, RF05, RNF06 e
RNF07.

**Contexto:** o Minha Quadra precisa ser acessível para clientes e
administradores em diferentes dispositivos, sem exigir instalação de um
aplicativo.

**Alternativas consideradas:** 1. Aplicativo nativo para Android e iOS.
2. Aplicação web responsiva acessada pelo navegador.

**Decisão:** utilizar uma aplicação web responsiva com React e
TypeScript.

**Consequências positivas:** - O usuário acessa o sistema pelo
navegador. - Uma única aplicação atende computadores, tablets e
celulares. - Atualizações são publicadas centralmente. - Não é
necessário distribuir o sistema por lojas de aplicativos.

**Consequências negativas:** - Algumas funcionalidades específicas dos
dispositivos podem ter limitações em comparação com aplicativos
nativos. - A experiência depende do navegador e da conexão com a
internet.

### ADR-002 --- Banco de dados relacional PostgreSQL

**Status:** Aceita

**Requisitos relacionados:** RF03, RF04, RF05, RF07, RF09, RF10, RN02,
RNF01 e RNF08.

**Contexto:** o sistema armazena dados relacionados, como usuários,
quadras, horários, reservas e pagamentos. É necessário manter a
consistência das informações e impedir reservas conflitantes.

**Alternativas consideradas:** 1. Banco de dados não relacional, como
MongoDB. 2. Banco de dados relacional PostgreSQL.

**Decisão:** utilizar PostgreSQL como banco de dados principal.

**Consequências positivas:** - Suporte a transações e integridade
referencial. - Permite relacionar usuários, quadras, reservas e
pagamentos. - Oferece mecanismos para proteger a consistência dos
dados. - É adequado para consultas estruturadas.

**Consequências negativas:** - Alterações complexas na estrutura podem
exigir migrações de banco. - A equipe precisa planejar tabelas,
relacionamentos e índices.

### ADR-003 --- Autenticação por token

**Status:** Aceita

**Requisitos relacionados:** RF01, RF02, RF09, RF10, RF11, RN06, RNF03 e
RNF04.

**Contexto:** clientes e administradores precisam acessar
funcionalidades diferentes. A API deve identificar o usuário e verificar
suas permissões em cada operação protegida.

**Alternativas consideradas:** 1. Autenticação baseada em sessão
armazenada no servidor. 2. Autenticação baseada em token de acesso, com
validação pelo servidor.

**Decisão:** utilizar autenticação por token de acesso, com validade
limitada, transmitido em conexão HTTPS. O servidor verificará a
identidade e o perfil do usuário antes de permitir operações protegidas.

**Consequências positivas:** - A API pode validar as requisições sem
manter uma sessão tradicional para cada usuário. - O mecanismo é
adequado à comunicação com uma aplicação web por API REST. - Permite
controlar permissões de cliente e administrador.

**Consequências negativas:** - A equipe precisa definir validade,
renovação e revogação dos tokens. - O armazenamento inadequado do token
no cliente pode expor a conta. - A implementação exige cuidados
adicionais contra roubo de credenciais e acessos indevidos.

------------------------------------------------------------------------

## 8. Comunicação cliente-servidor

### 8.1. Fluxo de sequência --- realização de uma reserva

O fluxo abaixo representa um caso de uso completo: o cliente consulta a
disponibilidade, solicita uma reserva, o servidor verifica os dados,
registra a operação, solicita o pagamento e retorna o resultado.

``` mermaid
sequenceDiagram
    actor Cliente
    participant Web as Aplicação Web
    participant API as Servidor/API
    participant BD as PostgreSQL
    participant PG as Gateway de pagamento
    participant Email as Serviço de e-mail

    Cliente->>Web: Seleciona quadra, data e horário
    Web->>API: GET /api/quadras/10/horarios?data=2026-11-20
    API->>BD: Consulta horários e reservas
    BD-->>API: Horários disponíveis
    API-->>Web: 200 OK + horários
    Web-->>Cliente: Exibe horários disponíveis

    Cliente->>Web: Confirma solicitação de reserva
    Web->>API: POST /api/reservas
    API->>BD: Verifica disponibilidade e registra reserva pendente
    BD-->>API: Reserva pendente criada
    API->>PG: Solicita pagamento
    PG-->>API: Pagamento aprovado
    API->>BD: Atualiza reserva para confirmada
    BD-->>API: Atualização concluída
    API->>Email: Solicita e-mail de confirmação
    Email-->>API: Solicitação recebida
    API-->>Web: 201 Created + reserva confirmada
    Web-->>Cliente: Exibe confirmação da reserva
```

**Observação:** o fluxo é uma representação conceitual. Em uma
implementação real, a confirmação do pagamento deve considerar
notificações confiáveis do gateway, e a reserva precisa de controle
transacional para evitar conflitos de horário. Se o pagamento for
recusado ou expirar, a reserva pendente deverá ser tratada conforme uma
política definida pelo estabelecimento.

### 8.2. Requisições HTTP

As requisições abaixo são exemplos de contrato da API. Os dados e
identificadores são fictícios e servem para demonstrar a comunicação.

#### Requisição 1 --- Consultar quadras (GET)

**Requisito relacionado:** RF03.

**Método:** `GET`\
**URL:** `/api/quadras`

**Resposta:** `200 OK`

``` json
{
  "quadras": [
    {
      "id": 10,
      "nome": "Quadra Central",
      "modalidade": "Futsal",
      "precoPorHora": 120.00,
      "ativa": true
    },
    {
      "id": 11,
      "nome": "Quadra Arena",
      "modalidade": "Basquete",
      "precoPorHora": 100.00,
      "ativa": true
    }
  ]
}
```

**Explicação:** o método GET consulta as quadras disponíveis no
catálogo. Não cria nem altera registros.

#### Requisição 2 --- Criar reserva (POST)

**Requisito relacionado:** RF05.

**Método:** `POST`\
**URL:** `/api/reservas`

**Corpo da requisição:**

``` json
{
  "quadraId": 10,
  "data": "2026-11-20",
  "horarioInicio": "18:00",
  "horarioFim": "19:00"
}
```

**Resposta:** `201 Created`

``` json
{
  "id": 501,
  "quadraId": 10,
  "data": "2026-11-20",
  "horarioInicio": "18:00",
  "horarioFim": "19:00",
  "status": "PENDENTE_PAGAMENTO",
  "mensagem": "Reserva criada. Aguardando pagamento."
}
```

**Explicação:** o método POST cria uma solicitação de reserva. A reserva
permanece pendente até que o pagamento seja aprovado, conforme a RN03.

#### Requisição 3 --- Atualizar dados de uma quadra (PUT)

**Requisito relacionado:** RF09.

**Método:** `PUT`\
**URL:** `/api/quadras/10`

**Corpo da requisição:**

``` json
{
  "nome": "Quadra Central Reformada",
  "modalidade": "Futsal",
  "precoPorHora": 130.00,
  "ativa": true
}
```

**Resposta:** `200 OK`

``` json
{
  "id": 10,
  "nome": "Quadra Central Reformada",
  "modalidade": "Futsal",
  "precoPorHora": 130.00,
  "ativa": true,
  "mensagem": "Quadra atualizada com sucesso."
}
```

**Explicação:** o método PUT atualiza os dados da quadra identificada
pelo número 10. A operação deve ser permitida somente a um administrador
autenticado.

#### Requisição 4 --- Cancelar uma reserva (DELETE)

**Requisito relacionado:** RF08.

**Método:** `DELETE`\
**URL:** `/api/reservas/501`

**Resposta:** `200 OK`

``` json
{
  "id": 501,
  "status": "CANCELADA",
  "mensagem": "Reserva cancelada com sucesso."
}
```

**Explicação:** o método DELETE solicita o cancelamento da reserva. O
servidor verifica se o usuário é o responsável pela reserva e se o
cancelamento respeita as regras RN04 e RN05.

#### Exemplo de resposta de erro 4xx

**Situação:** o cliente tenta cancelar uma reserva faltando menos de 24
horas para o início do horário.

**Método:** `DELETE`\
**URL:** `/api/reservas/501`

**Resposta:** `409 Conflict`

``` json
{
  "erro": "CANCELAMENTO_NAO_PERMITIDO",
  "mensagem": "O cancelamento pelo cliente deve ser solicitado com pelo menos 24 horas de antecedência."
}
```

**Explicação:** o status 409 informa que a solicitação entra em conflito
com uma regra do estado atual da reserva. O servidor não deve efetuar o
cancelamento nessa situação.

### 8.3. HTTPS e proteção dos dados

O Minha Quadra deverá utilizar HTTPS em toda comunicação entre navegador,
API e serviços externos. HTTPS utiliza o protocolo TLS para proteger a
comunicação em trânsito.

O TLS oferece três proteções importantes: - **Confidencialidade:**
dificulta que terceiros leiam os dados transmitidos. - **Integridade:**
permite detectar alterações indevidas nos dados durante a transmissão. -
**Autenticação do servidor:** o certificado digital ajuda o navegador a
verificar se está conectado ao servidor esperado.

Os dados que precisam de proteção incluem: - Nome, e-mail e demais dados
cadastrais dos clientes. - Senhas e tokens de autenticação. -
Identificadores e informações das reservas. - Informações de pagamento e
referências retornadas pelo gateway. - Dados de administração, como
alterações de preço e horários.

As senhas deverão ser armazenadas como hashes seguros, nunca em texto
puro. O sistema deverá evitar armazenar dados completos de cartão: o
processamento deverá ser delegado ao gateway de pagamento, mantendo
apenas identificadores e informações necessárias para consultar a
transação. O uso de HTTPS não substitui controle de acesso, validação de
entrada, proteção de credenciais e armazenamento seguro.

------------------------------------------------------------------------

## 9. Tabela de rastreabilidade

A rastreabilidade demonstra como os requisitos de qualidade e as
operações da API estão ligados às decisões e aos elementos da
arquitetura.

### 9.1. RNFs relacionados a decisões arquiteturais

  -----------------------------------------------------------------------
  Requisito não funcional Decisão ou elemento     Justificativa
                          arquitetural            
                          relacionado             
  ----------------------- ----------------------- -----------------------
  RNF01 --- Consultas em  ADR-002 e contêiner     O banco relacional
  até 2 segundos para 95% PostgreSQL do C4 nível  permite estruturar
  das solicitações, com   2.                      consultas e utilizar
  até 200 usuários                                índices para melhorar o
  simultâneos.                                    desempenho.

  RNF02 --- Processamento C4 nível 2 ---          A API centraliza a
  de confirmação em até 3 Servidor/API Java +     validação e o
  segundos,               Spring Boot.            processamento da
  desconsiderando o                               reserva, permitindo
  gateway externo.                                medir o tempo de
                                                  processamento interno.

  RNF03 --- HTTPS com TLS C4 nível 1 e nível 2    A comunicação segura
  1.2 ou superior em todo --- comunicação HTTPS;  protege dados
  o tráfego.              ADR-003.                transmitidos entre
                                                  usuários, API e
                                                  integrações.

  RNF04 --- Senhas        ADR-003 e C4 nível 3    O componente de
  armazenadas com hash e  --- componente de       autenticação controla a
  salt individual.        autenticação.           verificação de
                                                  credenciais sem
                                                  armazenar senhas em
                                                  texto puro.

  RNF05 ---               C4 nível 2 ---          A separação dos
  Disponibilidade mensal  servidor/API e banco de contêineres permite
  mínima de 99,5%.        dados separados.        monitoramento e
                                                  manutenção dos
                                                  componentes de forma
                                                  organizada.

  RNF06 --- Interface     ADR-001 --- aplicação   A escolha de uma
  utilizável em telas a   web responsiva.         aplicação web
  partir de 360 pixels.                           responsiva permite
                                                  adaptar a interface a
                                                  diferentes larguras de
                                                  tela.

  RNF07 ---               ADR-001 --- React +     A aplicação web será
  Compatibilidade com as  TypeScript no           validada nos
  duas versões estáveis   navegador.              navegadores definidos
  mais recentes dos                               como parte dos testes
  navegadores indicados.                          de compatibilidade.

  RNF08 --- Impedir duas  ADR-002 e C4 nível 3    O banco relacional e o
  reservas confirmadas no --- Serviço de reservas controle transacional
  mesmo horário e quadra. e Repositórios.         ajudam a garantir a
                                                  integridade das
                                                  reservas concorrentes.
  -----------------------------------------------------------------------

### 9.2. Requisições HTTP relacionadas a requisitos funcionais

  -----------------------------------------------------------------------
  Requisição HTTP         Requisito funcional     Relação
                          correspondente          
  ----------------------- ----------------------- -----------------------
  GET `/api/quadras`      RF03 --- Consultar      Permite obter a lista
                          quadras.                de quadras cadastradas.

  POST `/api/reservas`    RF05 --- Solicitar      Cria uma solicitação de
                          reserva.                reserva para uma quadra
                                                  e horário.

  PUT `/api/quadras/10`   RF09 --- Gerenciar      Permite ao
                          quadras.                administrador atualizar
                                                  os dados de uma quadra.

  DELETE                  RF08 --- Cancelar       Solicita o cancelamento
  `/api/reservas/501`     reserva.                de uma reserva, sujeito
                                                  às regras de negócio.
  -----------------------------------------------------------------------

**Verificação:** todos os oito requisitos não funcionais possuem relação
com pelo menos uma decisão arquitetural ou elemento C4. As quatro
requisições HTTP possuem um requisito funcional correspondente.

------------------------------------------------------------------------

# 10. Conclusão

O desenvolvimento conceitual do Minha Quadra permitiu identificar as
necessidades dos clientes e administradores de um sistema de reserva de
quadras esportivas. O levantamento classificou os requisitos funcionais,
não funcionais e as regras de negócio, estabelecendo o que o sistema
deverá oferecer e quais condições de qualidade deverá atender.

A proposta arquitetural cliente-servidor foi organizada por meio dos
três níveis do modelo C4, mostrando o contexto do sistema, seus
contêineres e os componentes internos do servidor. Os ADRs registraram
as principais decisões tecnológicas e suas consequências. Por fim, o
fluxo de sequência, os exemplos de requisições HTTP e a tabela de
rastreabilidade demonstraram como a arquitetura atende aos requisitos
definidos.

Conclui-se que a documentação apresenta uma proposta coerente para o
Minha Quadra, mantendo a ligação entre as necessidades do negócio, os
requisitos e as decisões de arquitetura.

------------------------------------------------------------------------


