
<div align="center">
### PHP Developer · Full-Stack Delivery · Cloud Infrastructure · CI/CD · Moodle

**I build, maintain and modernise PHP applications — from legacy PHP 5 systems to modern PHP 8.x environments.**

I enjoy working across the full software delivery process: understanding a monolithic codebase, implementing features, writing automated checks, managing source control, and deploying changes with repeatable pipelines.

`Vanilla PHP` · `PHP 5 → PHP 8.x` · `Laravel` · `Angular` · `Git` · `Bash` · `YAML` · `PHPUnit` · `PHPStan` · `AWS` · `Azure` · `Terraform` · `Moodle`

</div>

---

## 🚀 What I do — and how I do it

| Area | My hands-on approach |
| --- | --- |
| **Vanilla PHP development** | Build framework-independent, reusable functions and services with clear naming, small responsibilities, readable code and predictable error handling. |
| **Legacy modernisation** | Upgrade PHP 5-era applications to PHP 8, working incrementally through dependency constraints, deprecated behaviour, tests and runtime compatibility. |
| **CI/CD automation** | Write Bash scripts and YAML pipelines that install dependencies, run checks, test changes and enforce quality gates before deployment. |
| **Code quality** | Use PHPUnit, PHPStan and code-style checkers to find regressions, catch type issues and keep a consistent standard. |
| **Git workflows** | Work with branches, inspect diffs and logs, cherry-pick targeted changes, revert faulty commits and resolve merges. |
| **WordPress ↔ Moodle APIs** | Connect applications through REST APIs, validate requests/responses and troubleshoot integration issues. |
| **Linux automation and data processing** | Build CSV import scripts and cron jobs, plus Node.js processes that receive and return reports through SFTP. |
| **Moodle customisation** | Extend Moodle through custom plugins, hooks/events, capabilities and scheduled tasks rather than editing core wherever possible. |
| **Monolithic applications** | Navigate tightly coupled code, trace dependencies and introduce safer boundaries so large existing systems can evolve. |
| **Laravel + Angular delivery** | Build and validate changes locally, use Laravel Artisan for backend tasks, then deploy through AWS cluster services and task definitions. |
| **AWS operations** | Work with IAM, certificates, monitoring, CloudWatch metrics and alarms, notifications and email-delivery metrics/settings. |
| **Azure infrastructure as code** | Provision modular Azure infrastructure with Terraform, manage Key Vault secrets and environment configuration, set firewall rules, and debug deployed applications. |

## 🛠️ How I build a CI/CD pipeline

A pipeline should make the same checks run for every pull request, rather than relying on manual steps.

**My approach:**

1. **Define the checks** — Composer validation, coding standards, static analysis and unit tests.
2. **Automate with Bash** — keep build and test commands reproducible locally and in CI.
3. **Orchestrate with YAML** — trigger the checks on pushes and pull requests.
4. **Set quality gates** — block merging when required checks fail.
5. **Deploy deliberately** — add environment-specific secrets, approvals and deployment steps only when required.

**Example: `.github/workflows/php-ci.yml`** (adapt paths/tools to the project):

```yaml
name: PHP CI

on:
  push:
    branches: [develop, main]
  pull_request:
    branches: [develop, main]

jobs:
  quality-and-tests:
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v4

      - name: Set up PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: '8.2'
          tools: composer:v2
          coverage: none

      - name: Validate Composer config
        run: composer validate --strict

      - name: Install locked dependencies
        run: composer install --no-interaction --prefer-dist --no-progress

      - name: Check runtime requirements
        run: composer check-platform-reqs

      - name: Check coding standards
        run: vendor/bin/phpcs

      - name: Static analysis
        run: vendor/bin/phpstan analyse

      - name: Unit tests
        run: vendor/bin/phpunit
```

These commands assume **PHP_CodeSniffer, PHPStan and PHPUnit are installed as development dependencies** and configured for the repository. A production deployment would normally be a separate, protected job.

**Example: `scripts/check.sh`** — the same checks can run locally:

```bash
#!/usr/bin/env bash
set -euo pipefail

composer validate --strict
composer install --no-interaction --prefer-dist
composer check-platform-reqs
vendor/bin/phpcs
vendor/bin/phpstan analyse
vendor/bin/phpunit
```

