# Padrões de Código - Casa Unifamiliar

## 📋 Índice
- [Convenções Gerais](#convenções-gerais)
- [Estrutura de Arquivos](#estrutura-de-arquivos)
- [Nomenclatura](#nomenclatura)
- [Documentação](#documentação)
- [Tratamento de Erros](#tratamento-de-erros)
- [Performance](#performance)
- [Segurança](#segurança)
- [Testes](#testes)
- [Versionamento](#versionamento)

## 🎯 Convenções Gerais

### Princípios Fundamentais
- **SOLID**: Aplicar os princípios SOLID em todo o código
- **DRY**: Don't Repeat Yourself - evite duplicação de código
- **KISS**: Keep It Simple, Stupid - mantenha o código simples
- **YAGNI**: You Aren't Gonna Need It - não implemente funcionalidades desnecessárias

### Qualidade de Código
- **Legibilidade**: Código deve ser autoexplicativo
- **Manutenibilidade**: Fácil de modificar e estender
- **Testabilidade**: Código deve ser facilmente testável
- **Performance**: Otimizado para performance quando necessário

## 📁 Estrutura de Arquivos

### Organização de Diretórios
```
src/
├── components/          # Componentes reutilizáveis
├── pages/              # Páginas da aplicação
├── services/           # Serviços e APIs
├── utils/              # Funções utilitárias
├── hooks/              # Custom hooks (React)
├── types/              # Definições de tipos (TypeScript)
├── constants/          # Constantes da aplicação
├── assets/             # Imagens, ícones, etc.
└── tests/              # Testes unitários e de integração
```

### Convenções de Arquivos
- **Componentes**: PascalCase (`UserProfile.tsx`)
- **Utilitários**: camelCase (`formatDate.ts`)
- **Constantes**: UPPER_SNAKE_CASE (`API_ENDPOINTS.ts`)
- **Tipos**: PascalCase (`UserTypes.ts`)

## 🏷️ Nomenclatura

### Variáveis e Funções
```typescript
// ✅ Bom
const userName = 'João';
const isUserActive = true;
const getUserProfile = () => {};

// ❌ Ruim
const u = 'João';
const flag = true;
const get = () => {};
```

### Classes e Interfaces
```typescript
// ✅ Bom
class UserService {}
interface UserProfile {}
type UserRole = 'admin' | 'user';

// ❌ Ruim
class userService {}
interface userProfile {}
```

### Constantes
```typescript
// ✅ Bom
const MAX_RETRY_ATTEMPTS = 3;
const API_BASE_URL = 'https://api.example.com';

// ❌ Ruim
const maxRetryAttempts = 3;
const apiBaseUrl = 'https://api.example.com';
```

## 📚 Documentação

### Comentários
```typescript
/**
 * Calcula o desconto baseado no tipo de usuário e valor da compra
 * @param userType - Tipo do usuário (premium, standard, basic)
 * @param purchaseValue - Valor da compra em reais
 * @returns Valor do desconto calculado
 */
function calculateDiscount(userType: UserType, purchaseValue: number): number {
  // Implementação...
}
```

### README
- Documentar setup e instalação
- Explicar arquitetura do projeto
- Incluir exemplos de uso
- Manter atualizado

## ⚠️ Tratamento de Erros

### Estratégias
```typescript
// ✅ Tratamento explícito
try {
  const result = await apiCall();
  return result;
} catch (error) {
  logger.error('API call failed:', error);
  throw new CustomError('Failed to fetch data', error);
}

// ✅ Validação de entrada
function validateEmail(email: string): boolean {
  if (!email || typeof email !== 'string') {
    throw new ValidationError('Email is required and must be a string');
  }
  return emailRegex.test(email);
}
```

### Logs
- Use níveis apropriados (debug, info, warn, error)
- Inclua contexto relevante
- Evite logs sensíveis (senhas, tokens)

## 🚀 Performance

### Otimizações
```typescript
// ✅ Lazy loading
const LazyComponent = React.lazy(() => import('./HeavyComponent'));

// ✅ Memoização
const MemoizedComponent = React.memo(ExpensiveComponent);

// ✅ Debounce para inputs
const debouncedSearch = useMemo(
  () => debounce(handleSearch, 300),
  [handleSearch]
);
```

### Boas Práticas
- Evite re-renders desnecessários
- Use `useCallback` e `useMemo` adequadamente
- Implemente virtualização para listas grandes
- Otimize imagens e assets

## 🔒 Segurança

### Validação de Dados
```typescript
// ✅ Validação de entrada
function sanitizeInput(input: string): string {
  return input.trim().replace(/<script\b[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>/gi, '');
}

// ✅ Validação de tipos
function isValidUser(user: unknown): user is User {
  return (
    typeof user === 'object' &&
    user !== null &&
    'id' in user &&
    'email' in user
  );
}
```

### Boas Práticas
- Sempre valide dados de entrada
- Use HTTPS em produção
- Implemente rate limiting
- Sanitize dados antes de exibir
- Use bibliotecas de validação confiáveis

## 🧪 Testes

### Estrutura de Testes
```typescript
// ✅ Teste unitário
describe('UserService', () => {
  it('should create user with valid data', async () => {
    const userData = { name: 'João', email: 'joao@example.com' };
    const result = await userService.createUser(userData);
    
    expect(result).toBeDefined();
    expect(result.name).toBe(userData.name);
  });
});

// ✅ Teste de integração
describe('User API', () => {
  it('should return user list', async () => {
    const response = await request(app)
      .get('/api/users')
      .expect(200);
    
    expect(response.body).toHaveProperty('users');
    expect(Array.isArray(response.body.users)).toBe(true);
  });
});
```

### Cobertura
- Mínimo 80% de cobertura de código
- Teste casos de sucesso e falha
- Teste edge cases
- Use mocks para dependências externas

## 📦 Versionamento

### Git Flow
```bash
# Branches principais
main          # Produção
develop       # Desenvolvimento
feature/*     # Novas funcionalidades
hotfix/*      # Correções urgentes
release/*     # Preparação de releases
```

### Commits
```bash
# Formato: tipo(escopo): descrição
feat(auth): add OAuth2 authentication
fix(api): resolve user creation bug
docs(readme): update installation guide
refactor(utils): simplify date formatting
test(auth): add unit tests for login
```

### Tags
- Use versionamento semântico (v1.0.0)
- Tag releases estáveis
- Documente breaking changes

## 🔧 Ferramentas Recomendadas

### Linting e Formatação
- **ESLint**: Análise estática de código
- **Prettier**: Formatação automática
- **Husky**: Git hooks
- **lint-staged**: Lint apenas arquivos staged

### Qualidade
- **SonarQube**: Análise de qualidade
- **CodeClimate**: Métricas de código
- **Coverage**: Cobertura de testes

### Desenvolvimento
- **TypeScript**: Tipagem estática
- **Jest**: Framework de testes
- **Storybook**: Desenvolvimento de componentes
- **Webpack/Vite**: Bundling

## 📊 Métricas de Qualidade

### Objetivos
- **Complexidade Ciclomática**: < 10
- **Cobertura de Testes**: > 80%
- **Duplicação de Código**: < 3%
- **Debt Ratio**: < 5%

### Monitoramento
- Configure alertas para degradação de qualidade
- Revise métricas semanalmente
- Ajuste padrões conforme necessário

---

## 🎯 Checklist de Code Review

Antes de submeter um PR, verifique:

- [ ] Código segue os padrões estabelecidos
- [ ] Testes foram adicionados/atualizados
- [ ] Documentação foi atualizada
- [ ] Performance foi considerada
- [ ] Segurança foi validada
- [ ] Commits seguem o padrão estabelecido
- [ ] Não há código comentado ou console.log
- [ ] Tratamento de erros está implementado
- [ ] Tipos TypeScript estão definidos
- [ ] Código está limpo e legível

---

*Este documento deve ser revisado e atualizado regularmente conforme a evolução do projeto.*
