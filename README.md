# RevenueCat Intelligence Skill

An [AgentSkills](https://agentskills.io)-compatible skill that enables AI agents to query RevenueCat metrics, customer data, and documentation. This skill provides AI tools with the ability to interact with the RevenueCat REST API v2 and search RevenueCat documentation.

## Features

- **API Integration**: Query RevenueCat REST API v2 endpoints for metrics, customers, subscriptions, and more
- **Comprehensive Documentation**: Local reference files covering all major RevenueCat API domains
- **Progressive Disclosure**: Structured documentation that loads only what's needed to optimize context usage
- **Bash Script Wrapper**: Simple `rc-api` script for making authenticated API calls

## Prerequisites

- `curl` command-line tool
- `jq` JSON processor
- A RevenueCat v2 secret API key (set as `RC_API_KEY` environment variable)

## Installation

### For Claude Code

1. Clone this repository to your local machine
2. Set your RevenueCat API key:
   ```bash
   export RC_API_KEY="your_api_key_here"
   ```
3. The skill will be automatically discovered if placed in a standard skills directory

### For OpenClaw

1. Clone this repository
2. Configure the `RC_API_KEY` environment variable in your OpenClaw settings
3. OpenClaw will automatically detect and load the skill from the `skill/` directory

### For Other AgentSkills-Compatible Tools

1. Clone this repository
2. Point your AI tool to the `skill/` directory
3. Ensure the `RC_API_KEY` environment variable is set in your environment

## Usage

Once installed, AI agents can automatically invoke this skill when you ask questions about:

- RevenueCat metrics and analytics (MRR, churn, revenue)
- Customer data and subscriptions
- Products, offerings, and entitlements
- RevenueCat documentation and API usage

### Example Queries

```
"What's our current MRR?"
"Show me the most recent customers"
"How do I create a product in RevenueCat?"
"What are the rate limits for the RevenueCat API?"
```

## Skill Structure

```
skill/
├── SKILL.md                      # Main skill definition (AgentSkills format)
├── scripts/
│   └── rc-api                    # Bash wrapper for RevenueCat API calls
└── references/                   # Domain-specific API documentation
    ├── api-v2.md                 # Core API concepts (auth, pagination, expandables)
    ├── customers.md              # Customer CRUD, attributes, subscriptions
    ├── subscriptions.md          # Subscription management
    ├── products.md               # Product operations
    ├── offerings.md              # Offerings and packages
    ├── entitlements.md           # Entitlement configuration
    ├── purchases.md              # Purchase history and refunds
    ├── projects.md               # Project and app configuration
    ├── metrics.md                # Analytics and charts
    ├── paywalls.md               # Paywall creation
    ├── integrations.md           # Third-party integrations
    ├── virtual-currencies.md     # Virtual currency operations
    ├── error-handling.md         # Error codes and handling
    └── rate-limits.md            # API rate limit information
```

### Design Philosophy

The skill follows the AgentSkills principle of **progressive disclosure**:

1. **Metadata** (~100 tokens): The skill name and description help agents determine when to use it
2. **Core Instructions** (~1000 tokens): The main `SKILL.md` provides setup and navigation
3. **Reference Files** (loaded on demand): Detailed documentation is loaded only when needed for specific tasks

This structure minimizes context usage while providing comprehensive coverage of the RevenueCat API.

## API Script Usage

The included `rc-api` script simplifies API calls:

```bash
# List projects (typically first call to get project ID)
./skill/scripts/rc-api /projects

# Get customers for a project
./skill/scripts/rc-api /projects/{project_id}/customers

# Get a specific customer
./skill/scripts/rc-api /projects/{project_id}/customers/{customer_id}
```

The script automatically:

- Validates that `RC_API_KEY` is set
- Sets proper authentication headers
- Points to the correct API base URL (`https://api.revenuecat.com/v2`)

## Documentation Coverage

The skill includes comprehensive local documentation for:

- **Core Concepts**: Authentication, pagination, error handling, rate limits
- **Customer Management**: CRUD operations, attributes, aliases, entitlements
- **Subscription Operations**: Listing, cancellation, refunds, management URLs
- **Product Catalog**: Products, offerings, packages, entitlements
- **Analytics**: Overview metrics, charts, and chart options
- **Advanced Features**: Paywalls, integrations, virtual currencies

## Remote Documentation

In addition to local references, agents can access live RevenueCat documentation:

- Main docs: https://www.revenuecat.com/docs
- LLM-optimized index: https://www.revenuecat.com/docs/llms.txt
- Markdown versions: Add `.md` to any documentation URL

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Adding New Reference Files

When adding new reference documentation:

1. Keep files focused on a single domain
2. Use clear, descriptive filenames
3. Update the reference table in `revenuecat/SKILL.md`
4. Follow the existing format with clear examples

### Updating the API Script

When modifying the `rc-api` script:

1. Maintain backward compatibility
2. Keep error messages clear and actionable
3. Test with various API endpoints

## About AgentSkills

AgentSkills is an open format for packaging instructions, scripts, and resources that AI agents can discover and use. Skills enable:

- **Portability**: Write once, use across multiple AI tools
- **Progressive Loading**: Load only what's needed to optimize context
- **Domain Expertise**: Package specialized knowledge for reuse

Learn more at [agentskills.io](https://agentskills.io)

## License

This skill is licensed under the terms specified in [LICENSE](LICENSE).

## Resources

- [RevenueCat Documentation](https://www.revenuecat.com/docs)
- [RevenueCat REST API v2 Reference](https://www.revenuecat.com/reference)
- [AgentSkills Specification](https://agentskills.io/specification)
- [AgentSkills GitHub](https://github.com/agentskills/agentskills)

## Support

For issues specific to this skill:

- Open an issue in this repository

For RevenueCat API questions:

- Visit the [RevenueCat Help Center](https://support.revenuecat.com)
- Check the [RevenueCat Documentation](https://www.revenuecat.com/docs)

For AgentSkills format questions:

- See the [AgentSkills Specification](https://agentskills.io/specification)
- Visit the [AgentSkills GitHub](https://github.com/agentskills/agentskills)
