# Conventional Commits - Agente de Versionamento

## 📋 Visão Geral

Este agente define os padrões de commits convencionais para o projeto Casa Unifamiliar, garantindo um histórico de versionamento claro, consistente e automatizável.

## 🎯 Objetivos

- **Padronizar** mensagens de commit em todo o projeto
- **Facilitar** a geração automática de changelogs
- **Melhorar** a rastreabilidade de mudanças
- **Automatizar** versionamento semântico
- **Simplificar** o processo de code review

## 📝 Formato do Commit

```
<tipo>[escopo opcional]: <descrição>

[corpo opcional]

[rodapé opcional]
```

### Estrutura Detalhada

```
<type>(<scope>): <subject>

<body>

<footer>
```

## 🏷️ Tipos de Commit

### Tipos Principais

#### `feat` - Nova Funcionalidade
```bash
feat(arquitetura): adiciona planta baixa do térreo
feat(estrutural): implementa cálculo de lajes
feat(hidrossanitario): adiciona projeto de instalações
```

#### `fix` - Correção de Bug
```bash
fix(estrutural): corrige cálculo de pilares
fix(arquitetura): ajusta dimensões da sala
fix(orçamento): corrige preço unitário do concreto
```

#### `docs` - Documentação
```bash
docs(readme): atualiza estrutura do projeto
docs(especificacoes): adiciona especificações de materiais
docs(manual): atualiza manual do proprietário
```

#### `style` - Formatação
```bash
style(plantas): ajusta formatação dos desenhos
style(relatorios): padroniza layout dos relatórios
style(documentos): aplica formatação consistente
```

#### `refactor` - Refatoração
```bash
refactor(estrutural): simplifica cálculo de vigas
refactor(arquitetura): reorganiza layout dos cômodos
refactor(orçamento): otimiza planilha de custos
```

#### `perf` - Performance
```bash
perf(estrutural): otimiza cálculo de carregamentos
perf(render): melhora performance dos renderings
perf(calculos): acelera processamento de planilhas
```

#### `test` - Testes
```bash
test(estrutural): adiciona testes de cálculo
test(arquitetura): implementa testes de layout
test(qualidade): adiciona testes de conformidade
```

#### `chore` - Tarefas de Manutenção
```bash
chore(deps): atualiza dependências do projeto
chore(ci): configura pipeline de CI/CD
chore(scripts): adiciona scripts de automação
```

### Tipos Específicos do Projeto

#### `design` - Projeto/Desenho
```bash
design(arquitetura): cria planta baixa do primeiro pavimento
design(estrutural): desenha detalhes de ferragem
design(fachada): desenvolve elevação principal
```

#### `calc` - Cálculos
```bash
calc(estrutural): calcula dimensionamento de pilares
calc(hidrossanitario): dimensiona tubulações
calc(eletrico): calcula cargas elétricas
```

#### `spec` - Especificações
```bash
spec(materiais): especifica concreto C25
spec(execucao): define procedimentos de concretagem
spec(qualidade): estabelece critérios de aceitação
```

#### `budget` - Orçamento
```bash
budget(estrutural): orça materiais estruturais
budget(acabamentos): orça revestimentos
budget(instalacoes): orça instalações elétricas
```

#### `license` - Licenças
```bash
license(ambiental): solicita licença ambiental
license(construcao): renova alvará de construção
license(habite-se): protocola pedido de habite-se
```

## 🎯 Escopos do Projeto

### Escopos Arquitetônicos
- `arquitetura` - Projeto arquitetônico
- `layout` - Layout e distribuição
- `fachada` - Fachadas e elevações
- `corte` - Cortes e seções
- `detalhe` - Detalhes arquitetônicos

### Escopos Estruturais
- `estrutural` - Projeto estrutural
- `fundacao` - Fundações
- `laje` - Lajes
- `viga` - Vigas
- `pilar` - Pilares
- `ferragem` - Ferragem

