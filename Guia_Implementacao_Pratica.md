# Guia Prático de Implementação - Sistema Memory para Overthinking

## **PASSO A PASSO PARA IMPLEMENTAR O SISTEMA**

### **FASE 1: PREPARAÇÃO (Week 1)**

#### 1.1 Instalação do MCP Memory
```bash
# Opção 1: Via NPX
npx -y @modelcontextprotocol/server-memory

# Opção 2: Via Docker
docker run -i -v claude-memory:/app/dist --rm mcp/memory
```

#### 1.2 Configuração no Claude Desktop
Adicionar ao `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"],
      "env": {
        "MEMORY_FILE_PATH": "/path/to/overthinking_memory.json"
      }
    }
  }
}
```

#### 1.3 Primeiro Contato com o Sistema
- Responder ao questionário completo
- Processar respostas usando as funções do Memory
- Validar se todas as entidades foram criadas corretamente

---

### **FASE 2: ESTRUTURAÇÃO INICIAL (Week 2)**

#### 2.1 Criação das Entidades Base
```javascript
// Executar no Claude com Memory ativo
memory:create_entities([
  {
    "name": "default_user",
    "entityType": "person",
    "observations": ["Dados básicos do questionário"]
  },
  {
    "name": "perfil_overthinking", 
    "entityType": "psychological_profile",
    "observations": ["Características do overthinking identificadas"]
  }
])
```

#### 2.2 Mapeamento de Gatilhos
```javascript
memory:create_entities([
  {
    "name": "gatilho_decisoes_importantes",
    "entityType": "trigger",
    "observations": ["Descrição detalhada do gatilho"]
  }
])

memory:create_relations([
  {
    "from": "default_user",
    "to": "gatilho_decisoes_importantes",
    "relationType": "triggered_by"
  }
])
```

#### 2.3 Registro de Estratégias Tentadas
```javascript
memory:create_entities([
  {
    "name": "estrategia_pomodoro",
    "entityType": "coping_strategy", 
    "observations": ["Tentou por 2 semanas", "Resultado parcial"]
  }
])
```

---

### **FASE 3: MONITORAMENTO DIÁRIO (Semanas 3-4)**

#### 3.1 Check-in Diário
**Template de conversa diária:**
```
Claude: "Lembrando..."
[Claude acessa memory:read_graph()]

"Como foi seu dia em relação ao overthinking?
- Quantos episódios de paralisia?
- Quais gatilhos foram ativados?
- Que estratégias você usou?
- O que funcionou/não funcionou?"
```

#### 3.2 Registro de Episódios
```javascript
memory:create_entities([
  {
    "name": "episodio_2025_07_23",
    "entityType": "overthinking_episode",
    "observations": [
      "Duração: 2 horas",
      "Gatilho: Escolha de cor para logo",
      "Sintomas físicos: Tensão no peito",
      "Resolução: Pediu opinião da Sarah"
    ]
  }
])
```

#### 3.3 Atualização de Progresso
```javascript
memory:add_observations([
  {
    "entityName": "default_user",
    "contents": ["Melhorou 20% no tempo de decisão esta semana"]
  }
])
```

---

### **FASE 4: ANÁLISE SEMANAL (Ongoing)**

#### 4.1 Identificação de Padrões
```javascript
// Buscar padrões de gatilhos
memory:search_nodes("gatilho trigger")

// Analisar efetividade de estratégias
memory:search_nodes("estrategia funcionou")

// Verificar progressão em objetivos
memory:search_nodes("objetivo meta progresso")
```

#### 4.2 Relatório Semanal Automatizado
**Template de análise:**
```
"Com base na sua memória, vejo que:

📈 PROGRESSOS:
- [Padrões positivos identificados]
- [Estratégias que estão funcionando]

⚠️ PONTOS DE ATENÇÃO:
- [Gatilhos mais frequentes]
- [Padrões preocupantes]

🎯 RECOMENDAÇÕES:
- [Ajustes baseados nos dados]
- [Novas estratégias a testar]"
```

