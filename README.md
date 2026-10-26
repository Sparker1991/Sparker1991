
# 👋 PHP & Full-Stack Developer | Cloud Engineering | DevOps

### PHP 5–8.5 • Laravel • Angular • AWS • Azure • Terraform • CI/CD • Moodle

I am a PHP and full-stack developer with hands-on experience in maintaining, modernising and deploying web applications.

My experience covers legacy monolithic applications, modern PHP development, cloud infrastructure, automated testing and deployment pipelines.

I focus on understanding how applications work from end to end — from writing PHP functions and fixing bugs through to configuring infrastructure, diagnosing production issues and deploying reliable releases.

---

## 🛠️ Technical Skills

| Area | Technologies |
|---|---|
| Backend | PHP 5–8.x, Laravel, Composer, PHP Artisan |
| Frontend | Angular, JavaScript, HTML, CSS |
| Databases | MySQL, SQL Server, SQL |
| Testing | PHPUnit, PHPStan, PHP_CodeSniffer, code quality checks |
| CI/CD | GitHub Actions, YAML, Bash, automated pipelines |
| AWS | ECS, clusters, task definitions, IAM, CloudWatch, SES, ACM |
| Azure | App Service, Terraform, Key Vault, databases, networking |
| Infrastructure | Terraform, reusable modules, environment configuration |
| Version Control | Git, GitHub, branching, merging, reverting, cherry-picking |
| CMS & Learning | Moodle, custom Moodle plugins, WordPress |
| Architecture | Monolithic applications, legacy systems, application modernisation |

---

# 🚀 How I Build, Test and Deploy Applications

I use Git, Bash, YAML and CI/CD pipelines to automate the process of building, validating and deploying application changes.

My approach typically involves:

1. Developing and testing changes locally.
2. Creating a dedicated Git branch.
3. Implementing PHP or frontend functionality.
4. Running automated tests and static analysis.
5. Committing and reviewing changes.
6. Running a CI/CD pipeline.
7. Building and deploying the application.
8. Monitoring the deployed environment.
9. Investigating failures and rolling back when necessary.

## ⚙️ Building CI/CD Pipelines with YAML and Bash

I use YAML to define pipeline stages and Bash scripts to execute build, testing and deployment tasks.

### Example GitHub Actions pipeline

```yaml
name: PHP CI Pipeline

on:
  push:
    branches: [develop, main]
  pull_request:

jobs:
  php-tests:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: '8.2'
          coverage: none
          tools: composer:v2

      - name: Install dependencies
        run: composer install --no-interaction --prefer-dist

      - name: Run PHPUnit
        run: vendor/bin/phpunit

      - name: Run PHPStan
        run: vendor/bin/phpstan analyse

      - name: Check coding standards
        run: vendor/bin/phpcs
```

This example shows how I structure automated PHP quality checks. Real deployment workflows also require environment-specific configuration, credentials and permissions.

### Using Bash for automated tasks

```bash
#!/usr/bin/env bash
set -euo pipefail

echo "Checking PHP version..."
php -v

echo "Installing Composer dependencies..."
composer install --no-interaction --prefer-dist

echo "Running PHPUnit tests..."
vendor/bin/phpunit

echo "Running PHPStan..."
vendor/bin/phpstan analyse

echo "Build checks completed successfully."
```

Using `set -euo pipefail` allows a Bash script to stop when a command fails, a variable is undefined or a pipeline fails.

I use scripts like these to make repeated development and deployment tasks more consistent.

---

# 🐘 PHP Development and Legacy Modernisation

## Upgrading applications from PHP 5 to PHP 8

I have experience upgrading older PHP applications to modern PHP versions while identifying compatibility issues and preserving existing functionality.

This can involve:

- Reviewing legacy functions and unsupported syntax.
- Identifying deprecated and removed PHP functionality.
- Updating Composer dependencies.
- Reviewing application frameworks and libraries.
- Replacing outdated database functionality.
- Correcting errors caused by stricter PHP behaviour.
- Updating PHPUnit and static analysis tooling.
- Testing application behaviour before deployment.
- Checking logs for warnings, deprecations and runtime errors.

### Composer dependency investigation

```bash
php -v

composer --version

composer check-platform-reqs

composer outdated

composer prohibits php 8.2 -t
```

