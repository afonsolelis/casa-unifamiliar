# Diretrizes de Revisão de Código - Casa Unifamiliar

## 📋 Índice
- [Objetivos da Revisão](#objetivos-da-revisão)
- [Processo de Revisão](#processo-de-revisão)
- [Critérios de Aprovação](#critérios-de-aprovação)
- [Checklist do Revisor](#checklist-do-revisor)
- [Checklist do Autor](#checklist-do-autor)
- [Tipos de Feedback](#tipos-de-feedback)
- [Boas Práticas](#boas-práticas)
- [Ferramentas](#ferramentas)
- [Métricas](#métricas)

## 🎯 Objetivos da Revisão

### Principais Objetivos
1. **Qualidade**: Garantir que o código atenda aos padrões estabelecidos
2. **Funcionalidade**: Verificar se a implementação atende aos requisitos
3. **Manutenibilidade**: Assegurar que o código seja fácil de manter
4. **Performance**: Identificar possíveis gargalos e otimizações
5. **Segurança**: Detectar vulnerabilidades e riscos
6. **Aprendizado**: Compartilhar conhecimento entre a equipe

### Benefícios
- Redução de bugs em produção
- Melhoria contínua da qualidade
- Padronização do código
- Transferência de conhecimento
- Detecção precoce de problemas

## 🔄 Processo de Revisão

### Fluxo Padrão
1. **Desenvolvimento**: Autor cria feature branch
2. **Testes**: Autor executa testes locais
3. **Pull Request**: Criação do PR com descrição detalhada
4. **Revisão**: Pelo menos 2 revisores aprovam
5. **Merge**: Após aprovação, merge na branch principal
6. **Deploy**: Deploy automático (se configurado)

### Responsabilidades

#### Autor do PR
- Criar PR com descrição clara
- Executar testes antes de submeter
- Responder feedback de forma construtiva
- Fazer ajustes solicitados

#### Revisor
- Revisar código dentro de 24h
- Fornecer feedback construtivo
- Aprovar ou solicitar mudanças
- Verificar se testes foram adicionados

#### Tech Lead
- Revisar PRs críticos
- Decidir sobre mudanças arquiteturais
- Aprovar mudanças que afetam performance

## ✅ Critérios de Aprovação

### Obrigatórios
- [ ] Código segue padrões estabelecidos
- [ ] Testes unitários passam
- [ ] Testes de integração passam
- [ ] Cobertura de testes adequada (>80%)
- [ ] Documentação atualizada
- [ ] Sem vulnerabilidades de segurança
- [ ] Performance aceitável
- [ ] Aprovação de pelo menos 2 revisores

### Desejáveis
- [ ] Código limpo e legível
- [ ] Comentários adequados
- [ ] Tratamento de erros robusto
- [ ] Logs apropriados
- [ ] Otimizações implementadas

## 🔍 Checklist do Revisor

### Funcionalidade
- [ ] O código implementa o que foi solicitado?
- [ ] A lógica está correta?
- [ ] Edge cases foram considerados?
- [ ] Tratamento de erros está adequado?
- [ ] Validações de entrada estão presentes?

### Qualidade de Código
- [ ] Código está limpo e legível?
- [ ] Nomenclatura está clara e consistente?
- [ ] Funções são pequenas e focadas?
- [ ] Não há duplicação de código?
- [ ] Complexidade ciclomática é aceitável?

### Arquitetura
- [ ] Design patterns apropriados?
- [ ] Separação de responsabilidades?
- [ ] Acoplamento baixo?
- [ ] Coesão alta?
- [ ] Reutilização de código?

### Performance
- [ ] Algoritmos eficientes?
- [ ] Não há memory leaks?
- [ ] Queries otimizadas?
- [ ] Cache implementado quando necessário?
- [ ] Lazy loading quando apropriado?

### Segurança
- [ ] Validação de entrada?
- [ ] Sanitização de dados?
- [ ] Autenticação/autorização?
- [ ] Não há exposição de dados sensíveis?
- [ ] HTTPS em produção?

### Testes
- [ ] Testes unitários adequados?
- [ ] Testes de integração?
- [ ] Mocks apropriados?
- [ ] Cobertura de código suficiente?
- [ ] Testes de edge cases?

### Documentação
- [ ] README atualizado?
- [ ] Comentários no código?
- [ ] JSDoc/TSDoc adequado?
- [ ] Changelog atualizado?
- [ ] Documentação de API?

## 📝 Checklist do Autor

### Antes de Submeter
- [ ] Código foi testado localmente
- [ ] Todos os testes passam
- [ ] Linting sem erros
- [ ] Formatação aplicada
- [ ] Commits organizados
- [ ] Branch atualizada com main

### Descrição do PR
- [ ] Título claro e descritivo
- [ ] Descrição detalhada das mudanças
- [ ] Screenshots (se aplicável)
- [ ] Links para issues relacionadas
- [ ] Instruções de teste
- [ ] Breaking changes documentados

### Após Feedback
- [ ] Responder todos os comentários
- [ ] Fazer ajustes solicitados
- [ ] Testar mudanças
- [ ] Atualizar descrição se necessário

## 💬 Tipos de Feedback

### Sugestões (Suggestion)
```typescript
// 💡 Sugestão: Considere usar optional chaining
- const user = data.user && data.user.profile;
+ const user = data.user?.profile;
```

### Questões (Question)
```typescript
// ❓ Pergunta: Por que usar setTimeout aqui? 
// Não seria melhor usar requestAnimationFrame?
setTimeout(() => {
  updateUI();
}, 16);
```

### Problemas (Problem)
```typescript
// 🚨 Problema: Esta função pode retornar undefined
// Considere adicionar validação ou tipo de retorno
function getUser(id: string) {
  return users.find(u => u.id === id);
}
```

### Elogios (Praise)
```typescript
// ✅ Excelente: Boa implementação do padrão Observer
// Código limpo e bem estruturado!
```

## 🎯 Boas Práticas

### Para Revisores

#### Seja Construtivo
```markdown
❌ Ruim: "Este código está horrível"
✅ Bom: "Sugiro refatorar esta função para melhorar a legibilidade. 
         Considere quebrar em funções menores."
```

#### Seja Específico
```markdown
❌ Ruim: "Melhore a performance"
✅ Bom: "Esta query pode ser otimizada usando um índice na coluna 'email'. 
         Considere adicionar um índice composto em (user_id, created_at)."
```

#### Seja Educativo
```markdown
✅ Bom: "Para melhorar a performance, considere usar React.memo() aqui. 
        Isso evitará re-renders desnecessários quando as props não mudarem."
```

### Para Autores

#### Seja Responsivo
- Responda feedback em até 24h
- Faça perguntas se não entender
- Implemente sugestões quando apropriado

#### Seja Proativo
- Antecipe possíveis questões
- Documente decisões arquiteturais
- Inclua testes para casos complexos

## 🛠️ Ferramentas

### Análise Estática
- **ESLint**: Detecção de problemas de código
- **SonarQube**: Análise de qualidade
- **CodeClimate**: Métricas de código
- **Snyk**: Detecção de vulnerabilidades

### Revisão de Código
- **GitHub/GitLab**: Interface de revisão
- **Review Board**: Ferramenta dedicada
- **Phabricator**: Plataforma completa
- **Crucible**: Ferramenta enterprise

### Automação
- **Husky**: Git hooks
- **lint-staged**: Lint apenas arquivos modificados
- **CI/CD**: Testes automáticos
- **Dependabot**: Atualizações de dependências

## 📊 Métricas

### Métricas de Qualidade
- **Tempo médio de revisão**: < 24h
- **Taxa de aprovação**: > 90%
- **Bugs em produção**: < 5% relacionados a PRs
- **Cobertura de testes**: > 80%

### Métricas de Processo
- **PRs por desenvolvedor/semana**
- **Tempo médio de merge**
- **Taxa de rejeição**
- **Número de revisões por PR**

### Dashboards
- Configure dashboards para monitorar:
  - PRs abertos há mais de 48h
  - Taxa de bugs por PR
  - Tempo de ciclo de desenvolvimento
  - Satisfação da equipe com o processo

## 🚨 Sinais de Alerta

### Red Flags
- PRs muito grandes (>500 linhas)
- Muitas mudanças não relacionadas
- Falta de testes
- Código complexo sem documentação
- Mudanças em arquivos críticos sem revisão adequada

### Ações Corretivas
- Quebrar PRs grandes em menores
- Solicitar mais testes
- Pedir documentação adicional
- Revisar arquitetura para mudanças grandes

## 📚 Recursos Adicionais

### Treinamento
- Workshops sobre code review
- Sessões de pair programming
- Compartilhamento de boas práticas
- Retrospectivas sobre o processo

### Documentação
- Guias de estilo de código
- Padrões arquiteturais
- Templates de PR
- Exemplos de boas práticas

---

## 🎯 Checklist Rápido

### Para Aprovar um PR
- [ ] Funcionalidade implementada corretamente
- [ ] Código limpo e legível
- [ ] Testes adequados
- [ ] Performance aceitável
- [ ] Segurança validada
- [ ] Documentação atualizada
- [ ] Sem breaking changes não documentados

### Para Solicitar Mudanças
- [ ] Problemas de funcionalidade
- [ ] Violações de padrões
- [ ] Falta de testes
- [ ] Problemas de performance
- [ ] Vulnerabilidades de segurança
- [ ] Código não legível

---

*Este documento deve ser revisado trimestralmente e atualizado conforme a evolução da equipe e do projeto.*
