# 🤝 Contribuindo para o Epístola

Obrigado por seu interesse em contribuir para o Epístola! Este documento fornece diretrizes para contribuições efetivas.

## 🎯 Como Contribuir

### 1. 🐛 Reportando Bugs
- Use os templates de issue do GitHub
- Forneça informações detalhadas sobre reprodução
- Inclua logs e screenshots quando aplicável
- Verifique se já não existe issue similar

### 2. 💡 Sugerindo Features
- Descreva o problema que a feature resolve
- Explique como a funcionalidade deveria funcionar
- Considere alternativas e trade-offs
- Relacione com os milestones existentes

### 3. 🔧 Contribuindo com Código
- Fork o repositório
- Crie uma branch descritiva (`feature/auth-improvements`)
- Faça commits pequenos e focados
- Escreva testes para novas funcionalidades
- Siga os padrões de código estabelecidos

## 📋 Processo de Development

### Setup do Ambiente
```bash
# Clone o repositório
git clone https://github.com/epistola-com-br/Epistola.git
cd Epistola

# Instale dependências (quando disponível)
npm install
# ou
pip install -r requirements.txt

# Configure variáveis de ambiente
cp .env.example .env

# Execute testes
npm test
# ou
pytest
```

### Workflow de Git
```bash
# Crie uma nova branch
git checkout -b feature/nova-funcionalidade

# Faça suas alterações
git add .
git commit -m "feat: adiciona nova funcionalidade X"

# Push da branch
git push origin feature/nova-funcionalidade

# Abra um Pull Request
```

## 📝 Padrões de Código

### Commits
Seguimos [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: nova funcionalidade
fix: correção de bug
docs: documentação
style: formatação
refactor: refatoração
test: testes
chore: tarefas auxiliares
```

### Code Style
- Use nomes descritivos para variáveis e funções
- Mantenha funções pequenas e focadas
- Comente código complexo
- Remova código morto

### Testes
- Escreva testes unitários para nova lógica
- Mantenha cobertura > 80%
- Use nomes descritivos para testes
- Teste casos edge e errors

## 🏷️ Labels e Issues

### Prioridades
- 🔴 `critical` - Bloqueia desenvolvimento
- 🟡 `high` - Importante para MVP
- 🟢 `medium` - Melhoria significativa
- 🔵 `low` - Nice to have

### Categorias
- `backend` - APIs e lógica de negócio
- `frontend` - Interface de usuário
- `database` - Modelagem de dados
- `security` - Segurança
- `devops` - Infraestrutura
- `docs` - Documentação
- `testing` - Testes

### Status
- `needs-triage` - Precisa análise
- `ready-for-dev` - Pronto para desenvolvimento
- `in-progress` - Em desenvolvimento
- `needs-review` - Aguarda review
- `blocked` - Bloqueado

## 🔍 Review Process

### Para Revisores
- Verifique se resolve a issue relacionada
- Teste localmente quando possível
- Considere impacto em performance
- Valide se seguiu padrões de código
- Seja construtivo nos comentários

### Para Desenvolvedores
- Responda comentários de review
- Faça mudanças solicitadas
- Mantenha PR atualizado com main
- Documente decisões arquiteturais

## 🚀 Release Process

### Versioning
Seguimos [Semantic Versioning](https://semver.org/):
- `MAJOR`: Breaking changes
- `MINOR`: Novas funcionalidades
- `PATCH`: Bug fixes

### Deploy
1. Merge para `main` após review
2. CI/CD executa testes automáticos
3. Deploy automático para staging
4. Validação manual
5. Deploy para produção

## 📚 Recursos

### Documentação
- [Arquitetura](./docs/architecture.md)
- [API Docs](./docs/api.md)
- [Roadmap](./ROADMAP.md)
- [Milestones](./MILESTONES.md)

### Comunicação
- **Issues**: Para bugs e features
- **Discussions**: Para dúvidas gerais
- **Discord**: Para chat em tempo real _(em breve)_

## ❓ Dúvidas Frequentes

### "Como posso ajudar sendo iniciante?"
- Comece com issues marcadas como `good-first-issue`
- Contribua com documentação
- Teste features e reporte bugs
- Sugira melhorias de UX

### "Que skills preciso ter?"
**Backend**: Node.js/TypeScript, PostgreSQL, Docker  
**Frontend**: React/Next.js, CSS, Design responsivo  
**DevOps**: Docker, CI/CD, Monitoring  
**Geral**: Git, Testing, Documentation

### "Posso trabalhar em uma feature grande?"
- Prefira dividir em issues menores
- Discuta a abordagem antes de começar
- Faça PRs incrementais
- Mantenha comunicação ativa

## 🎉 Reconhecimento

Contribuidores são reconhecidos:
- README com lista de contributors
- Changelog mencionando contribuições
- Participação em decisões arquiteturais
- Possibilidade de se tornar maintainer

## 📄 Código de Conduta

Esperamos que todos os contribuidores:
- Sejam respeitosos e inclusivos
- Aceitem feedback construtivo
- Mantenham discussões focadas no projeto
- Ajudem a criar ambiente acolhedor

Comportamentos inaceitáveis resultarão em advertência ou banimento.

---

**Obrigado por contribuir para o Epístola! 🚀**

*Em caso de dúvidas, abra uma issue ou discussion.*