These commands help determine whether application dependencies and the running environment support a target PHP version.

### PHP 8.x quality and compatibility

My work involves maintaining and updating applications across PHP 8 releases, including compatibility planning towards PHP 8.5.

Areas I work with include:

- Type declarations and return types.
- Exceptions and error handling.
- Nullable types and stricter function signatures.
- Object-oriented programming.
- Dependency management with Composer.
- Modernising deprecated PHP features.
- CLI scripts and scheduled jobs.
- Automated testing and static analysis.

## Creating PHP functions and scheduled jobs

I use PHP to implement reusable business logic, integrations, command-line utilities and scheduled background tasks.

A reliable scheduled job should provide meaningful logging, clear error handling and appropriate exit codes.

### Example PHP CLI job

```php
<?php

declare(strict_types=1);

function processPendingJobs(): void
{
    // Retrieve and process pending jobs.
    // Replace with application-specific logic.
}

try {
    processPendingJobs();

    echo "Jobs completed successfully.\n";
    exit(0);

} catch (Throwable $exception) {
    error_log(
        "Scheduled job failed: " .
        $exception->getMessage()
    );

    exit(1);
}
```

This structure allows a scheduler or CI system to detect job failures using the process exit code.

---

# 🧪 Testing and Code Quality

I use automated testing and code quality tools to improve reliability during development and PHP upgrades.

## PHPUnit

I use PHPUnit to test individual functions, classes and application behaviour.

```php
<?php

use PHPUnit\Framework\TestCase;

final class CalculatorTest extends TestCase
{
    public function testAddition(): void
    {
        $result = 10 + 5;

        $this->assertSame(15, $result);
    }
}
```

Run tests with:

```bash
vendor/bin/phpunit
```

## PHPStan

I use PHPStan to identify potential defects without executing application code.

```bash
vendor/bin/phpstan analyse
```

This can highlight incorrect types, potentially invalid method calls and other issues before deployment.

## PHP_CodeSniffer

I use coding standard checks to identify inconsistent formatting and violations of configured coding standards.

```bash
vendor/bin/phpcs
```

These tools can also run automatically as part of CI/CD pipelines, preventing changes from progressing when important checks fail.

---

# 🅰️ Laravel and Angular Application Development

I have worked on a project combining a Laravel PHP backend with an Angular frontend, including local development, testing and deployment to AWS.

## Local development workflow

### Laravel backend

```bash
composer install

php artisan key:generate

php artisan migrate

php artisan serve
```

I use Laravel Artisan commands for application configuration, migrations, testing and operational tasks.

Commands are selected according to the needs and configuration of each project.

### Angular frontend

```bash
npm ci

ng test

ng build
```

I use Angular tooling to install dependencies, test frontend functionality and create production-ready builds.

## Deployment to AWS ECS

My experience includes deploying application changes using AWS clusters, services and task definitions.

A deployment workflow can include:

1. Testing Laravel and Angular changes locally.
2. Committing changes through Git.
3. Running the appropriate pipeline checks.
4. Building application artefacts and container images.
5. Publishing versioned container images.
6. Creating a new ECS task definition revision.
7. Updating the ECS service to use the new revision.
8. Monitoring task health and application logs.
9. Investigating failed deployments and rolling back if required.

### Example AWS ECS deployment command

```bash
aws ecs update-service \
  --cluster application-cluster \
  --service application-service \
  --task-definition application-task:25
```

The cluster, service and revision shown are illustrative.

## Rolling back application releases

If a deployment introduces an issue, I can investigate the affected release and redeploy a previously working ECS task definition.

For example:

```bash
aws ecs update-service \
  --cluster application-cluster \
  --service application-service \
  --task-definition application-task:24
```

This updates the ECS service to use a previous task definition revision.

I also use ECS service events, CloudWatch logs and application health checks to investigate failed releases.

A rollback needs to account for database changes and other infrastructure dependencies, rather than assuming that every earlier application version is automatically compatible.

---

# ☁️ AWS Cloud Engineering

My AWS experience includes application hosting, deployment, security, monitoring and troubleshooting.

## ECS clusters and task management

- Managing ECS clusters and services.
- Working with container task definitions.
- Deploying new task revisions.
- Monitoring service deployment status.
- Investigating stopped and unhealthy tasks.
- Restoring previous application versions when required.

