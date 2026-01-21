# Contributing to Order Pipeline Managed

Thank you for your interest in contributing! This project is part of a research initiative on observability and resilience in event-driven serverless architectures.

## Code of Conduct

Please treat all contributors with respect. We are committed to providing a welcoming and inclusive environment.

## Getting Started

### Prerequisites
- .NET 8 SDK
- Azure Account with active subscription
- Git
- Visual Studio 2022 or VS Code with C# extension

### Development Setup

1. **Fork and Clone**
   ```bash
   git clone https://github.com/YOUR_USERNAME/order-pipeline-managed.git
   cd order-pipeline-managed
   git remote add upstream https://github.com/LuisMarchio03/order-pipeline-managed.git
   ```

2. **Setup Local Development**
   ```bash
   dotnet restore
   cp .env.example .env
   # Update .env with your Azure configuration
   ```

3. **Create Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

## Development Workflow

### Branching Strategy
- `main` - production-ready code
- `develop` - integration branch (if applicable)
- `feature/*` - feature branches
- `bugfix/*` - bug fix branches
- `docs/*` - documentation updates

### Commit Messages

Use conventional commits:
- `feat:` new feature
- `fix:` bug fix
- `docs:` documentation
- `test:` tests
- `refactor:` code refactoring
- `perf:` performance improvements
- `chore:` maintenance

Example:
```
feat: add order validation in receiver function

- Implement order schema validation
- Add error handling for invalid orders
- Include logging for validation failures
```

## Making Changes

### Code Style
- Follow .NET naming conventions (PascalCase for classes, camelCase for variables)
- Use meaningful variable and method names
- Add XML comments for public APIs
- Keep functions focused and DRY

### Testing

**Unit Tests**
```bash
dotnet test tests/Unit/
```

**Integration Tests**
```bash
dotnet test tests/Integration/
```

Aim for:
- 70%+ code coverage
- Test both happy path and error scenarios
- Use meaningful test names

### Documentation

- Update README.md if changing public APIs
- Add comments for complex logic
- Update relevant docs/ files
- Keep CHANGELOG.md updated

## Submitting Changes

### Pull Request Process

1. **Update your branch**
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```

3. **Create Pull Request**
   - Use a descriptive title
   - Reference related issues (#123)
   - Describe what changed and why
   - Include before/after screenshots if UI changes

4. **PR Checklist**
   - [ ] Tests pass locally
   - [ ] Code follows style guidelines
   - [ ] Documentation is updated
   - [ ] Commit messages follow conventions
   - [ ] No breaking changes (unless documented)

### Review Process

- At least one maintainer review required
- All CI/CD checks must pass
- Resolve conversations before merging
- Squash commits if requested

## Areas for Contribution

### High Priority
- Core Azure Functions implementation
- Observability features
- Performance optimization
- Bug fixes

### Welcome
- Documentation improvements
- Test coverage increases
- Example implementations
- Issue discussions

## Getting Help

- Check existing issues and PRs
- Review documentation in `docs/`
- Ask in issues before starting large changes
- Join discussions for design decisions

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for contributing! Your help makes this research project better.** 🙏
