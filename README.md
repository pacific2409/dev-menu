# DevMenu

> [!NOTE]
> 本Repositoryは、DevMenu Project全体と関連する公開成果物を案内するポートフォリオ用の入口です。各Repositoryは公開用Snapshotであり、Security、Environment固有情報、運用記録、作業履歴、Credentialその他の一部内容を公開対象から除外またはExample値へ置換しています。

## Overview

DevMenuは、学びたい技術、難易度、使える時間および目的を指定すると、個人開発やPoCで取り組める実装課題を3件提案するWeb Applicationです。

「試したい技術はあるが、具体的に何を作れば学習や検証につながるか決めにくい」という状態から、実際に取り組める課題へ進めることを目的としています。生成された提案と入力条件は共有履歴へ保存され、利用者は保存済みの技術名から過去の提案を再発見できます。

### Main Experience

1. 学びたい技術、難易度、所要時間、目的および任意の意向を入力する。
2. Amazon Bedrockを利用して生成された3件の実装課題を比較する。
3. 入力条件と成立した提案を共有履歴へ保存する。
4. 技術名を起点に過去の提案を一覧・詳細画面から再発見する。

Initial Implementationでは、要求定義、機能・Architecture・詳細設計、Infrastructure、Database、Backend、Frontend、Integration Test、Production ReleaseおよびProduction Verificationまでを一つのTrainとして実施しました。

## System Architecture

DevMenuは、ReactによるSingle Page Application、Jakarta EEによるModular Monolith Backend、Amazon Bedrock、RDS for MySQLで構成されています。ApplicationはAmazon EKS on Fargateで実行し、AWS InfrastructureはTerraform / Terragrunt、Application DeploymentはKubernetes / Kustomize、DeliveryはGitLab CI/CDを中心に管理します。

![DevMenu Production AWS Architecture](https://raw.githubusercontent.com/pacific2409/dev-menu-docs-public/master/persistent/infrastructure-architecture.png)

## Public Repositories

| Name | Overview | Main Contents / Technology Stack | Link |
| --- | --- | --- | --- |
| DevMenu Documentation | Product RequirementからArchitecture、API、UI、Tableまでを管理する公開設計Snapshot | Product Requirements、Function Design、System / Infrastructure Architecture、API / UI / Table Specification、Draw.io | [dev-menu-docs-public](https://github.com/pacific2409/dev-menu-docs-public) |
| AWS Infrastructure | DevMenuのAWS Infrastructure、Environment、Identity、DeliveryおよびLifecycleを管理するModule | Terraform、Terragrunt、AWS / Helm / Kubernetes Provider、VPC、EKS / Fargate、RDS、ECR、Route 53、ACM、WAF、CloudWatch、CloudTrail、Secrets Manager、Bedrock、GitLab CI/CD、Bash、Python | [dev-menu-aws-public](https://github.com/pacific2409/dev-menu-aws-public) |
| Database State Management | Environment別Schema、Account、GrantおよびTable DDLをVersion管理するDatabase Module | MySQL 8.4 LTS、SQL、SQLFluff、Amazon RDS for MySQL、AWS Secrets Manager、AWS Systems Manager Port Forwarding | [dev-menu-database-state-management-public](https://github.com/pacific2409/dev-menu-database-state-management-public) |
| Proposal Service | 課題提案、Amazon Bedrock連携、共有履歴およびHealth Endpointを提供するBackend Module | Java 21、Maven、Jakarta EE 11、MicroProfile、Payara Micro 7、AWS SDK for Java 2、EclipseLink、MySQL Connector/J、Log4j 2、JUnit 5、Docker、Kubernetes / Kustomize、GitLab CI/CD | [dev-menu-proposal-service-public](https://github.com/pacific2409/dev-menu-proposal-service-public) |
| Web Frontend | 課題注文・提案結果・共有履歴を提供するBrowser向けSingle Page Application | Node.js 24、React 19、React Router 7、TypeScript 6、Vite 8、Vitest 5、Testing Library、Playwright 1.64、OpenAPI TypeScript、Nginx、Docker、Kubernetes / Kustomize、GitLab CI/CD | [dev-menu-web-public](https://github.com/pacific2409/dev-menu-web-public) |
| Codex Project Template | DevMenu開発で使用した、Codex Agentによる仕様策定・実装・Review・Release管理のProject基盤 | Codex、AGENTS.md、Flow / Work Skills、Manager / Executor責務分離、Steering、Review用Subagent（Document Reviewer / Spec Comparator）、Explorer Subagent、Dev Container | [project-template](https://github.com/pacific2409/project-template) |

## Development Approach

DevMenuでは、Codex Agentを単一の実装担当として扱うのではなく、ManagerとModule別Executorに責務を分離しました。要求・設計・担当間Contractを文書として確定し、それぞれ独立したContextとRepositoryで作業しています。

- **Docs-first**: Product Requirement、Function Design、System / Infrastructure Architecture、詳細仕様を実装前に定義する。
- **Responsibility separation**: Infrastructure、Database、Backend、Frontendを独立したModuleとして管理する。
- **Train-based delivery**: Requirement、Design、Development、Integration、Release、Production Verificationを一つの変更単位として追跡する。
- **Explicit gates**: Development、Integration、Releaseの進行条件とユーザー承認を明示する。
- **Documented handoff**: Module間の依存事項、判断、Review、Handoffおよび検証結果を文書で受け渡す。
- **Immutable promotion**: Integrationで検証したArtifactを再BuildせずProductionへ昇格する。
- **Sanitized evidence**: Credential、Response Body、Raw Log等を残さず、検証結果と判定を追跡可能にする。

この進め方の基盤は、公開Repositoryの[project-template](https://github.com/pacific2409/project-template)にまとめています。

## Development Platform

実際の開発とCI/CDは、基本的に[GitLab.com / highEnough](https://gitlab.com/highEnough)上のRepositoryとPipelineで実施しました。

GitHub上のDevMenu各Repositoryは、完成した成果物をポートフォリオとして参照できるように作成した公開用Snapshotです。実EnvironmentのCredential、識別値、内部Runbook、Evidence、Handover、作業履歴およびGit履歴は公開対象に含めていません。

## Publication and License

- 公開Repositoryだけで実Environmentを再現・運用できることは保証しません。
- Example値を実値へ置き換えるだけで、安全なDeploymentが成立することは保証しません。
- 公開SnapshotにはLicenseを付与していません。著作権法上認められる範囲を超える利用、複製または再配布の許諾を意味しません。
