# backend-cloud-r2-1 digest (round 2 fit check)

All accessed 2026-10-10. Method note: WebFetch returns a summary from a small model, not raw text; quotes are as relayed. Pub_date is "not stated" where the page shows none.

## Claims

1. NestJS: latest stable release is v12.1.1 (28 Sep 2026); latest major v12.0.0 released 27 Aug 2026.
   - source: https://github.com/nestjs/nest/releases | publisher: NestJS (GitHub) | pub_date: 2026-08-27 / 2026-09-28 | confidence: med | class: official primary | sources_count: 1 (docs.nestjs.com task-scheduling page links "See Version 11" which hints docs may lag; not verified against nestjs.com)

2. Node.js release schedule: v20 EOL 2026-04-30; v22 (Jod) Active LTS 2024-10-29, maintenance 2025-10-21, EOL 2027-04-30; v24 (Krypton) LTS 2025-10-28, maintenance 2026-10-20, EOL 2028-04-30; v26 Current (released 2026-05-05), LTS 2026-10-28, EOL 2029-04-30. Page notes dates are subject to change.
   - source: https://github.com/nodejs/release#release-schedule | publisher: Node.js Release WG | pub_date: not stated | confidence: high | class: official primary | sources_count: 2 (consistent with nodejs.org previous-releases: v20 EOL, v22 and v24 LTS, v26 Current)
   - second source: https://nodejs.org/en/about/previous-releases (publisher Node.js; that page gives status but no EOL dates; says LTS gets about 30 months total support). Resolves the round 1 conflict in favour of the GitHub schedule above; note nodejs.org page "last updated" column is not an EOL date, which may be the source of the earlier confusion (inference).

3. NestJS scheduler pitfall confirmed in official docs: "The scheduler runs every job in every process of your application"; example: a daily @Cron job runs three times on three instances. Docs recommend @OnOneInstance() from @nestjs/locks with a shared store (PostgreSQL or Redis).
   - source: https://docs.nestjs.com/techniques/task-scheduling | publisher: NestJS | pub_date: not stated | confidence: med (summary via WebFetch) | class: official primary | sources_count: 1

4. PostgreSQL RLS: superusers and BYPASSRLS roles always bypass; table owners bypass unless ALTER TABLE ... FORCE ROW LEVEL SECURITY; policies can target ALL, SELECT, INSERT, UPDATE, DELETE; only the table owner can enable/disable RLS or add policies; with RLS enabled and no policy, default-deny applies. An INSERT-only policy approximating append-only is an inference from documented mechanics, not a documented pattern; blocked UPDATE/DELETE on filtered rows can silently affect 0 rows.
   - source: https://www.postgresql.org/docs/current/ddl-rowsecurity.html | publisher: PostgreSQL Global Development Group | pub_date: not stated (current) | confidence: high for mechanics, med for append-only use | class: official primary | sources_count: 1

5. PostgreSQL privileges: an owner can revoke their own INSERT/UPDATE/DELETE/TRUNCATE ("make the table read-only to themselves"), but the owner implicitly holds all grant options and can grant them back; DROP/ALTER rights cannot be granted or revoked. Implication: REVOKE alone does not defend against the owner role or superuser; the app should connect as a non-owner role (inference).
   - source: https://www.postgresql.org/docs/current/sql-grant.html | publisher: PostgreSQL Global Development Group | pub_date: not stated | confidence: high | class: official primary | sources_count: 1

6. Regional availability (AWS service endpoints docs): Amazon RDS has endpoints in both ap-south-1 (Mumbai) and ap-south-2 (Hyderabad). Amazon SES API endpoints exist in both Mumbai and Hyderabad; SES SMTP endpoints are NOT available in Hyderabad (available in Mumbai); SES email receiving listed for Mumbai, not Hyderabad. RDS quotas docs list ap-south-1 with lower default quotas (20 DB instances vs 40 elsewhere).
   - source: https://docs.aws.amazon.com/general/latest/gr/rds-service.html and https://docs.aws.amazon.com/general/latest/gr/ses.html | publisher: AWS | pub_date: not stated | confidence: high (endpoint existence; does not prove every instance class or feature) | class: official primary | sources_count: 2 (one per service)

