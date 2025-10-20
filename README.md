# DevSecOps Templates

Centralized GitLab CI templates for automated security scanning and vulnerability management across all projects in the organization with automatic upload of results to DefectDojo.\
This repository provides reusable CI/CD templates that can be easily included in other GitLab pipelines to enforce secure development practices.\

| Category                     | Tool       | Description                                                                                        |
| ---------------------------- | ---------- | -------------------------------------------------------------------------------------------------- |
| **SAST**                     | Semgrep    | Static Application Security Testing — scans source code for vulnerabilities and insecure patterns. |
| **bSCA**                      | Trivy      | Software Composition Analysis — detects vulnerabilities in dependencies in container images.      |
| **DAST**                     | OWASP ZAP  | Dynamic Application Security Testing — performs security testing of running web applications.      |
| **Secrets Detection**        | Trufflehog | Searches for exposed secrets, credentials, and private keys in the repository.                     |
| **Vulnerability Management** | DefectDojo | Automatically uploads scan results for centralized tracking and triage.                            |


### To include and use these templates in your project, simply add the following to your .gitlab-ci.yml:\

```
include:
  - project: 'devsecops/devsecops-template'
    ref: master
    file:
      - '.gitlab-ci-sast-semgrep.yml'
      - '.gitlab-ci-sca-trivy.yml'
      - '.gitlab-ci-dast-zap.yml'
      - '.gitlab-ci-trufflehog.yml'

# Example jobs
sast_semgrep_scan:
  stage: sast
  extends: .sast_semgrep_scan_template

upload_semgrep_to_defectdojo:
  stage: upload
  extends: .upload_semgrep_to_defectdojo_template
  needs: [sast_semgrep_scan]
```
See the usage example in .gitlab-ci.yml\

### Template List
| File                               | Description                                        |
| ---------------------------------- | -------------------------------------------------- |
| `.gitlab-ci-sast-semgrep.yml`      | Static analysis (SAST) using Semgrep               |
| `.gitlab-ci-sca-trivy.yml`         | Container and dependency scanning using Trivy      |
| `.gitlab-ci-dast-zap.yml`          | Dynamic testing (DAST) using OWASP ZAP             |
| `.gitlab-ci-trufflehog.yml`        | Secret detection using Trufflehog                  |
| `.gitlab-ci.yml`                   | Template, example of use                           |
\
##### Requirements

GitLab Runner with Docker-in-Docker support

Access to the internal registry and DefectDojo instance

CI variables:

DEFECTDOJO_URL

DEFECTDOJO_TOKEN

(Optional) REPO_USER, REPO_TOKEN, REGISTRY

#### Notes

Each template is modular — you can include only what you need.

All reports are uploaded to DefectDojo for centralized vulnerability management.

Ideal for integrating DevSecOps best practices across all projects.


# DevSecOps Templates

Централизованный набор шаблонов GitLab CI для автоматизированного сканирования безопасности и управления уязвимостями во всех проектах организации.
Репозиторий содержит шаблоны, которые можно подключать к любому пайплайну GitLab для обеспечения безопасной разработки.

### Основные возможности
Категория	- Инструмент -	Описание
SAST	- Semgrep	- Статический анализ исходного кода на наличие уязвимостей и небезопасных конструкций.
bSCA	- Trivy	- Анализ зависимостей в контейнерах на известные уязвимости.
DAST	- OWASP ZAP	- Динамическое тестирование веб-приложений на этапе выполнения.
Secrets Detection	- Trufflehog	- Поиск открытых секретов, токенов и приватных ключей в репозитории.

### Пример использования

Добавьте шаблоны в свой .gitlab-ci.yml:


```
include:
  - project: 'devsecops/devsecops-template'
    ref: master
    file:
      - '.gitlab-ci-sast-semgrep.yml'
      - '.gitlab-ci-sca-trivy.yml'
      - '.gitlab-ci-dast-zap.yml'
      - '.gitlab-ci-trufflehog.yml'

# Example jobs
sast_semgrep_scan:
  stage: sast
  extends: .sast_semgrep_scan_template

upload_semgrep_to_defectdojo:
  stage: upload
  extends: .upload_semgrep_to_defectdojo_template
  needs: [sast_semgrep_scan]
```
Пример подключения смотри в файле .gitlab-ci.yml

### Список шаблонов:

| Файл                               | Назначение                                |
| ---------------------------------- | ----------------------------------------- |
| `.gitlab-ci-sast-semgrep.yml`      | SAST-анализ исходного кода (Semgrep)      |
| `.gitlab-ci-sca-trivy.yml`         | Анализ зависимостей в контейнерах (Trivy) |
| `.gitlab-ci-dast-zap.yml`          | Динамическое сканирование (OWASP ZAP)     |
| `.gitlab-ci-trufflehog.yml`        | Поиск секретов (Trufflehog)               |
| `.gitlab-ci.yml`                   | Шаблон, пример использования              |


#### Требования

GitLab Runner с поддержкой Docker-in-Docker

Доступ к внутреннему Docker Registry и DefectDojo

Переменные CI:

DEFECTDOJO_URL

DEFECTDOJO_TOKEN

(опционально) REPO_USER, REPO_TOKEN, REGISTRY

#### Примечания

Шаблоны модульные — можно подключать только нужные.

Все отчёты автоматически отправляются в DefectDojo.

Подходит для унификации DevSecOps-практик в всех проектах.