## AWS Certificate Manager

- Working with SSL/TLS certificates.
- Configuring certificate usage for HTTPS.
- Investigating certificate configuration and validation.

## Identity and Access Management (IAM)

- Managing IAM users and permissions.
- Working with policies, roles and access requirements.
- Reviewing application and deployment access.
- Following least-privilege principles.

## CloudWatch monitoring and metrics

- Reviewing application and infrastructure logs.
- Configuring CloudWatch metrics and alarms.
- Monitoring application health and service behaviour.
- Identifying errors and operational issues.
- Creating notifications for conditions requiring attention.

## Email services and metrics

- Working with AWS email delivery settings.
- Investigating delivery and sending configuration.
- Reviewing email-related metrics.
- Monitoring sending failures and delivery behaviour.

## Notifications

- Configuring operational alerts.
- Connecting monitoring events to notifications.
- Investigating issues raised by alarms.
- Using monitoring information during deployment troubleshooting.

---

# 🌐 Azure Infrastructure with Terraform

I have experience setting up Azure application infrastructure using Terraform, including organising reusable modules and configuring application environments.

## Terraform project structure

I structure Terraform projects by separating reusable infrastructure components from environment-specific application configuration.

Example:

```text
terraform/
├── modules/
│   ├── app-service/
│   ├── mysql/
│   ├── sql-server/
│   ├── key-vault/
│   ├── networking/
│   └── monitoring/
│
└── applications/
    └── example-app/
        ├── main.tf
        ├── variables.tf
        ├── outputs.tf
        └── terraform.tfvars
```

This approach allows infrastructure to be maintained consistently without duplicating large amounts of Terraform configuration.

## Calling reusable Terraform modules

### Example application configuration

```hcl
module "app_service" {
  source = "../../modules/app-service"

  app_name            = var.app_name
  resource_group_name = var.resource_group_name
  location            = var.location
}
```

A database module can be called in the same way:

```hcl
module "mysql" {
  source = "../../modules/mysql"

  resource_group_name = var.resource_group_name
  location            = var.location
}
```

The examples demonstrate module composition. Module input variables must match the definitions in the actual project.

## Provisioning Azure services

My infrastructure work includes:

- Azure App Service configuration.
- MySQL database provisioning.
- Azure SQL Server and SQL Database configuration.
- Resource groups and application resources.
- Networking and firewall rules.
- Application configuration settings.
- Monitoring and infrastructure troubleshooting.

## Azure Key Vault and secrets

I use Azure Key Vault to manage sensitive application configuration, such as database credentials and service secrets.

I also work with environment variables and Terraform input variables to configure environments without hardcoding values directly into infrastructure code.

### Example Terraform input

```hcl
variable "app_name" {
  type = string
}

variable "environment" {
  type = string
}
```

For production environments, secrets should be supplied securely and referenced through Key Vault or appropriate managed identity mechanisms.

Sensitive values should not be committed to Git or unnecessarily written into Terraform state.

## Terraform deployment workflow

```bash
terraform init

terraform fmt -check

terraform validate

terraform plan

terraform apply
```

I use these commands to initialise infrastructure, validate configuration, review proposed changes and provision resources.

## Azure firewall and configuration troubleshooting

I have worked with Azure networking and application settings to identify connectivity and configuration problems.

This includes:

- Reviewing firewall rules and allowed connections.
- Checking database connectivity.
- Validating App Service configuration.
- Investigating environment variables.
- Checking application logs and runtime settings.

## Debugging live Azure applications

I have used Azure's SSH and diagnostic capabilities to troubleshoot issues preventing an application from operating correctly.

My troubleshooting experience includes identifying and resolving problems involving:

- Application storage configuration.
- Session storage and persistence.
- Incorrect environment settings.
- Filesystem permissions.
- Application startup and runtime errors.
- Database connectivity.

I use application logs, configuration inspection and controlled testing to identify the cause of issues before making corrections.

---

# 🌿 Git Version Control and Troubleshooting

I use Git for collaborative development, release management and investigating changes that introduce application issues.

## Checking repository state

```bash
git status

git log --oneline --graph --decorate -15

git diff
```

## Investigating changes

```bash
git show <commit-sha>

git diff main..develop

git blame path/to/file.php
```

These commands help identify what changed, compare branches and investigate the history of a particular file.