> **What this demonstrates:** Bash scripting, YAML configuration, dependency management, automated testing and a repeatable delivery process — not just familiarity with tool names.

## ⚙️ Laravel + Angular: from local development to AWS deployment

On a full-stack project using **Laravel (PHP backend)** and **Angular (frontend)**, my workflow takes a feature from local development through tests, versioned deployment and operational verification.

| Stage | What I do | Example |
| --- | --- | --- |
| **Develop locally** | Update Laravel controllers/services, migrations or jobs and Angular components/services; use Git branches to isolate changes. | `php artisan serve` / `ng serve` |
| **Validate** | Use Artisan to check routes and run application tests; build and test the Angular app before committing. | `php artisan test` / `ng test` / `ng build` |
| **Build & package** | Install locked dependencies and build deployable application/container artifacts via CI. | `composer install`, `npm ci` |
| **Deploy to AWS** | Publish a new application image/release, update the service task definition and roll out the new revision to the cluster. | ECS task definition + service update (illustrative) |
| **Monitor & recover** | Watch service health, container logs and CloudWatch alarms; if the release fails, deploy a previously known-good task definition. | AWS console / CLI |

> **Important distinction:** `php artisan` runs Laravel commands such as migrations, jobs and tests. Angular uses the Angular CLI (`ng`) for frontend development, builds and tests.

**A typical local verification sequence:**

```bash
# Laravel backend
composer install
php artisan migrate:status
php artisan test

# Angular frontend (run in its project directory)
npm ci
npx ng test --watch=false
npx ng build --configuration production
```

**How I manage releases and rollback on AWS ECS:**

1. Package the tested version and publish the container image to the image registry.
2. Register a **new ECS task definition revision** that points to that image.
3. Update the ECS service in the target cluster to use that revision.
4. Confirm that tasks are healthy and inspect application logs and service events.
5. If a regression is found, redeploy a **previously working task definition revision** and verify service health. Database changes may require a separate rollback strategy.

```bash
# Example only — substitute your actual names and tested task definition ARN
aws ecs update-service \
  --cluster "<cluster-name>" \
  --service "<service-name>" \
  --task-definition "<task-definition-family>:<revision>"

# Observe the rollout
aws ecs describe-services \
  --cluster "<cluster-name>" \
  --services "<service-name>"
```

This describes the release workflow rather than asserting that each project uses the same CI runner or deployment tooling.

## ☁️ AWS: deploying, monitoring and operating applications

I work across deployment and day-to-day operational concerns, connecting infrastructure configuration to how applications actually behave in production.

| AWS capability | How I apply it |
| --- | --- |
| **Clusters & tasks** | Check ECS services, task health and deployments; introduce new task revisions for application releases. |
| **Certificates** | Configure and check application TLS certificates, including AWS Certificate Manager (ACM) where applicable. |
| **Monitoring** | Investigate logs, metrics and failures through CloudWatch and service events. |
| **Cloud metrics & alarms** | Set up relevant metrics/alarms and notification thresholds to surface service issues. |
| **IAM users & permissions** | Work with IAM users, roles and policies, using least-privilege access for people and workloads. |
| **Email metrics & settings** | Review email delivery settings and sending metrics with Amazon SES where used. |
| **Notifications** | Configure operational notifications, for example CloudWatch alarms routed through Amazon SNS. |

**Practical example — diagnosing a failed release:** inspect ECS deployment events, review the task/container logs, correlate failure timing with CloudWatch metrics, then either fix and deploy a new revision or restore a tested revision.

## 🏗️ Azure + Terraform: provisioning infrastructure from reusable modules

I have set up project infrastructure in **Microsoft Azure using Terraform**, separating reusable infrastructure modules from application-specific configuration.

**How I structure the project:**

```text
infrastructure/
├── modules/
│   ├── app-service/
│   ├── database/
│   ├── key-vault/
│   ├── networking/
│   └── monitoring/
└── applications/
    └── example-app/
        ├── main.tf
        ├── variables.tf
        ├── outputs.tf
        └── terraform.tfvars.example
```

This is an **illustrative structure** showing my modular approach — not a copy of an employer's infrastructure.

**Example: calling an App Service module from an application configuration:**

```hcl
module "app_service" {
  source              = "../../modules/app-service"
  app_name            = var.app_name
  resource_group_name = var.resource_group_name
  location            = var.location
}

module "database" {
  source              = "../../modules/database"
  resource_group_name = var.resource_group_name
  location            = var.location
}
```

