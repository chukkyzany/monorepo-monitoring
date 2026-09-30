# Monorepo Monitoring

Five CloudWatch dashboards that monitor a monorepo: its CI/CD pipelines,
deployments, code activity, running services (including the MySQL database)
and cost/security.

## Dashboards

| # | Dashboard | Question it answers | Key metrics | Audience |
|---|-----------|--------------------|-------------|----------|
| 1 | CI/CD health | Are builds reliable? | success rate, build duration, queue time | Everyone |
| 2 | Deployments | How fast and safely do we ship? | deploy frequency, lead time, failure rate | Everyone |
| 3 | Code activity | Where is work happening? | PRs per service, review time | Everyone |
| 4 | Runtime | Are services and the database healthy? | latency, traffic, errors, saturation; RDS CPU, connections, storage | Service owners |
| 5 | Cost & security | What does it cost and what's exposed? | spend per service, vulnerabilities | Platform team |

## Repo layout

- `services/api`, `services/web`: sample services
- `infra/`: Terraform (VPC, ALB, EC2, RDS MySQL, alarms)
- `dashboards/`: dashboard definitions
- `docs/`: architecture diagram, screenshots

## Tooling

CloudWatch dashboards and alarms, SNS for email alerts, Terraform for
infrastructure, GitHub Actions for CI/CD.

## Access model (RBAC)

- Viewer: read-only access to dashboards
- Editor: service owners can edit their own service's dashboard
- Admin: platform team, full access including cost and security

## Alerts

Alarms for 5xx errors, high CPU, low database storage and high
database connections, sent to an SNS email topic.