## Reverting a problematic change

```bash
git revert <commit-sha>
```

This creates a new commit that reverses an earlier change without rewriting published branch history.

## Cherry-picking a specific fix

```bash
git cherry-pick <commit-sha>
```

I use cherry-picking when a particular change needs to be applied to another branch without merging unrelated commits.

## Merging branch history

```bash
git checkout develop

git merge --no-ff <commit-sha>
```

This can create a merge commit incorporating the history reachable from the selected commit.

## Troubleshooting workflow

When investigating a regression, I typically:

1. Reproduce the reported error.
2. Review the application and server logs.
3. Inspect recent Git commits.
4. Compare affected branches or releases.
5. Identify the relevant change.
6. Test a fix locally.
7. Run automated checks.
8. Deploy the correction.
9. Monitor the application after release.

---

# 🎓 Moodle Development and Custom Plugins

I have experience working with Moodle and extending its functionality through custom development.

This includes understanding how Moodle plugins interact with the wider platform and how custom functionality can be introduced while maintaining compatibility.

## Working with Moodle

- Understanding the Moodle application structure.
- Developing and adapting custom plugins.
- Working with Moodle PHP APIs.
- Extending application functionality.
- Integrating custom business requirements.
- Troubleshooting plugin compatibility.
- Testing changes after Moodle and PHP upgrades.

## Example Moodle local plugin structure

```text
local/customfeature/
├── db/
│   ├── access.php
│   └── tasks.php
├── classes/
│   └── task/
│       └── example_task.php
├── lang/
│   └── en/
│       └── local_customfeature.php
├── settings.php
└── version.php
```

This demonstrates a typical layout for a Moodle local plugin.

### Example scheduled task definition

```php
<?php

defined('MOODLE_INTERNAL') || die();

$tasks = [
    [
        'classname' =>
            '\local_customfeature\task\example_task',
        'blocking' => 0,
        'minute' => '0',
        'hour' => '2',
        'day' => '*',
        'month' => '*',
        'dayofweek' => '*',
    ],
];
```

I use Moodle's plugin mechanisms to extend functionality rather than making unnecessary modifications to the platform's core files.

---

# 🏗️ Maintaining Monolithic Applications

I also work with legacy monolithic applications where functionality, dependencies and application components are closely connected.

My approach involves:

- Understanding existing application architecture.
- Tracing functionality across multiple areas of the codebase.
- Identifying dependencies before making changes.
- Isolating changes to reduce regression risk.
- Updating outdated PHP functionality.
- Introducing automated tests.
- Improving error handling.
- Using static analysis to find potential defects.
- Planning upgrades in manageable stages.
- Monitoring behaviour after deployment.

I recognise that modernising a monolithic application is often about improving reliability and maintainability without disrupting important business functionality.

---

# 💡 How I Approach Technical Problems

My development approach combines application-level debugging with infrastructure and deployment investigation.

When something fails, I work through the problem systematically:

1. **Identify** — Understand the error and its impact.
2. **Investigate** — Review logs, code, configuration and recent changes.
3. **Reproduce** — Confirm the problem in a controlled environment where possible.
4. **Fix** — Apply a targeted change.
5. **Validate** — Run tests and code quality checks.
6. **Deploy** — Release the change through the appropriate process.
7. **Monitor** — Confirm that the application is behaving correctly.
8. **Document** — Record the cause and resolution for future reference.

---

## 📌 Areas of Expertise

**Application Development**
PHP • Laravel • Angular • Moodle • WordPress

**Application Modernisation**
Legacy PHP • PHP 5 to PHP 8 • Composer • Monolithic Applications

**Testing and Quality**
PHPUnit • PHPStan • PHP_CodeSniffer • Static Analysis

**CI/CD and Version Control**
Git • GitHub • YAML • Bash • Automated Deployment

**AWS**
ECS • IAM • CloudWatch • SES • Certificate Manager • Notifications

**Azure**
Terraform • App Service • Key Vault • MySQL • Azure SQL • Networking

---

### 🎯 My Focus

Building, maintaining and improving applications through practical development, automated testing, infrastructure management and reliable deployment workflows.

I enjoy solving problems across the full application lifecycle — from understanding legacy PHP code and developing new functionality to troubleshooting cloud environments and improving release processes.
