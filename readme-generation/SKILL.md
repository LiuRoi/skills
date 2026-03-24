---
name: readme-generation
description: README best practices including structure, badges, installation, usage, and contributing sections. Use when creating or improving project README files.
---

# README Best Practices

## Recommended Structure

A well-structured README follows this order:

1. **Title and description** — what the project does in one sentence
2. **Badges** — build status, version, license, coverage
3. **Table of contents** — for longer READMEs
4. **Features** — key capabilities
5. **Prerequisites** — required tools and versions
6. **Installation** — step-by-step setup
7. **Usage** — basic examples
8. **Configuration** — environment variables, config files
9. **API reference** — link to detailed docs
10. **Contributing** — how to contribute
11. **License** — license type

## Title and Description

```markdown
# Project Name

One-line description of what this project does and why it exists.
```

Keep it concise. Avoid marketing language.

## Badges

```markdown
[![CI](https://github.com/org/repo/actions/workflows/ci.yml/badge.svg)](https://github.com/org/repo/actions)
[![npm version](https://img.shields.io/npm/v/package-name.svg)](https://www.npmjs.com/package/package-name)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![codecov](https://codecov.io/gh/org/repo/branch/main/graph/badge.svg)](https://codecov.io/gh/org/repo)
```

Only include badges that provide useful information. Common badges: CI status, version, license, coverage, downloads.

## Table of Contents

```markdown
## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [License](#license)
```

Include for READMEs longer than 3 screens.

## Installation

```markdown
## Installation

### Prerequisites

- Node.js >= 18
- PostgreSQL >= 15

### Setup

\`\`\`bash
git clone https://github.com/org/repo.git
cd repo
cp .env.example .env
npm install
npm run db:migrate
npm start
\`\`\`
```

Always include prerequisites, provide copy-pasteable commands, and mention `.env` setup.

## Usage

Show the most common use case first:

```markdown
## Usage

### Basic Example

\`\`\`typescript
import { Client } from 'my-library';

const client = new Client({ apiKey: process.env.API_KEY });
const result = await client.query('SELECT 1');
console.log(result);
\`\`\`

### Advanced Example

\`\`\`typescript
const stream = client.stream('SELECT * FROM users');
for await (const row of stream) {
  process.stdout.write(JSON.stringify(row));
}
\`\`\`
```

## Configuration

Document all environment variables with descriptions and defaults:

```markdown
## Configuration

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `PORT` | Server port | `3000` | No |
| `DATABASE_URL` | PostgreSQL connection string | — | Yes |
| `LOG_LEVEL` | Logging level | `info` | No |
```

## Contributing

```markdown
## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit changes: `git commit -m 'Add my feature'`
4. Push to branch: `git push origin feature/my-feature`
5. Open a Pull Request

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.
```

## License

```markdown
## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
```

## Common Mistakes

- Missing installation steps or prerequisites
- Outdated examples that no longer compile
- No information about how to run tests
- Assuming reader knows the project context
- Including generated content that becomes stale

## Workflow

1. Start with title, one-line description, and badges
2. Add installation with all prerequisites and commands
3. Write usage examples starting with the simplest case
4. Document configuration variables in a table
5. Add contributing guide and license
6. Review by following the README as a new user would