**My end-to-end workflow:**

1. **Structure the Terraform code** into reusable modules, with an application folder that calls only the modules needed for that project.
2. **Provision hosting** using Azure App Service and configure application settings required by the deployment.
3. **Set up database connectivity** for the project's chosen engine — Azure Database for MySQL or Azure SQL Database / SQL Server, depending on application requirements.
4. **Handle secrets** using Azure Key Vault and references/managed identity where supported. Keep non-secret environment-specific configuration in Azure App Service settings or approved deployment variables, rather than hard-coding values.
5. **Set network rules** and check database firewall, networking, access restrictions and connection settings in the Azure portal.
6. **Validate and deploy** using `terraform fmt`, `terraform validate`, `terraform plan` and a reviewed `terraform apply`.
7. **Debug live issues** with Azure App Service SSH/console, logs and configuration inspection, then reproduce and fix problems with session handling and persistent storage.

```bash
terraform fmt -check -recursive
terraform init
terraform validate
terraform plan -var-file="dev.tfvars"
# Run apply only after checking the plan and selecting the correct environment
terraform apply -var-file="dev.tfvars"
```

**Real troubleshooting theme:** during a deployment, investigate why an app works locally but fails in Azure. I have used the Azure application console/SSH and settings to identify **storage and session configuration problems**, make corrections, and verify the application after deployment.

> **Security practice:** never commit real `.tfvars` values containing secrets, credentials, `.env` files or Terraform state. Use identity-based access and secure secret management; be aware that Terraform state can contain sensitive values.

## 🐘 How I modernise PHP applications

I work with PHP 8.0–8.5 concepts and legacy migration paths, including upgrades from PHP 5-era applications. My focus is on **maintaining behaviour while reducing upgrade risk**.

**Typical upgrade process:**

1. **Audit the application:** identify the PHP version, Composer constraints, extensions, framework/plugin versions and runtime environment.
2. **Find incompatibilities:** inspect deprecations, removed functions, stricter typing, dynamic properties and dependency conflicts.
3. **Introduce safety checks:** add or update PHPUnit tests around critical business logic.
4. **Improve code quality:** run PHPStan and a coding-standard checker, fixing issues in manageable batches.
5. **Upgrade incrementally:** update the runtime and dependencies in staging, then verify CLI jobs, web requests and integrations.
6. **Deploy with rollback:** release through version control and CI/CD, with monitoring and a documented rollback path.

**Example commands I use during an upgrade:**

```bash
php -v
composer validate
composer prohibits php 8.2 -t
composer check-platform-reqs
vendor/bin/phpunit
vendor/bin/phpstan analyse
vendor/bin/phpcs
```

### PHP functions and scheduled jobs

I use PHP for reusable business logic, integration points and command-line/scheduled jobs. A good job should provide meaningful exit codes and logs so problems can be surfaced by the scheduler or CI.

```php
<?php

declare(strict_types=1);

function formatJobResult(int $processed): string
{
    return sprintf('Processed %d records', $processed);
}

try {
    // Call application services here rather than placing all logic in a CLI script.
    fwrite(STDOUT, formatJobResult(0) . PHP_EOL);
    exit(0);
} catch (Throwable $exception) {
    error_log($exception->getMessage());
    exit(1);
}
```

*Illustrative example — replace with a sanitised real-world use case from your work.*

## ♻️ Vanilla PHP: reusable, readable functionality

I work with **vanilla PHP**, not just frameworks. I aim for code that is easy to understand, test and reuse: small functions with one responsibility, meaningful names, typed inputs/outputs where supported, and application-specific behaviour separated from input/output handling.

For example, when processing an imported CSV, I can put validation in a reusable function rather than repeating it inside an upload handler or cron job:

```php
<?php

declare(strict_types=1);

function normaliseEmail(string $email): ?string
{
    $value = strtolower(trim($email));

    return filter_var($value, FILTER_VALIDATE_EMAIL) ? $value : null;
}
```

**How I apply this:** keep CSV parsing, validation, database updates and logging in separate functions or classes so the same logic can be called from a web request, CLI script or scheduled job. Add PHPUnit tests around shared behaviour and use PHPStan / PHP_CodeSniffer to catch problems early.