7. CloudFront is a global-endpoint service (not regional); the region table lists both Mumbai and Hyderabad as regions. Edge-location presence in India was not confirmed here.
   - source: https://docs.aws.amazon.com/general/latest/gr/rande.html | publisher: AWS | pub_date: not stated | confidence: med | class: official primary | sources_count: 1

8. Azure: the official pricing page fetched shows B1ms (1 vCore, 2 GiB) for PostgreSQL Flexible Server but price cells rendered as placeholders; a third-party aggregator lists about USD 18/month on-demand for B1ms in Central India (page updated 2026-07-20), about USD 12/month US East. Single source, third party.
   - source: https://www.bytebase.com/dbcost/azure-flexible/instance/B1ms/ (found via search snippet, not fetched directly) | publisher: Bytebase | pub_date: 2026-07-20 | confidence: low | class: third-party aggregator | sources_count: 1

9. AWS RDS PostgreSQL pricing page fetched exposed no Mumbai instance, storage or backup rates (tables collapsed). Only a general figure: T4g CPU credits USD 0.075 per vCPU-hour when baseline is exceeded.
   - source: https://aws.amazon.com/rds/postgresql/pricing/ | publisher: AWS | pub_date: not stated | confidence: med | class: official primary | sources_count: 1

10. ORM and migration (search-snippet level only, all low): Prisma migrations are generated SQL files reviewed in PRs, `migrate deploy` for production, NestJS integration via a custom PrismaService; TypeORM generates migrations from entities, must disable `synchronize` in production, and has had maintainer-activity concerns (claims conflict across sources); MikroORM has little production-migration evidence found.
    - source: search results incl. https://www.bytebase.com/blog/prisma-vs-typeorm.md | publisher: Bytebase and others (blogs) | pub_date: 2025 (title) | confidence: low | class: third-party blog | sources_count: several, none fetched

## Leads

- Azure cost: query https://prices.azure.com/api/retail/prices with a plain `$filter` via curl (WebFetch returned an empty Items list for my filter; filter syntax or the fetch layer may be at fault, not proven). Use serviceName 'Azure Database for PostgreSQL', armRegionName 'centralindia' (also 'southindia'), currencyCode=INR option.
- AWS cost: AWS Price List bulk JSON (https://pricing.us-east-1.amazonaws.com/offers/v1.0/aws/AmazonRDS/current/ap-south-1/index.json) via curl/Bash would give exact Mumbai RDS rates; I did not try Bash curl because of the call budget.
- Google Cloud: not attempted (Cloud SQL, Cloud Run, Cloud Scheduler pricing pages; Mumbai asia-south1 and Delhi asia-south2).
- AWS regional product table: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/ did not render data; try the SSM public parameters route (/aws/service/global-infrastructure/regions/ap-south-2/services) for ECS, Fargate, EventBridge Scheduler (service pages scheduler.* endpoints in docs.aws.amazon.com/general/latest/gr/ ecs-service.html and scheduler.html).
- NestJS @nestjs/locks and @OnOneInstance: confirm maturity and whether it is first party.
- Practitioner retrospectives: look at engineering blogs and Reddit/HN threads ("moved from NestJS to Django/Spring Boot") dated 2025-2026.
- pgaudit: check https://www.pgaudit.org and the AWS RDS docs for pgaudit support on RDS PostgreSQL.

## Looked for and could not find

- 6 to 12 month team retrospectives comparing NestJS with Django, FastAPI and Spring Boot: search returned only StackShare and generic comparison pages (one 2020-2021 thread noting NestJS cons: debugging difficulty, smaller community, breaking-change updates; unverified and old). No FastAPI coverage at all.
- PostgreSQL docs page for pgaudit: https://www.postgresql.org/docs/current/pgaudit.html returned 404 (pgaudit is an external extension, not in core docs; inference from the 404). Trigger-based audit docs not fetched.
- Per-service availability in Mumbai and Hyderabad for ECS Fargate and EventBridge Scheduler: not confirmed (regional-product-services page gave no table; Hyderabad not mentioned).
- Any official monthly cost figure for AWS, Azure or Google Cloud: none retrieved; no INR figures.
- Second source for the NestJS v12 version and date (nestjs.com or npm); only GitHub releases was consulted.
- MikroORM migration maturity evidence.
- Distinct sources used exceeded the 8 budget slightly (11 pages incl. failed ones); tool calls about 17.