### Escopos de Instalações
- `hidrossanitario` - Instalações hidrossanitárias
- `eletrico` - Instalações elétricas
- `telefonia` - Instalações de telefonia
- `seguranca` - Sistema de segurança

### Escopos de Gestão
- `orcamento` - Orçamentos e custos
- `cronograma` - Cronogramas
- `licenca` - Licenças e aprovações
- `qualidade` - Controle de qualidade
- `medicao` - Medições e pagamentos

### Escopos de Documentação
- `readme` - Documentação principal
- `manual` - Manuais técnicos
- `especificacao` - Especificações técnicas
- `relatorio` - Relatórios técnicos

## 📋 Exemplos Práticos

### Commits Arquitetônicos
```bash
feat(arquitetura): adiciona planta baixa do térreo
fix(layout): corrige posicionamento da cozinha
design(fachada): desenvolve elevação principal
docs(arquitetura): atualiza memorial descritivo
```

### Commits Estruturais
```bash
calc(estrutural): calcula dimensionamento de pilares
fix(ferragem): corrige detalhes de armadura
spec(concreto): especifica concreto C25
test(estrutural): adiciona testes de cálculo
```

### Commits de Instalações
```bash
feat(hidrossanitario): adiciona projeto de instalações
calc(eletrico): dimensiona cargas elétricas
fix(telefonia): corrige roteamento de cabos
docs(instalacoes): atualiza especificações
```

### Commits de Gestão
```bash
budget(estrutural): orça materiais estruturais
chore(cronograma): atualiza cronograma de execução
license(ambiental): protocola licença ambiental
docs(gestao): atualiza procedimentos
```

## 🔧 Configuração Automática

### Git Hooks
```bash
# .git/hooks/commit-msg
#!/bin/sh
# Validação de formato de commit
commit_regex='^(feat|fix|docs|style|refactor|perf|test|chore|design|calc|spec|budget|license)(\(.+\))?: .{1,50}'

if ! grep -qE "$commit_regex" "$1"; then
    echo "❌ Formato de commit inválido!"
    echo "✅ Use: <tipo>(<escopo>): <descrição>"
    echo "📋 Tipos: feat, fix, docs, style, refactor, perf, test, chore"
    echo "🎯 Escopos: arquitetura, estrutural, hidrossanitario, eletrico, etc."
    exit 1
fi
```

### Scripts de Automação
```bash
#!/bin/bash
# Script para gerar changelog automático

# Gerar changelog baseado em commits
git log --oneline --grep="^feat\|^fix\|^docs" --since="1 month ago" > CHANGELOG.md

# Categorizar commits
echo "# Changelog" > CHANGELOG.md
echo "" >> CHANGELOG.md
echo "## Funcionalidades" >> CHANGELOG.md
git log --oneline --grep="^feat" --since="1 month ago" >> CHANGELOG.md
echo "" >> CHANGELOG.md
echo "## Correções" >> CHANGELOG.md
git log --oneline --grep="^fix" --since="1 month ago" >> CHANGELOG.md
```

## 📊 Versionamento Semântico

### Regras de Versionamento
- **MAJOR** (1.0.0): Mudanças incompatíveis
- **MINOR** (0.1.0): Novas funcionalidades compatíveis
- **PATCH** (0.0.1): Correções compatíveis

### Mapeamento de Commits
```bash
# Commits que geram MAJOR
feat!: quebra compatibilidade
fix!: correção que quebra compatibilidade

# Commits que geram MINOR
feat: nova funcionalidade
design: novo projeto
calc: novo cálculo

# Commits que geram PATCH
fix: correção de bug
docs: atualização de documentação
style: formatação
```

## 🎯 Boas Práticas

### Mensagens de Commit
```bash
# ✅ Bom
feat(arquitetura): adiciona planta baixa do térreo
fix(estrutural): corrige cálculo de pilares
docs(readme): atualiza estrutura do projeto

# ❌ Ruim
adiciona planta
corrige bug
atualiza docs
```

