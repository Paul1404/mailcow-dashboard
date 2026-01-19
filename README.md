# Mailcow Grafana Dashboard

A comprehensive Grafana dashboard for monitoring Mailcow email servers, featuring a VMware VCF-inspired design with dark theme aesthetics.

## Overview

This dashboard provides real-time visibility into your Mailcow infrastructure by visualizing Prometheus metrics from the [mailcow-exporter](https://github.com/Hiren-Khatri/mailcow-exporter). It covers all critical aspects of your mail server including container health, domain quotas, spam filtering, mailbox analytics, and quarantine status.

## Features

- **System Overview**: At-a-glance health status, container count, active domains, total mailboxes, message count, and quarantine items
- **Container Health Grid**: Individual status indicators for all 18 Mailcow containers (Postfix, Dovecot, Rspamd, ClamAV, SOGo, Nginx, MariaDB, Redis, and more)
- **Domain Quota Usage**: Visual representation of storage consumption per domain with threshold indicators
- **Spam Filtering Analytics**: Rspamd action breakdown, ham vs spam classification, scanned messages, and learned patterns
- **Mailbox Analytics**: Top mailboxes by storage usage and detailed mailbox information with last login timestamps
- **Quarantine Monitoring**: Quarantine items by recipient with virus detection status
- **API Performance**: Response time tracking for Mailcow API endpoints
- **Fuzzy Hash Statistics**: Local, Mailcow, and Rspamd.com fuzzy hash counts

## Requirements

- Grafana 10.x or newer
- Prometheus data source configured
- [mailcow-exporter](https://github.com/Hiren-Khatri/mailcow-exporter) running and scraping your Mailcow instance

## Installation

1. Ensure your Prometheus instance is scraping metrics from mailcow-exporter
2. In Grafana, navigate to **Dashboards** > **Import**
3. Click **Upload JSON file** and select `mailcow-dashboard.json`
4. Select your Prometheus data source (default name: `Prometheus`)
5. Click **Import**

## Configuration

### Data Source

The dashboard expects a Prometheus data source with the UID `Prometheus`. If your data source has a different name, you can either:

- Rename your data source to match
- Update the `uid` values in the JSON file before importing

### Variables

The dashboard includes a `host` variable that allows filtering metrics by host label. This is useful when monitoring multiple Mailcow instances from a single Prometheus server.

## Dashboard Sections

| Section | Description |
|---------|-------------|
| System Overview | Key metrics header with health status and counts |
| Container Health | Status grid showing all Mailcow containers |
| Domain Quota Usage | Storage consumption gauges and details table |
| Spam Filtering | Rspamd actions, classifications, and statistics |
| Mailbox Analytics | Top mailboxes and detailed mailbox information |
| Quarantine | Quarantine items with recipient and virus status |
| Fuzzy Hashes | Rspamd fuzzy hash statistics |

## Metrics Used

This dashboard visualizes the following metric families:

- `mailcow_container_running` - Container status
- `mailcow_container_start` - Container start timestamps
- `mailcow_domain_*` - Domain quotas, mailboxes, aliases, messages
- `mailcow_mailbox_*` - Mailbox quotas, messages, last login
- `mailcow_rspamd_*` - Spam filtering actions, classifications, statistics
- `mailcow_quarantine_*` - Quarantine counts and metadata
- `mailcow_api_*` - API response times and status
- `mailcow_exporter_success` - Exporter health status

## Screenshots

The dashboard features a dark theme with:

- Color-coded status indicators (green for healthy, amber for warning, red for critical)
- Gradient bar gauges for quota visualization
- Donut charts for spam filtering breakdowns
- Responsive tables with inline gauges

## License

MIT License - see [LICENSE](LICENSE) for details.

## Contributing

Contributions are welcome. Please open an issue or submit a pull request.

## Related Projects

- [Mailcow](https://mailcow.email/) - The dockerized mailserver suite
- [mailcow-exporter](https://github.com/Hiren-Khatri/mailcow-exporter) - Prometheus exporter for Mailcow
