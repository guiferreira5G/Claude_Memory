# Exemplo de Processamento no Memory - Perfil Overthinking

## **Exemplo Prático de Como Estruturar as Respostas no Sistema Memory**

### **1. ENTIDADES PRINCIPAIS A CRIAR**

```json
// Entidade do Usuário
{
  "name": "default_user",
  "entityType": "person",
  "observations": [
    "Sofre com overthinking há 5 anos",
    "Designer gráfico, 28 anos",
    "Perfeccionista nível 8/10",
    "Prefere explicações detalhadas com exemplos práticos"
  ]
}

// Perfil Psicológico
{
  "name": "perfil_overthinking_user",
  "entityType": "psychological_profile",
  "observations": [
    "Paralisia por análise em decisões criativas",
    "Tende a cenários negativos",
    "Procrastina por medo de imperfeição",
    "Tem 15+ projetos mentais simultâneos"
  ]
}

// Gatilhos Identificados
{
  "name": "gatilho_decisoes_criativas",
  "entityType": "trigger",
  "observations": [
    "Fica paralisado ao escolher direção criativa",
    "Manifesta-se com tensão no peito",
    "Dura em média 2-3 horas de análise"
  ]
}

{
  "name": "gatilho_projetos_importantes",
  "entityType": "trigger", 
  "observations": [
    "Medo de não entregar algo perfeito",
    "Pesquisa excessiva antes de começar",
    "Evita começar para não 'estragar'"
  ]
}

// Estratégias Testadas
{
  "name": "estrategia_pomodoro",
  "entityType": "coping_strategy",
  "observations": [
    "Tentou por 2 semanas",
    "Funcionou parcialmente para tarefas simples",
    "Falhou em projetos criativos complexos"
  ]
}

{
  "name": "estrategia_mindfulness",
  "entityType": "coping_strategy",
  "observations": [
    "Pratica meditação há 6 meses",
    "Ajuda a reconhecer início do overthinking",
    "Não impede a paralisia quando surge"
  ]
}

// Objetivos e Aspirações
{
  "name": "objetivo_principal_user",
  "entityType": "goal",
  "observations": [
    "Finalizar 3 projetos pessoais em 6 meses",
    "Reduzir tempo de análise de 3h para 30min",
    "Desenvolver confiança para 'good enough'"
  ]
}

// Suporte Social
{
  "name": "amiga_sarah",
  "entityType": "person",
  "observations": [
    "Única pessoa que entende o perfil analítico",
    "Consegue dar validação sem pressionar",
    "Designer sênior, referência profissional"
  ]
}
```

### **2. RELAÇÕES A ESTABELECER**

```json
// Relações de Gatilho
{
  "from": "default_user",
  "to": "gatilho_decisoes_criativas", 
  "relationType": "triggered_by"
}

{
  "from": "gatilho_decisoes_criativas",
  "to": "perfil_overthinking_user",
  "relationType": "manifests_as"
}

// Relações de Estratégias
{
  "from": "default_user",
  "to": "estrategia_pomodoro",
  "relationType": "tried"
}

{
  "from": "estrategia_mindfulness",
  "to": "gatilho_decisoes_criativas",
  "relationType": "helps_recognize"
}

// Relações de Objetivos
{
  "from": "default_user",
  "to": "objetivo_principal_user",
  "relationType": "wants_to_achieve"
}

{
  "from": "objetivo_principal_user",
  "to": "perfil_overthinking_user",
  "relationType": "addresses"
}

// Relações Sociais
{
  "from": "default_user",
  "to": "amiga_sarah",
  "relationType": "supported_by"
}

{
  "from": "amiga_sarah",
  "to": "estrategia_validacao",
  "relationType": "provides"
}
```

### **3. OBSERVAÇÕES CONTEXTUAIS IMPORTANTES**

