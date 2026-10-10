# Digest cloud-r1-1: AWS vs Azure vs GCP fit check (accessed 2026-10-10)

Note: WebFetch worked, but every provider pricing and region-availability page returned truncated or JS-rendered content (no tables). Only WebFetch was used (no WebSearch). Cost (Q3) and per-service India availability (Q2 partly) are NOT answered. Do not treat absence as evidence. The fetch tool summarizes pages with a small model, so claims are medium unless the page text was shown verbatim.

## Claims

1. claim: Stack Overflow Developer Survey 2025, "extensive development work in past year": all respondents AWS 43.3%, Azure 26.3%, Google Cloud 24.6%; professional developers AWS 45.9%, Azure 27.2%, GCP 24.3%; learning to code AWS 20.2%, Azure 12.1%, GCP 21.6%. AWS leads every group except GCP slightly ahead of AWS among learners.
   source: https://survey.stackoverflow.co/2025/technology | publisher: Stack Overflow | pub_date: 2025 (survey year; exact date not shown) | accessed 2026-10-10 | confidence: medium (fetch summary, figures not seen verbatim) | class: adoption | sources_count: 1

2. claim: Azure has three India-area regions with availability zones: Central India (Pune, 3 AZ, paired South India), India South Central (Hyderabad, 3 AZ, paired Central India). South India (Chennai) and West India (Mumbai) have no AZ (N/A) and are paired to each other's neighbours (South India pairs Central India; West India pairs South India). Geography for all is "India".
   source: https://learn.microsoft.com/en-us/azure/reliability/regions-list | publisher: Microsoft Learn | pub_date: page metadata updated 2026-09-23 | accessed 2026-10-10 | confidence: high (table text shown verbatim) | class: region/residency | sources_count: 1

3. claim: AWS lists two India regions: Asia Pacific (Mumbai) ap-south-1 and Asia Pacific (Hyderabad) ap-south-2.
   source: https://docs.aws.amazon.com/general/latest/gr/rande.html | publisher: AWS Docs | pub_date: not shown | accessed 2026-10-10 | confidence: high (table shown verbatim) | class: region | sources_count: 1

4. claim: Google Cloud states Cloud SQL, Compute Engine, GKE, Cloud Storage, KMS and Secret Manager are available at launch in every region, while Cloud Run is added within 6 months of a region's launch (so Cloud Run is expected in an established region but this does not confirm India specifically).
   source: https://cloud.google.com/about/locations | publisher: Google Cloud | pub_date: not shown | accessed 2026-10-10 | confidence: medium | class: service availability (general policy) | sources_count: 1

5. claim: AWS says Fargate, RDS, and Secrets Manager are "core services included in all Region launches", while CloudFront is delivered via edge locations and "usually launches within 12 months" of a new region. EventBridge Scheduler and App Runner are not mentioned on that page (the regional table did not render). Mumbai/Hyderabad were not confirmed per service.
   source: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/ | publisher: AWS | pub_date: not shown | accessed 2026-10-10 | confidence: medium | class: service availability (general policy) | sources_count: 1

6. claim: Azure Database for PostgreSQL flexible server: automated backups with PITR, default retention 7 days, max 35 days; WAL backup RPO up to ~5 minutes; backup storage free up to 100% of provisioned storage; restore always creates a new server; Burstable tier does NOT support on-demand backups; backup retention cannot be changed to geo-redundant after creation; long-term retention (to 10 years) via Azure Backup; zone-redundant backup storage keeps data in-country in AZ regions (residency note).
   source: https://learn.microsoft.com/en-us/azure/postgresql/backup-restore/concepts-backup-restore | publisher: Microsoft Learn | pub_date: 2026-07-05 (page metadata) | accessed 2026-10-10 | confidence: high (text shown verbatim) | class: ops/backup | sources_count: 1

7. claim: Amazon RDS automated backups let you restore to any point in time during the retention period; backups stored in S3; deleting an instance deletes automated backups unless you choose to retain them; up to 100 manual snapshots per region. (Retention default/max not in the retrieved excerpt.) AWS free tier (new accounts, 1 year): 20 GB automated backup storage; T4g CPU credits $0.075 per vCPU-hour (USD, all regions).
   sources: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html ; https://aws.amazon.com/rds/postgresql/pricing/ | publisher: AWS | pub_date: not shown | accessed 2026-10-10 | confidence: medium-high | class: ops/backup, cost | sources_count: 2

8. claim: Cloud SQL (PostgreSQL) automated backups are configurable 1 to 365 retained backups; backups are billed on backup size (first about DB size, later incremental); on-demand backups persist until deleted (cost risk); final backups are charged for days retained. Default count not confirmed.
   source: https://docs.cloud.google.com/sql/docs/postgres/backup-recovery/backups | publisher: Google Cloud Docs | pub_date: not shown | accessed 2026-10-10 | confidence: medium (fetch summary) | class: ops/backup | sources_count: 1

9. claim: Cloud Run free tier and regional tiering: a fetch summary said monthly free tier (180,000 vCPU-s, 360,000 GiB-s, 2M requests) and that asia-south1/2 are likely Tier 2 (higher price) - but both statements came from the model's background knowledge, not the page (page truncated). Treat as UNVERIFIED lead only.
   source: https://cloud.google.com/run/pricing | publisher: Google Cloud | accessed 2026-10-10 | confidence: low | class: cost | sources_count: 0 usable

## Cost (Q3): NOT ANSWERED
No INR/USD monthly estimate can be given from retrieved evidence. Fargate, RDS, Cloud Run, Azure PostgreSQL pricing pages all returned without region price tables (Azure B1ms showed only a "$-" placeholder). Pricing calculators are JS apps and not fetchable.

## Leads
- Use calculator.aws, cloud.google.com/products/calculator and azure.microsoft.com pricing calculator manually (or the AWS Price List bulk JSON / Azure Retail Prices API https://prices.azure.com/api/retail/prices with a Central India filter, which is fetchable JSON) for Mumbai/Central India/asia-south1 prices.
- AWS Systems Manager public parameters (/aws/service/global-infrastructure/regions/ap-south-1/services) or `aws apprunner list-services --region ap-south-1` can verify per-service availability programmatically; same with `gcloud run regions` / Azure "az provider show".
- Verify App Runner status/availability for new customers (not confirmed in any fetched source).
- Azure Learn "products by region" and GCP Region Picker need browser rendering.
- Data residency: AWS Mumbai/Hyderabad, Google asia-south1/asia-south2, and Azure region details (DPDP Act implications) not retrieved; only Azure ZRS in-country backup note.
- Not covered: Static hosting/CDN (S3+CloudFront, Static Web Apps, Firebase Hosting), scheduler services, secrets pricing, CI/CD options, monitoring/logging basics, and 6-12 month small-team experience reports.

## Looked for and could not find
- Per-service availability in ap-south-1/ap-south-2, Central India, asia-south1/asia-south2 (tables did not render).
- Any monthly price for Fargate, RDS db.t4g, Azure PostgreSQL B1ms, Cloud SQL, Cloud Run, CloudFront, schedulers in India regions.
- Cloud SQL default backup retention and PITR window; RDS default/max retention (excerpt cut).
- Community or practitioner reports on operational pain at 6-12 months (WebSearch not used; budget spent on pages that failed to render).
- Google Cloud India region list/launch details (locations page did not list India).
