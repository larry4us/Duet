# Duet

![](assets/CapaDuet.png)

O **Duet** é um aplicativo para iOS criado para ajudar casais — especialmente millenials que estão começando a morar juntos — a lidar com tensões e desequilíbrios na divisão das tarefas domésticas.  
O app torna a rotina compartilhada mais leve, justa e colaborativa.

---

## Propósito do Projeto

O objetivo do Duet é simplificar a comunicação do dia a dia e promover equilíbrio na relação, oferecendo ferramentas práticas para organização, negociação e cuidado mútuo.

---

## O que o Duet faz

- **Distribuição rápida de tarefas:** organização intuitiva das atividades da casa, com alertas quando alguém está sobrecarregado.  
- **Renegociação de responsabilidades:** permite revisar acordos e equilibrar a rotina conforme a necessidade do casal.  
- **Reforça o romance do casal:** lembra datas importantes e recompensa quem contribui mais com cupons simbólicos (ex: massagem, jantar, surpresa).

<p align="center">
  <img src="assets/Screens/Dashboard.png" width="220"/>
  <img src="assets/Screens/Tasks.png" width="220"/>
    <img src="assets/Screens/Deals.png" width="220"/>
</p>

---

## Arquitetura

O Duet utiliza uma arquitetura modular baseada em **MVVM-C**, organizada por **Domínios**.

Cada domínio agrupa tudo o que é relacionado a uma funcionalidade específica do app — incluindo Model, ViewModel, Views e Components.

A estrutura geral segue o seguinte formato:

```
RelaxShip/
├── BaseApp/ # Configurações gerais do app
├── Coordinator/ # Navegação com Coordinator Pattern
├── Docs/ # Documentação técnica
├── Domains/ # Módulos separados por contexto
│ ├── HomeTasks/ # Ex.: Tarefas da casa
│ │ ├── Model/
│ │ ├── ViewModel/
│ │ └── Views/
│ ├── Deals
│ ├── Rewards/
│ └── CommonComponents/ # Componentes compartilhados entre domínios
├── Protocols/ # Protocolos e contratos reutilizáveis
├── Resources/ # Assets, fontes e arquivos estáticos
└── Services/ # Serviços independentes de UI (CloudKit, etc.)
```


---

### **Por que essa organização foi escolhida?**

Essa estrutura favorece:

- **Baixo acoplamento:** cada domínio funciona como um mini-módulo isolado.  
- **Alta coesão:** cada pasta contém apenas o que pertence ao mesmo contexto.  
- **Escalabilidade:** novos domínios podem ser adicionados facilmente.  
- **Testabilidade:** cada camada pode ser testada separadamente.  
- **Legibilidade:** facilita a navegação e manutenção do código.

---

### **Detalhamento das Camadas**

#### **Model**
- Contém os tipos de domínio: entidades, structs e regras puras de negócio.   

#### **ViewModel**
- Expõe dados para a view usando `ObservableObject` ou `@Observable`.  
- Lida com intenção do usuário (Intent Functions).  
- Converte modelos para formatos prontos para exibir.  
- Orquestra ações chamando serviços, persistência e lógica de negócio.

#### **View**
- Composição de interface usando **SwiftUI**.  
- Observa o estado através do ViewModel.  
- Divide a UI em **Views** e **Components** reutilizáveis para manter modularidade.

---

### **Navegação: Coordinator Pattern**

O app utiliza um **Coordinator** para gerenciar fluxos de navegação de forma:

- centralizada  
- independente das Views  
- declarativa  
- fácil de testar  

Isso evita que Views fiquem responsáveis pela navegação e permite que toda a lógica de fluxo seja agrupada em um único lugar. 

---

### **Serviços**

Os serviços ficam na pasta `Services/` e são responsáveis por:

- Persistência com **CloudKit** (incluindo CRUD genérico)  
- Notificações  
- Sincronização  
- Operações assíncronas e independentes da UI  

Cada serviço é isolado, testável e pode ser injetado nos ViewModels.

---

### **Common Components**

Componentes visuais reutilizáveis que podem ser usados em qualquer domínio.  
Exemplos:
- cartões  
- botões  
- layouts  
- indicadores  
- modais reutilizáveis  

## Minhas responsabilidades neste projeto

- **Implementação completa do serviço de CloudKit:** incluindo criação das zonas, containers, operações assíncronas e camadas de CRUD genéricas e específicas.  
- **Configuração dos bancos de dados:** definição da estrutura de dados no iCloud, organização dos registros e lógica de sincronização.  
- **Desenvolvimento de telas do aplicativo:** incluindo interfaces funcionais e componentes reutilizáveis dentro dos domínios do projeto.  
- **Criação de animações e transições:** para aprimorar a experiência do usuário e reforçar a sensação de colaboração no app.

---

## Disponível na App Store (:
https://apps.apple.com/br/app/duet-organizer-for-couples/id6753019952

---

_O app segue em andamento, por isso algumas funções ainda serão implementadas futuramente. Além disso, qualquer feedback será muito bem vindo._ 

Projeto colaborativo desenvolvido por:
- **Pedro Larry**
- **Amanda Rabelo** (https://github.com/amandrbl)
- **Ana Beatriz Seixas** (https://github.com/aseixas7)
