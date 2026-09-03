# Resources — mod-103-build-vs-buy-and-platform-economics

Primary references for the topics covered in this module.
Every entry is linked to a publisher, an author-maintained
URL, or an official standards body / vendor documentation
page. See [`JOB_REQUIREMENTS.md`](../../JOB_REQUIREMENTS.md)
for the full authoritative-reference list that grounds the
whole curriculum.

## Portfolio framing (chapter 01)

- **Fred Brooks** — *The Mythical Man-Month: Essays on
  Software Engineering* (Addison-Wesley) — background on
  the ongoing-cost side of the build column. Overview at
  [en.wikipedia.org/wiki/The_Mythical_Man-Month](https://en.wikipedia.org/wiki/The_Mythical_Man-Month).
- **Michael Nygard** — *Documenting Architecture Decisions* —
  [cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) —
  the ADR template every "buy" row in the matrix resolves
  into. Introduced in [`mod-102`](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md);
  used here as the resolution artifact.
- **Matthew Skelton and Manuel Pais** — *Team Topologies* —
  [teamtopologies.com/book](https://teamtopologies.com/book) —
  the team-load / cognitive-capacity vocabulary the
  team-time axis of the portfolio frame borrows from.

## Cloud providers as economic actors (chapter 02)

### Committed-use pricing

- **AWS Savings Plans** —
  [aws.amazon.com/savingsplans](https://aws.amazon.com/savingsplans/)
- **GCP Committed Use Discounts (CUDs)** —
  [cloud.google.com/docs/cuds](https://cloud.google.com/docs/cuds)
- **Azure Reserved VM Instances** —
  [azure.microsoft.com/pricing/reserved-vm-instances](https://azure.microsoft.com/en-us/pricing/reserved-vm-instances/)

### Interruptible / spot capacity

- **AWS EC2 Spot** —
  [aws.amazon.com/ec2/spot](https://aws.amazon.com/ec2/spot/)
- **GCP Spot VMs** —
  [cloud.google.com/spot-vms](https://cloud.google.com/spot-vms)
- **Azure Spot Virtual Machines** —
  [azure.microsoft.com/services/virtual-machines/spot](https://azure.microsoft.com/en-us/services/virtual-machines/spot/)

### Object-storage pricing (the reference workload the
chapter uses to compare the three)

- **Amazon S3 pricing** —
  [aws.amazon.com/s3/pricing](https://aws.amazon.com/s3/pricing/)
- **Google Cloud Storage pricing** —
  [cloud.google.com/storage/pricing](https://cloud.google.com/storage/pricing)
- **Azure Blob Storage pricing** —
  [azure.microsoft.com/pricing/details/storage/blobs](https://azure.microsoft.com/en-us/pricing/details/storage/blobs/)

### Egress — the lock-in trap the chapter names

- **AWS EC2 on-demand pricing — Data Transfer section** —
  [aws.amazon.com/ec2/pricing/on-demand](https://aws.amazon.com/ec2/pricing/on-demand/#Data_Transfer)
- **AWS — Free data transfer out to internet when moving
  out of AWS** (2024 announcement) —
  [aws.amazon.com/blogs/aws/free-data-transfer-out-to-internet-when-moving-out-of-aws](https://aws.amazon.com/blogs/aws/free-data-transfer-out-to-internet-when-moving-out-of-aws/) —
  the anti-egress-trap concession; read the fine print.
- **GCP VPC / Network pricing** —
  [cloud.google.com/vpc/network-pricing](https://cloud.google.com/vpc/network-pricing)
- **Azure Bandwidth pricing** —
  [azure.microsoft.com/pricing/details/bandwidth](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)
- **Cloudflare — *AWS's Egregious Egress*** —
  [blog.cloudflare.com/aws-egregious-egress](https://blog.cloudflare.com/aws-egregious-egress/) —
  vendor-partisan but load-bearing on the egress-margin
  argument that shapes the industry discussion.

### Credits programmes for startups

- **AWS Activate** —
  [aws.amazon.com/activate](https://aws.amazon.com/activate/)
- **Google Cloud for Startups** —
  [cloud.google.com/startup](https://cloud.google.com/startup)
- **Microsoft for Startups** —
  [microsoft.com/startups](https://www.microsoft.com/en-us/startups)

### Migration tooling

- **GCP Migration Center** —
  [cloud.google.com/migration-center](https://cloud.google.com/migration-center)
- **AWS Migration Hub** —
  [aws.amazon.com/migration-hub](https://aws.amazon.com/migration-hub/)

### Compute pricing (used by exercise 02's worked
comparison)

- **AWS EC2 on-demand pricing** —
  [aws.amazon.com/ec2/pricing/on-demand](https://aws.amazon.com/ec2/pricing/on-demand/)
- **GCP Compute Engine — all pricing** —
  [cloud.google.com/compute/all-pricing](https://cloud.google.com/compute/all-pricing)
- **Azure Virtual Machines — Linux pricing** —
  [azure.microsoft.com/pricing/details/virtual-machines/linux](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/linux/)

## Managed vs. self-hosted for the classic categories (chapter 03)

### Data warehouse / analytics

- **Snowflake** — [snowflake.com](https://www.snowflake.com/);
  pricing at
  [snowflake.com/pricing](https://www.snowflake.com/pricing/).
- **Google BigQuery** —
  [cloud.google.com/bigquery](https://cloud.google.com/bigquery);
  pricing at
  [cloud.google.com/bigquery/pricing](https://cloud.google.com/bigquery/pricing).
- **Amazon Redshift** —
  [aws.amazon.com/redshift](https://aws.amazon.com/redshift/).
- **ClickHouse** — [clickhouse.com](https://clickhouse.com/) —
  the leading OSS OLAP engine cited as the self-host
  option.
- **DuckDB** — [duckdb.org](https://duckdb.org/) — the
  in-process OLAP option the chapter names for the
  small-team case.
- **Apache Iceberg** —
  [iceberg.apache.org](https://iceberg.apache.org/) — the
  open table format cited as the storage-layer OSS
  fallback.

### Auth / identity

- **Auth0** — [auth0.com](https://auth0.com/) (now part of
  Okta).
- **WorkOS** — [workos.com](https://workos.com/) —
  positioned for enterprise SSO / SAML / SCIM.
- **Clerk** — [clerk.com](https://clerk.com/).
- **Firebase Authentication** —
  [firebase.google.com/products/auth](https://firebase.google.com/products/auth).
- **Amazon Cognito** —
  [aws.amazon.com/cognito](https://aws.amazon.com/cognito/).
- **Microsoft Entra External ID** —
  [microsoft.com/entra/external-id](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-external-id).
- **Keycloak** —
  [keycloak.org](https://www.keycloak.org/) — the reference
  OSS identity provider.
- **Ory Kratos** —
  [ory.sh/kratos](https://www.ory.sh/kratos/) — the
  modern-Go OSS identity engine.
- **SuperTokens** —
  [supertokens.com](https://supertokens.com/) — hybrid
  OSS / managed option.

### Payments

- **Stripe** — [stripe.com](https://stripe.com/) — the
  default recommendation for the US / dev-first product
  case; documentation at [stripe.com/docs](https://stripe.com/docs).
- **Adyen** — [adyen.com](https://www.adyen.com/) — the
  global-acquiring / large-merchant reference.
- **Braintree** —
  [braintreepayments.com](https://www.braintreepayments.com/) —
  PayPal-owned; the third option cited.
- **PCI DSS SAQ A** (the lightest self-assessment tier the
  chapter references) — [pcisecuritystandards.org — SAQ
  documents](https://www.pcisecuritystandards.org/document_library/) —
  useful for the PCI-scope-reduction argument the chapter
  makes for buying payments.

### Observability

- **Datadog** —
  [datadoghq.com](https://www.datadoghq.com/).
- **Grafana Cloud** —
  [grafana.com/products/cloud](https://grafana.com/products/cloud/) —
  Grafana Labs' managed offering built on the OSS Grafana
  / Loki / Mimir / Tempo stack.
- **New Relic** — [newrelic.com](https://newrelic.com/).
- **Honeycomb** —
  [honeycomb.io](https://www.honeycomb.io/) — high-cardinality
  event tracing.
- **OpenTelemetry** —
  [opentelemetry.io](https://opentelemetry.io/) — the
  CNCF vendor-neutral instrumentation standard that keeps
  the observability decision reversible.

### CI / CD

- **GitHub Actions** —
  [github.com/features/actions](https://github.com/features/actions).
- **CircleCI** — [circleci.com](https://circleci.com/).
- **GitLab CI/CD** —
  [about.gitlab.com](https://about.gitlab.com/topics/ci-cd/).
- **Buildkite** — [buildkite.com](https://buildkite.com/) —
  hybrid model (managed control plane, self-hosted runners).
- **Jenkins** — [jenkins.io](https://www.jenkins.io/) —
  the incumbent self-host option.
- **Argo Workflows / Argo CD** —
  [argoproj.github.io](https://argoproj.github.io/) — the
  Kubernetes-native CI / CD reference.
- **Woodpecker CI** —
  [woodpecker-ci.org](https://woodpecker-ci.org/) — a
  lighter-weight OSS option.
- **OpenSSF SLSA — Supply-chain Levels for Software
  Artifacts** — [slsa.dev](https://slsa.dev/) — the
  build-provenance target the chapter names for the
  hosted-vs-self-hosted attestation posture.

### Feature flags

- **LaunchDarkly** —
  [launchdarkly.com](https://launchdarkly.com/) — the
  incumbent managed option.
- **Split** — [split.io](https://www.split.io/).
- **Optimizely** —
  [optimizely.com](https://www.optimizely.com/) — the
  A/B-testing-first option.
- **GrowthBook** —
  [growthbook.io](https://www.growthbook.io/) — leading
  OSS / hybrid alternative.
- **Flagsmith** —
  [flagsmith.com](https://www.flagsmith.com/) — leading
  OSS / hybrid alternative.
- **OpenFeature** —
  [openfeature.dev](https://openfeature.dev/) — the CNCF
  vendor-neutral feature-flag standard.

### Licence reference (for OSS-fallback assessment)

- **Open Source Initiative — Licenses** —
  [opensource.org/licenses](https://opensource.org/licenses/) —
  the canonical list used to check whether a "self-host"
  option is actually OSI-approved OSS or a
  source-available BSL / SSPL / Elastic-License 2.0
  offering.

## AI-native stack decisions (chapter 04)

### Foundation-model APIs

- **OpenAI Platform** —
  [platform.openai.com/docs](https://platform.openai.com/docs);
  pricing at
  [openai.com/pricing](https://openai.com/pricing).
  Enterprise privacy / retention posture at
  [openai.com/enterprise-privacy](https://openai.com/enterprise-privacy/).
- **Anthropic** — docs at
  [docs.anthropic.com](https://docs.anthropic.com/); pricing
  at [anthropic.com/pricing](https://www.anthropic.com/pricing);
  HIPAA posture at
  [anthropic.com/legal/hipaa](https://www.anthropic.com/legal/hipaa).
- **Google — Gemini API** —
  [ai.google.dev](https://ai.google.dev/); pricing at
  [ai.google.dev/pricing](https://ai.google.dev/pricing).
- **Azure OpenAI Service** —
  [azure.microsoft.com/products/ai-services/openai-service](https://azure.microsoft.com/en-us/products/ai-services/openai-service).
- **AWS Bedrock** —
  [aws.amazon.com/bedrock](https://aws.amazon.com/bedrock/) —
  multi-model API surface (Anthropic, Meta, Mistral, Cohere,
  Amazon Titan).
- **Google Vertex AI — Generative AI docs** —
  [cloud.google.com/vertex-ai/generative-ai/docs](https://cloud.google.com/vertex-ai/generative-ai/docs).

### Open-weight models

- **Llama** — [llama.com](https://www.llama.com/) — Meta's
  open-weight family, cited in chapter 04 as the reference
  open-weight case.
- **Mistral AI** — [mistral.ai](https://mistral.ai/) —
  cited in chapter 04 alongside Llama for the
  European-hosted open-weight option.
- Qwen (Alibaba), Gemma (Google), and DeepSeek are named in
  chapter 04 as further open-weight families to evaluate;
  consult each publisher's current model card and licence
  page directly, as URLs and licence terms shift by release.

### Inference / hosting for open-weight models

- **Together AI** —
  [together.ai](https://www.together.ai/).
- **Fireworks AI** —
  [fireworks.ai](https://fireworks.ai/).
- **Replicate** — [replicate.com](https://replicate.com/).
- **Modal** — [modal.com](https://modal.com/).
- **Baseten** — [baseten.co](https://www.baseten.co/).

### Self-hosted inference runtimes

- **vLLM** — [docs.vllm.ai](https://docs.vllm.ai/) — the
  reference high-throughput OSS serving runtime.
- **Hugging Face Text Generation Inference (TGI)** —
  [github.com/huggingface/text-generation-inference](https://github.com/huggingface/text-generation-inference).
- **NVIDIA Triton Inference Server** —
  [developer.nvidia.com/triton-inference-server](https://developer.nvidia.com/triton-inference-server).

### Papers named in chapter 04's architecture section

- **Lewis et al. (2020)** — *Retrieval-Augmented Generation
  for Knowledge-Intensive NLP Tasks* —
  [arxiv.org/abs/2005.11401](https://arxiv.org/abs/2005.11401) —
  the RAG reference.
- **Dettmers et al. (2023)** — *QLoRA: Efficient Finetuning
  of Quantized LLMs* —
  [arxiv.org/abs/2305.14314](https://arxiv.org/abs/2305.14314) —
  the reference cost-efficient fine-tuning technique.
- **Rafailov et al. (2023)** — *Direct Preference
  Optimization: Your Language Model is Secretly a Reward
  Model* —
  [arxiv.org/abs/2305.18290](https://arxiv.org/abs/2305.18290) —
  the DPO reference for lightweight alignment.

### Vector / retrieval infrastructure

- **Pinecone** — [pinecone.io](https://www.pinecone.io/).
- **Weaviate** — [weaviate.io](https://weaviate.io/).
- **Qdrant** — [qdrant.tech](https://qdrant.tech/).

### Orchestration / agents

- **Model Context Protocol** —
  [modelcontextprotocol.io](https://modelcontextprotocol.io/) —
  the open protocol for tool-use / context integration
  chapter 04 names for the tool-use architecture.
- **LangChain** —
  [langchain.com](https://www.langchain.com/).
- **LlamaIndex** —
  [llamaindex.ai](https://www.llamaindex.ai/).

### Data-protection posture (DPA / BAA / residency)

- **GDPR — plain-language reference** —
  [gdpr.eu/what-is-gdpr](https://gdpr.eu/what-is-gdpr/); the
  EU regulator's page at
  [edpb.europa.eu](https://www.edpb.europa.eu/); official
  regulation text (Regulation (EU) 2016/679) at
  [eur-lex.europa.eu/eli/reg/2016/679/oj](https://eur-lex.europa.eu/eli/reg/2016/679/oj).
- **OpenAI Data Processing Addendum** —
  [openai.com/policies/data-processing-addendum](https://openai.com/policies/data-processing-addendum/).
- **Anthropic — legal / DPA** —
  [anthropic.com/legal](https://www.anthropic.com/legal).
- **Google Cloud Data Processing Addendum** —
  [cloud.google.com/terms/data-processing-addendum](https://cloud.google.com/terms/data-processing-addendum).
- **AWS — GDPR Center (includes DPA)** —
  [aws.amazon.com/compliance/gdpr-center](https://aws.amazon.com/compliance/gdpr-center/).
- **Microsoft Data Protection Addendum** —
  [microsoft.com/licensing/docs/view/Data-Protection-Addendum](https://www.microsoft.com/licensing/docs/view/Data-Protection-Addendum).
- **HHS — HIPAA Security Rule** —
  [hhs.gov/hipaa/for-professionals/security/index.html](https://www.hhs.gov/hipaa/for-professionals/security/index.html) —
  the underlying US regulation the BAA operationalises.
- **OpenAI — Enterprise Privacy (BAA reference)** —
  [openai.com/enterprise-privacy](https://openai.com/enterprise-privacy/).
- **Anthropic — HIPAA / BAA** —
  [anthropic.com/legal/hipaa](https://www.anthropic.com/legal/hipaa).
- **Microsoft Trust Center — HIPAA** —
  [microsoft.com/trust-center/compliance/hipaa](https://www.microsoft.com/en-us/trust-center/compliance/hipaa) —
  covers Azure OpenAI eligibility.
- **AWS — HIPAA Compliance** —
  [aws.amazon.com/compliance/hipaa-compliance](https://aws.amazon.com/compliance/hipaa-compliance/) —
  covers Bedrock eligibility; also see the
  HIPAA-eligible-services list linked from that page.
- **Google Cloud — HIPAA Compliance** —
  [cloud.google.com/security/compliance/hipaa](https://cloud.google.com/security/compliance/hipaa).

MLOps and ML platform depth are deliberately out of scope
here; they defer to
[`ai-infra-mlops`](../../../ai-infra-mlops-learning)
(level 25) and
[`ai-infra-ml-platform`](../../../ai-infra-ml-platform-learning)
(level 30).

## ThoughtWorks Radar and CNCF Landscape as references (chapter 05)

### The two industry references themselves

- **ThoughtWorks Technology Radar** —
  [thoughtworks.com/radar](https://www.thoughtworks.com/en-us/radar);
  FAQ at
  [thoughtworks.com/radar/faq](https://www.thoughtworks.com/en-us/radar/faq).
- **CNCF Landscape** —
  [landscape.cncf.io](https://landscape.cncf.io/); about
  page at
  [landscape.cncf.io/about](https://landscape.cncf.io/about).
- **CNCF Projects — Sandbox / Incubating / Graduated
  index** — [cncf.io/projects](https://www.cncf.io/projects/).
- **CNCF Graduation Criteria** (the maturity contract) —
  [github.com/cncf/toc/blob/main/process/graduation_criteria.md](https://github.com/cncf/toc/blob/main/process/graduation_criteria.md).

### CNCF graduated projects the chapter names

- **Kubernetes** — [kubernetes.io](https://kubernetes.io/).
- **Prometheus** — [prometheus.io](https://prometheus.io/).
- **Envoy** — [envoyproxy.io](https://www.envoyproxy.io/).
- **Fluentd** — [fluentd.org](https://www.fluentd.org/).
- **containerd** — [containerd.io](https://containerd.io/).
- **Helm** — [helm.sh](https://helm.sh/).
- **Argo** — [argoproj.github.io](https://argoproj.github.io/).

### Peer foundations the chapter contrasts with the CNCF

- **Apache Software Foundation** —
  [apache.org](https://apache.org/) — has its own
  incubation / TLP maturity model.
- **The Linux Foundation** —
  [linuxfoundation.org](https://www.linuxfoundation.org/).
- **OpenJS Foundation** —
  [openjsf.org](https://openjsf.org/).

### Third-party signal sources cross-referenced in chapter 05

- **DORA — State of DevOps research** —
  [dora.dev/research](https://dora.dev/research/) — the
  delivery-cadence signal set (also used in mod-106).
- **Stack Overflow Developer Survey** —
  [survey.stackoverflow.co](https://survey.stackoverflow.co/) —
  practitioner-adoption evidence.
- **JetBrains Developer Ecosystem Survey** —
  [jetbrains.com/lp/devecosystem](https://www.jetbrains.com/lp/devecosystem/) —
  independent secondary signal on tooling adoption.

## Vendor-selection scorecard (chapter 06)

### Vendor-trajectory incidents cited by name

- **Okta — completion of Auth0 acquisition** (2021-05-03)
  — [businesswire.com — Okta announces close](https://www.businesswire.com/news/home/20210503005357/en/Okta-Completes-Acquisition-of-Auth0)
  — the canonical reference the chapter uses for the
  "vendor-gets-acquired" trajectory case.
- **HashiCorp — adoption of the Business Source Licence**
  (BSL, 2023) —
  [hashicorp.com/blog/hashicorp-adopts-business-source-license](https://www.hashicorp.com/blog/hashicorp-adopts-business-source-license) —
  the canonical reference for the "OSS licence change"
  trajectory case.
- **Elastic — *Why We're Changing Our Licence*** (2021) —
  [elastic.co/blog/why-license-change-aws](https://www.elastic.co/blog/why-license-change-aws) —
  the peer-precedent case; the announcement that triggered
  the OpenSearch fork.
- **OpenTofu** — [opentofu.org](https://opentofu.org/) —
  Linux Foundation fork of Terraform after the HashiCorp
  BSL change; the OSS-fallback case study.
- **OpenSearch** —
  [opensearch.org](https://opensearch.org/) — AWS-led fork
  of Elasticsearch / Kibana; the OSS-fallback case study.

### OSS-fallback references (the third non-negotiable scorecard column)

- **Keycloak** — [keycloak.org](https://www.keycloak.org/) —
  OSS fallback for the auth / identity category.
- **Ory Kratos** — [ory.sh](https://www.ory.sh/) — OSS
  fallback for the auth / identity category.
- **OpenTelemetry** —
  [opentelemetry.io](https://opentelemetry.io/) — the
  vendor-neutral instrumentation standard that keeps the
  observability decision reversible.
- **OpenFeature** —
  [openfeature.dev](https://openfeature.dev/) — the
  vendor-neutral feature-flag standard.
- **Apache Iceberg** —
  [iceberg.apache.org](https://iceberg.apache.org/) — the
  open table format that decouples warehouse-storage from
  warehouse-compute.
- **Argo Workflows / Argo CD** —
  [argoproj.github.io](https://argoproj.github.io/) — OSS
  CI / CD fallback.
- **Woodpecker CI** —
  [woodpecker-ci.org](https://woodpecker-ci.org/) — OSS
  CI fallback.
- **Kubernetes** — [kubernetes.io](https://kubernetes.io/) —
  the compute-substrate OSS fallback for the "managed
  container platform" decision.
- **MinIO** — [min.io](https://min.io/) — S3-compatible OSS
  object storage; noted as a *comparable-fallback caveat*
  in chapter 06 rather than a drop-in substitute for
  hyperscale-managed S3.
- **Ceph** — [ceph.io](https://ceph.io/) — same category as
  MinIO for the object-storage OSS-fallback slot.

## Security, compliance, and enterprise-readiness references (chapter 03 and chapter 04)

Chapter 03's "SOC 2 / HIPAA-BAA / GDPR-DPA" decision-forcing
questions and chapter 04's data-posture sub-questions inherit
from the founder-scope compliance references. Full depth on
each is in
[`mod-107-founder-scope-security-and-compliance`](../mod-107-founder-scope-security-and-compliance/).

- **AICPA — SOC 2 Trust Services Criteria** —
  [aicpa-cima.com — SOC 2](https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-soc-2).
- **ISO/IEC 27001:2022** —
  [iso.org/standard/27001](https://www.iso.org/standard/27001) —
  information-security management systems.
- **NIST Cybersecurity Framework 2.0** —
  [nist.gov/cyberframework](https://www.nist.gov/cyberframework).
- **NIST SP 800-53 Rev. 5** —
  [nvlpubs.nist.gov — NIST.SP.800-53r5.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf).
- **GDPR — Regulation (EU) 2016/679** —
  [eur-lex.europa.eu — 2016/679](https://eur-lex.europa.eu/eli/reg/2016/679/oj).
- **CCPA / CPRA — California Attorney General** —
  [oag.ca.gov/privacy/ccpa](https://oag.ca.gov/privacy/ccpa).
- **HIPAA Security Rule (HHS)** —
  [hhs.gov/hipaa/for-professionals/security/index.html](https://www.hhs.gov/hipaa/for-professionals/security/index.html).
- **OWASP Application Security Verification Standard
  (ASVS)** —
  [owasp.org — ASVS](https://owasp.org/www-project-application-security-verification-standard/).
- **PCI Security Standards Council — document library** —
  [pcisecuritystandards.org](https://www.pcisecuritystandards.org/document_library/) —
  the source for SAQ A and the other self-assessment
  questionnaires the "buy payments" case in chapter 03
  invokes.

## Adjacent-module references

- **`mod-101-cto-role-and-ownership-map`** — the CTO ladder
  and the shared reading vocabulary (Majors, Horowitz,
  Fournier, Larson). Chapter 05 of that module is the
  vocabulary this module's readers are assumed to share.
- **`mod-102-architecture-under-uncertainty`** — the ADR
  (chapter 02), C4 (chapter 03), monolith-first (chapter
  01), and spike (chapter 06) vocabulary that every "buy"
  row in this module resolves into. Exercise 02's Bucket-B
  vendor ADR is the input this module extends into a full
  scorecard.
- **`mod-104-first-engineering-hires-and-team-topology`** —
  every "build" disposition on the build-vs-buy matrix has
  a hiring consequence; mod-104's hiring plan is built
  against exercise 01's matrix.
- **`mod-105-technical-debt-as-business-decision`** — the
  deprecate-vs-rewrite frame reuses the portfolio vocabulary
  chapter 01 introduces; some vendor decisions are debt
  decisions in disguise.
- **`mod-107-founder-scope-security-and-compliance`** —
  full depth on the SOC 2 / HIPAA / GDPR / DPA / BAA
  vocabulary chapter 03 and chapter 04 lean on.
- **`mod-108-cto-ceo-and-board-communication`** — the
  vendor-strategy package this module builds up is one of
  the artifacts the technical-due-diligence and
  board-communication material in mod-108 assumes exists.

## Higher-level tracks this module explicitly defers up to

- **`ai-infra-mlops`** (level 25) —
  [../../../ai-infra-mlops-learning](../../../ai-infra-mlops-learning) —
  MLOps platform depth (training / eval infrastructure,
  model registry, deployment pipelines) beyond the
  seed-stage CTO's build-vs-buy scope.
- **`ai-infra-ml-platform`** (level 30) —
  [../../../ai-infra-ml-platform-learning](../../../ai-infra-ml-platform-learning) —
  ML platform depth (feature store, serving mesh,
  multi-tenant model isolation) beyond the seed-stage
  CTO's build-vs-buy scope.
- **`ai-infra-senior-architect`** (level 45) —
  [../../../ai-infra-senior-architect-learning](../../../ai-infra-senior-architect-learning) —
  deep multi-region / multi-tenant / high-scale
  architecture beyond the pre-seed / seed CTO's scope.
- **`ai-infra-principal-architect`** (level 55) —
  [../../../ai-infra-principal-architect-learning](../../../ai-infra-principal-architect-learning) —
  highest-altitude architectural depth for multi-cloud /
  multi-region posture.

## Communities and ongoing peer-learning surfaces

- **CTO Craft** — [ctocraft.com](https://www.ctocraft.com/) —
  community of practice for CTOs across stages; recurring
  vendor-selection retrospectives.
- **First Round Review** —
  [review.firstround.com](https://review.firstround.com/) —
  operator-authored essays; useful for vendor-trajectory
  and platform-economics case studies.
- **Lenny's Newsletter — Engineering / CTO track** —
  [lennysnewsletter.com](https://www.lennysnewsletter.com/).
- **a16z — technical due-diligence checklist** —
  [a16z.com/tech-diligence-checklist](https://a16z.com/tech-diligence-checklist/) —
  investor-side reference for the artifacts this module's
  scorecard and matrix ultimately have to survive.

---

Full citations with `use` notes for the whole curriculum are
in [`.aicg/job-requirements.json`](../../.aicg/job-requirements.json)
under `authoritative_references`.