*Simplified illustrative example; not a copy of private project code.*

## 🔗 WordPress ↔ Moodle: integration through APIs

On a current project, I work on **communication between WordPress and Moodle**. Rather than treating them as isolated platforms, I work with the request/response flow and integration points connecting the applications.

**How I approach the integration:**

1. Establish which application is the caller and which owns the data or operation.
2. Use the available API endpoints and the appropriate authentication method.
3. Validate payloads, required fields, HTTP statuses and error responses.
4. Test requests with **Postman** or repeatable automated checks.
5. Capture useful diagnostics without logging tokens, passwords or personal information.
6. Verify the workflow across both systems after changes or PHP upgrades.

**Example REST response check** (illustrative endpoint and payload):

```bash
curl --fail-with-body --silent --show-error \
  -H 'Accept: application/json' \
  'https://example.invalid/api/status'
```

In real integrations, secrets belong in protected application configuration rather than command history or source control.

## 🐧 Linux automation: CSV imports, cron and scheduled jobs

I use Linux-hosted scripts to process uploaded CSV files and run recurring application tasks. The goal is **repeatability, validation and visibility**, not just scheduling a script.

**Typical workflow:** receive a CSV → validate headings and records → process records with reusable PHP functions → record successes/errors → return an appropriate exit code → investigate logs when the scheduler reports failure.

**Example crontab entry** (illustrative paths):

```cron
15 2 * * * /usr/bin/php /srv/app/bin/import-csv.php >> /var/log/app/import-csv.log 2>&1
```

I consider idempotency (safe reruns), file permissions, duplicate records and what should happen after partial failure. I also keep secrets out of scripts and logs.

## 📦 Node.js: SFTP report processing and delivery

I have worked with **Node.js to build a report processor** that retrieves an incoming file over SFTP, processes its contents and sends a generated report back to the user through SFTP.

```text
SFTP source
    ↓ download incoming file
Node.js report processor
    ↓ validate → transform → generate report
SFTP destination
    ↓ upload completed report
Logs / error handling / retry or investigation
```

**How I approach this:**

1. Connect securely using credentials or keys provided through environment configuration.
2. Identify and download the expected input file.
3. Validate file structure and process its records.
4. Generate an output report with a predictable name and format.
5. Upload it to the required SFTP location.
6. Log outcomes and handle missing files, failed transfers or invalid data so the process can be diagnosed safely.

*This describes the workflow; implementation details and client data are deliberately omitted.*

## 🌿 How I use Git to deliver and troubleshoot changes

I use Git as both a collaboration tool and a way to investigate what changed when something goes wrong.

```bash
# Understand the current state
git status
git log --oneline --graph --decorate -15
git diff

# Identify a change and inspect it
git show <commit-sha>

# Undo a published change safely with a new commit
git revert <commit-sha>

# Apply a specific fix to another branch
git cherry-pick <commit-sha>

# Compare release branches
git diff main...develop
```

**My approach:** make small, reviewable commits; use pull requests and automated checks; favour `git revert` over rewriting shared branch history; and use logs/diffs to trace regressions. Git shows **changes and commit history**; runtime errors are investigated via application logs and test output.

## 🎓 How I extend Moodle

I work with the Moodle platform and its plugin architecture to add features to existing learning environments.

**My typical process:**

1. Identify the extension point: a **local plugin**, block, activity module or another supported plugin type.
2. Implement PHP functionality using Moodle APIs and coding conventions.
3. Define permissions/capabilities, configuration, database changes or scheduled tasks as required.
4. Connect functionality through Moodle's events, hooks and external APIs where suitable.
5. Test upgrades and compatibility in a non-production Moodle environment.
6. Package and deploy the plugin in a maintainable way, avoiding changes to Moodle core where possible.

**Portfolio idea:** add a public, sanitised example plugin that demonstrates a settings page, capability checks and a scheduled task. Avoid publishing proprietary Moodle code or learner data.

## 🧩 Working with monolithic workloads

Much of real-world software engineering involves improving existing systems safely. For a monolithic PHP application, I focus on:

- Tracing request paths and dependencies before changing behaviour.
- Isolating business logic into testable functions or services where practical.
- Keeping backwards compatibility visible through regression tests.
- Breaking upgrades into smaller deployable changes.
- Improving observability with clear logs, failed-job reporting and reproducible error cases.

