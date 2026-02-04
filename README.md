# RevenueCat Skill

An [AgentSkills](https://agentskills.io)-compatible skill that enables AI agents to query RevenueCat metrics, customer data, and documentation. This skill provides AI tools with the ability to interact with the RevenueCat REST API v2 and search RevenueCat documentation.

## Features

- **API Integration**: Query RevenueCat REST API v2 endpoints for metrics, customers, subscriptions, and more
- **Comprehensive Documentation**: Local reference files covering all major RevenueCat API domains
- **Progressive Disclosure**: Structured documentation that loads only what's needed to optimize context usage
- **Bash Script Wrapper**: Simple `rc-api` script for making authenticated API calls

## Prerequisites

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
3. OpenClaw will automatically detect and load the skill from the `revenuecat/` directory

### For Other AgentSkills-Compatible Tools

1. Clone this repository
2. Point your AI tool to the `revenuecat/` directory
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

## API Script Usage

The included `rc-api` script simplifies API calls:

```bash
# List projects (typically first call to get project ID)
./revenuecat/scripts/rc-api /projects

# Get customers for a project
./revenuecat/scripts/rc-api /projects/{project_id}/customers

# Get a specific customer
./revenuecat/scripts/rc-api /projects/{project_id}/customers/{customer_id}
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

## License

This skill is licensed under the terms specified in [LICENSE](LICENSE).

## Resources

- [RevenueCat Documentation](https://www.revenuecat.com/docs)
- [RevenueCat REST API v2 Reference](https://www.revenuecat.com/reference)
- [AgentSkills Specification](https://agentskills.io/specification)

## Support

For issues specific to this skill:

- Open an issue in this repository

For RevenueCat API questions:

- Visit the [RevenueCat Help Center](https://support.revenuecat.com)
- Check the [RevenueCat Documentation](https://www.revenuecat.com/docs)