```json
// Padrões Temporais
{
  "entityName": "perfil_overthinking_user",
  "observations": [
    "Pior no período da tarde (14h-18h)",
    "Melhora significativa após exercícios físicos",
    "Paralisia aumenta antes de deadlines"
  ]
}

// Preferências de Comunicação
{
  "entityName": "default_user", 
  "observations": [
    "Prefere estruturas visuais (mapas mentais)",
    "Responde bem a perguntas direcionadas",
    "Precisa de validação antes de grandes mudanças",
    "Funciona melhor com metas micro (diárias)"
  ]
}

// Contexto Profissional
{
  "entityName": "contexto_trabalho_user",
  "observations": [
    "Freelancer há 3 anos",
    "Área criativa exige decisões rápidas", 
    "Clients impacientes com revisões excessivas",
    "Renda varia conforme produtividade"
  ]
}

// Indicadores de Sucesso
{
  "entityName": "metricas_progresso_user",
  "observations": [
    "Tempo de decisão: atualmente 3h, meta 30min",
    "Projetos finalizados: 2 em 6 meses, meta 3 por mês",
    "Nível de satisfação: 4/10, meta 7/10",
    "Horas de overthinking: 20h/semana, meta 5h/semana"
  ]
}
```

### **4. QUERIES ÚTEIS PARA ACOMPANHAMENTO**

```javascript
// Buscar estratégias que funcionaram
memory:search_nodes("estrategia funcionou")

// Identificar gatilhos principais  
memory:search_nodes("gatilho trigger paralisia")

// Verificar progresso em objetivos
memory:search_nodes("objetivo meta progresso")

// Encontrar padrões temporais
memory:search_nodes("período tempo quando")

// Buscar suporte social efetivo
memory:search_nodes("ajuda suporte funciona")
```

### **5. ESTRUTURA DE FOLLOW-UP SEMANAL**

**Entidades a atualizar regularmente:**
- `progresso_semanal_[data]`: Observações sobre avanços
- `episodios_overthinking_[data]`: Registrar ocorrências e contexto  
- `estrategias_testadas_[data]`: Novas tentativas e resultados
- `insights_[data]`: Descobertas importantes sobre padrões

**Relações a monitorar:**
- Quais gatilhos estão diminuindo
- Quais estratégias estão ganhando efetividade
- Como objetivos estão sendo alcançados
- Mudanças no suporte social

### **6. TEMPLATE DE SESSÃO DE ACOMPANHAMENTO**

```json
// Criar nova entidade a cada sessão
{
  "name": "sessao_[data]",
  "entityType": "therapy_session",
  "observations": [
    "Episódios de overthinking esta semana: [número]",
    "Gatilho mais frequente: [gatilho]",
    "Estratégia mais efetiva: [estratégia]",
    "Insight principal: [descoberta]",
    "Nível de energia/motivação: [1-10]"
  ]
}

// Relacionar com progresso
{
  "from": "sessao_[data]",
  "to": "objetivo_principal_user",
  "relationType": "contributes_to"
}
```

### **7. INDICADORES DE MELHORIA A MONITORAR**

```json
{
  "name": "indicadores_melhoria",
  "entityType": "metrics",
  "observations": [
    "Redução do tempo de análise antes de agir",
    "Aumento do número de decisões tomadas por dia",
    "Diminuição da ansiedade física (tensão, respiração)",
    "Maior satisfação com projetos entregues",
    "Feedback positivo de clientes sobre agilidade",
    "Melhoria na qualidade do sono",
    "Aumento da autoconfiança em decisões criativas"
  ]
}
```

### **8. ALERTAS E PADRÕES DE RISCO**

```json
// Identificar sinais de recaída
{
  "name": "sinais_alerta",
  "entityType": "warning_signs",
  "observations": [
    "Mais de 5h de análise em uma decisão",
    "Evitar começar projetos por mais de 3 dias",
    "Procrastinação aumentando gradualmente",
    "Feedback negativo repetido sobre lentidão",
    "Diminuição da qualidade do sono por overthinking",
    "Isolamento social por vergonha da paralisia"
  ]
}

// Relacionar com estratégias de emergência
{
  "from": "sinais_alerta",
  "to": "protocolo_emergencia",
  "relationType": "triggers"
}
```

Este sistema permitirá um acompanhamento detalhado e personalizado da evolução do usuário, identificando padrões sutis e adaptando estratégias de forma contínua, sempre com base em dados concretos armazenados na memória do sistema.