## 🤝 Delivery, quality, security and leadership

Alongside the code and infrastructure work above, I have experience with the people and delivery processes that help software teams ship reliable changes. I group these by **how they contribute to delivery**, rather than using a long list of unconnected keywords.

| Competency | How I apply it |
| --- | --- |
| **Leadership, coaching and mentoring** | Support developers through knowledge sharing, code reviews, feedback and practical problem-solving. |
| **Recruitment and onboarding** | Help colleagues understand the codebase, development environment, team practices and expectations. |
| **Agile / Scrum delivery** | Work with sprint planning, estimation, prioritisation and iterative releases. |
| **Requirements and risk assessment** | Translate requests into achievable changes; identify dependencies, edge cases and rollout risks. |
| **API testing / Postman** | Verify REST requests, responses, authentication behaviour and negative/error cases. |
| **Test design and execution** | Carry out manual, regression and exploratory testing; support UAT and investigate defects. |
| **Root cause analysis** | Reproduce errors, inspect logs and Git history, isolate the failing component and verify the fix. |
| **Secure development / ISO 27001 awareness** | Apply access controls, appropriate handling of secrets and secure release practices in line with organisational policies. |
| **Accessibility / WCAG** | Consider and test accessibility requirements during UI changes. |
| **Stakeholder communication** | Explain risks, progress and technical issues in terms that help others make decisions. |
| **Process improvement and documentation** | Document repeatable workflows, simplify manual tasks and improve development/onboarding guidance. |
| **SQL / MySQL** | Investigate data issues and work with queries, application persistence and database configuration. |
| **Pull requests and code reviews** | Review changes for readability, correctness, test coverage and deployment impact. |

> For a public portfolio, keep only responsibilities you have **actually carried out**. In particular, distinguish *ISO 27001-aware practices* from formal auditor/certification experience, and *supporting recruitment* from owning hiring decisions.

## 📌 Featured work / case studies

> Replace these with **real repositories, screenshots, redacted pipeline runs or short technical write-ups**. The examples above are templates, not claims that a specific repository is publicly available.

| Case study | What to show
| --- | --- | --- |
| **PHP legacy upgrade** | Before/after dependency constraints, compatibility fixes, PHPUnit test coverage, upgrade plan|
| **CI/CD in Bash + YAML** | Workflow, reusable Bash script, quality gates, example failed and passing checks |
| **Moodle custom plugin** | Plugin structure, capabilities, events/hooks, scheduled tasks and upgrade steps |
| **Monolith maintenance** | A carefully anonymised refactor, regression test and rollback strategy |
| **Laravel + Angular → AWS** | Local commands, validation, ECS task rollout and restoring a prior revision |
| **Azure Terraform deployment** | Modules, App Service, database, Key Vault, firewall configuration and troubleshooting |
| **WordPress ↔ Moodle integration** | Redacted request/response flow, validation and API troubleshooting |
| **Linux CSV + cron processing** | Input validation, scheduled execution, logging and recovery behaviour |
| **Node.js SFTP report processor** | File-transfer workflow, processing, outbound report and error handling |

## 🔧 Tools and technologies

**Languages & frameworks:** Vanilla PHP (PHP 5-to-8 modernisation; PHP 8.x), Laravel, Angular, JavaScript/TypeScript, Node.js, Bash, YAML, SQL  
**Testing & quality:** PHPUnit, PHPStan, PHP_CodeSniffer, Composer, Angular CLI  
**Cloud & infrastructure:** AWS ECS, CloudWatch, IAM, ACM, SES, SNS; Azure App Service, Key Vault, MySQL, Azure SQL, Terraform modules  
**Platform & delivery:** WordPress, Moodle, REST APIs, Postman, Linux, cron, CSV processing, SFTP, Git, GitHub, CI/CD, Docker, release management  
**Engineering practices:** debugging, monitoring, code review, dependency upgrades, automation, monolith modernisation, rollback planning, Agile/Scrum, mentoring, test design, UAT, risk assessment, security awareness and accessibility testing

---

<div align="center">

### 📫 Connect

[GitHub](https://github.com/Sparker1991) · [LinkedIn](https://www.linkedin.com/in/scott-parker-bsc-62252625)

*Building dependable software and making complex upgrades easier to maintain.*

</div>
