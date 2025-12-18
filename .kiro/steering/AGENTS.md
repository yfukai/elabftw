---
inclusion: always
---

# eLabFTW Development Guidelines

## Project Overview
eLabFTW is a free, open-source electronic lab notebook for research teams. It's a PHP-based web application with TypeScript frontend components, using modern web technologies and following security best practices.

## Architecture & Technology Stack

### Backend (PHP 8.3+)
- **Framework**: Custom MVC architecture with Symfony components
- **Database**: MySQL/MariaDB with PDO
- **Authentication**: Multi-factor auth, LDAP, SAML support
- **Security**: CSRF protection, input validation, encrypted storage
- **File Structure**: PSR-4 autoloading, namespace `Elabftw\`

### Frontend
- **Languages**: TypeScript (ES2022), SCSS, HTML5
- **Build Tools**: Webpack, Yarn package manager
- **Libraries**: jQuery, Bootstrap 4, React components, TinyMCE
- **Bundling**: Separate bundles for different page types

### Key Directories
- `src/`: PHP source code (Models, Controllers, Services, etc.)
- `src/ts/`: TypeScript frontend code
- `src/scss/`: Stylesheets
- `web/`: Public web root
- `tests/`: Codeception test suites

## Code Style & Standards

### PHP
- **PSR-12** coding standard enforced by PHP-CS-Fixer
- **Strict typing**: Use type declarations and return types
- **Enums**: Prefer backed enums for constants (PHP 8.1+)
- **Exceptions**: Custom exception hierarchy in `src/Exceptions/`
- **Static Analysis**: Psalm and PHPStan for type checking

### TypeScript/JavaScript
- **ESLint** configuration with TypeScript rules
- **Indentation**: 2 spaces for JS/TS, 4 spaces for PHP/CSS
- **Modules**: Use ES6 imports/exports
- **Types**: Prefer explicit typing where beneficial

### Database
- **Migrations**: Use `src/sql/` for schema changes
- **Prepared Statements**: Always use PDO prepared statements
- **Transactions**: Wrap multi-table operations in transactions

## Security Guidelines

### Input Validation
- **Never trust user input**: Validate and sanitize all inputs
- **CSRF Protection**: Use CSRF tokens for state-changing operations
- **SQL Injection**: Use prepared statements exclusively
- **XSS Prevention**: Escape output, use Twig's auto-escaping

### Authentication & Authorization
- **Permissions**: Check user permissions before any operation
- **Sessions**: Secure session handling with proper regeneration
- **API Keys**: Support for API authentication alongside sessions

## Development Patterns

### Models
- Extend `AbstractEntity` for database entities
- Use `EntitySqlBuilder` for complex queries
- Implement proper validation in model methods

### Controllers
- Extend appropriate abstract controller class
- Keep controllers thin, delegate business logic to services
- Return proper HTTP status codes

### Services
- Single responsibility principle
- Dependency injection through constructor
- Stateless where possible

### Error Handling
- Use custom exceptions with meaningful messages
- Log errors appropriately (Monolog)
- Provide user-friendly error messages

## Testing Requirements

### Unit Tests
- **Codeception** framework for all test types
- **Coverage**: Aim for high test coverage on critical paths
- **Mocking**: Use appropriate mocking for external dependencies

### API Testing
- Test all API endpoints with various scenarios
- Validate response formats and status codes
- Test authentication and authorization

## File Handling
- **Uploads**: Use `CreateUpload` classes for file processing
- **Storage**: Support multiple storage backends (local, S3)
- **Security**: Validate file types and scan for malware

## Internationalization
- **Gettext**: Use `_()` function for translatable strings
- **21 Languages**: Support for multiple languages
- **JavaScript**: Use i18next for frontend translations

## Performance Considerations
- **Caching**: Implement appropriate caching strategies
- **Database**: Optimize queries, use indexes properly
- **Assets**: Minify and compress CSS/JS assets
- **Images**: Generate thumbnails, optimize file sizes

## API Design
- **RESTful**: Follow REST principles for APIv2
- **Versioning**: Maintain backward compatibility
- **Documentation**: OpenAPI specification in `apidoc/v2/`
- **Rate Limiting**: Implement appropriate rate limiting

## Common Pitfalls to Avoid
- Don't bypass permission checks
- Don't use raw SQL queries
- Don't ignore CSRF protection
- Don't store sensitive data in plain text
- Don't trust file uploads without validation
- Don't expose internal error details to users

## Development Workflow
- **Branches**: Use feature branches for development
- **Commits**: Write clear, descriptive commit messages
- **Code Review**: All changes should be reviewed
- **CI/CD**: Tests must pass before merging