### Descrições
- **Máximo 50 caracteres** no título
- **Verbo no imperativo** (adiciona, corrige, atualiza)
- **Primeira letra minúscula**
- **Sem ponto final** no título
- **Descrição clara e objetiva**

### Corpo do Commit
```bash
feat(estrutural): adiciona cálculo de lajes

Implementa cálculo de lajes maciças de concreto armado
seguindo a NBR 6118. Inclui verificação de flechas e
cálculo de armaduras.

- Adiciona planilha de cálculo
- Implementa verificação de flechas
- Calcula armaduras longitudinais
- Adiciona testes de conformidade

Closes #123
```

## 🔍 Validação e Qualidade

### Checklist de Commit
- [ ] Tipo de commit correto
- [ ] Escopo apropriado
- [ ] Descrição clara e objetiva
- [ ] Máximo 50 caracteres no título
- [ ] Verbo no imperativo
- [ ] Sem ponto final no título
- [ ] Corpo explicativo (se necessário)
- [ ] Referências a issues (se aplicável)

### Ferramentas de Validação
```bash
# Instalar commitizen
npm install -g commitizen

# Configurar conventional commits
commitizen init cz-conventional-changelog --save-dev

# Usar commitizen
git cz
```

## 📚 Recursos Adicionais

### Documentação
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Semantic Versioning](https://semver.org/)
- [Angular Commit Guidelines](https://github.com/angular/angular/blob/main/CONTRIBUTING.md)

### Ferramentas
- **commitizen**: Interface interativa para commits
- **commitlint**: Validação de commits
- **conventional-changelog**: Geração automática de changelogs
- **semantic-release**: Versionamento automático

### Templates
```bash
# Template para commits arquitetônicos
feat(arquitetura): <descrição>

# Template para commits estruturais
calc(estrutural): <descrição>

# Template para commits de instalações
feat(hidrossanitario): <descrição>

# Template para commits de gestão
budget(orcamento): <descrição>
```

## 🎯 Exemplos por Área

### Projeto Arquitetônico
```bash
feat(arquitetura): adiciona planta baixa do térreo
design(layout): desenvolve distribuição dos cômodos
docs(arquitetura): atualiza memorial descritivo
fix(fachada): corrige elevação principal
```

### Projeto Estrutural
```bash
calc(estrutural): calcula dimensionamento de pilares
feat(ferragem): adiciona detalhes de armadura
spec(concreto): especifica concreto C25
test(estrutural): adiciona testes de cálculo
```

### Projeto Hidrossanitário
```bash
feat(hidrossanitario): adiciona projeto de instalações
calc(tubulacoes): dimensiona diâmetros das tubulações
docs(hidrossanitario): atualiza especificações
fix(instalacoes): corrige roteamento de tubos
```

### Projeto Elétrico
```bash
feat(eletrico): adiciona projeto de instalações
calc(cargas): calcula cargas elétricas
docs(eletrico): atualiza especificações
fix(quadros): corrige diagramas elétricos
```

### Orçamentos e Custos
```bash
budget(estrutural): orça materiais estruturais
budget(acabamentos): orça revestimentos
budget(instalacoes): orça instalações elétricas
docs(orcamento): atualiza planilha de custos
```

### Licenças e Aprovações
```bash
license(ambiental): solicita licença ambiental
license(construcao): renova alvará de construção
license(habite-se): protocola pedido de habite-se
docs(licencas): atualiza status das aprovações
```

---

## 🎯 Checklist de Implementação

### Configuração Inicial
- [ ] Instalar commitizen
- [ ] Configurar conventional commits
- [ ] Criar git hooks de validação
- [ ] Configurar scripts de automação
- [ ] Treinar equipe nos padrões

### Uso Diário
- [ ] Usar formato correto nos commits
- [ ] Validar mensagens antes de enviar
- [ ] Gerar changelogs automaticamente
- [ ] Aplicar versionamento semântico
- [ ] Manter histórico limpo e organizado

---

*Este agente deve ser seguido por toda a equipe para garantir consistência no versionamento do projeto.*