---

### **FASE 5: OTIMIZAÇÃO CONTÍNUA**

#### 5.1 Refinamento de Estratégias
```javascript
// Atualizar estratégias baseado em resultados
memory:add_observations([
  {
    "entityName": "estrategia_mindfulness",
    "contents": ["Mais efetiva quando praticada de manhã"]
  }
])

// Criar novas estratégias
memory:create_entities([
  {
    "name": "estrategia_timer_decisao",
    "entityType": "coping_strategy",
    "observations": ["Limita tempo de análise a 15min", "Testando por 1 semana"]
  }
])
```

#### 5.2 Evolução de Objetivos
```javascript
// Atualizar objetivos conforme progresso
memory:add_observations([
  {
    "entityName": "objetivo_principal_user",
    "contents": ["Meta de 30min atingida, nova meta: 15min"]
  }
])
```

---

### **FUNCIONALIDADES AVANÇADAS**

#### 6.1 Sistema de Alertas
```javascript
// Criar gatilhos de alerta
memory:create_entities([
  {
    "name": "alerta_regressao",
    "entityType": "alert_system", 
    "observations": [
      "Ativa quando >3 episódios longos por semana",
      "Sugere contato com suporte social",
      "Recomenda técnicas de emergência"
    ]
  }
])
```

#### 6.2 Integração com Calendário
```javascript
// Registrar correlações temporais
memory:create_entities([
  {
    "name": "padrao_temporal_tardes",
    "entityType": "time_pattern",
    "observations": [
      "Overthinking pior entre 14h-17h",
      "Coincide com baixa de energia pós-almoço",
      "Estratégia: pausas ativas neste horário"
    ]
  }
])
```

#### 6.3 Rastreamento de Humor
```javascript
// Correlacionar humor com episódios
memory:create_entities([
  {
    "name": "humor_tracking",
    "entityType": "mood_tracker",
    "observations": ["Humor baixo = mais overthinking", "Humor alto = mais ação"]
  }
])
```

---

### **DICAS DE OTIMIZAÇÃO**

#### 7.1 Nomeação Consistente
- Use sempre `default_user` para o usuário principal
- Prefixos padrão: `gatilho_`, `estrategia_`, `objetivo_`, `episodio_`
- Datas no formato: `YYYY_MM_DD`

#### 7.2 Observações Atômicas
- Uma observação = um fato
- Evite observações compostas
- Use linguagem objetiva e mensurável

#### 7.3 Relações Significativas
- Sempre em voz ativa
- Tipos padronizados: `triggered_by`, `helps_with`, `leads_to`
- Evite relações redundantes

#### 7.4 Queries Eficientes
- Use palavras-chave específicas
- Combine termos para filtrar melhor
- Teste diferentes formulações da query

---

### **TROUBLESHOOTING COMUM**

**Problema**: Memory não lembra informações importantes  
**Solução**: Verificar se entidades foram criadas com `memory:read_graph()`

**Problema**: Muitas entidades similares  
**Solução**: Consolidar usando `memory:delete_entities()` e recriar

**Problema**: Dificuldade para encontrar informações  
**Solução**: Melhorar nomeação e adicionar mais observações descritivas

**Problema**: Relações confusas  
**Solução**: Revisar tipos de relação e usar sempre voz ativa

---

### **CHECK-LIST DE IMPLEMENTAÇÃO**

- [ ] MCP Memory instalado e configurado
- [ ] Questionário respondido completamente
- [ ] Entidades base criadas (usuário, perfil, gatilhos, estratégias)
- [ ] Relações fundamentais estabelecidas
- [ ] Sistema de monitoramento diário ativo
- [ ] Processo de análise semanal definido
- [ ] Métricas de progresso estabelecidas
- [ ] Sistema de alertas configurado
- [ ] Backup regular da memória configurado

**Resultado esperado**: Sistema completo de acompanhamento personalizado que evolui com o usuário, fornecendo insights precisos e suporte contínuo para superar paralisia por análise.