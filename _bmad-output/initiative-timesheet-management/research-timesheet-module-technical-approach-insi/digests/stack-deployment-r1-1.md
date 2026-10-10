# Digest: stack-deployment-r1-1

Accessed 2026-10-10 for all claims. WebFetch worked (it summarizes via a small model, so figures are second-hand to the page). Class: fact / vendor-doc / anecdote.

## Claims

1. Claim: In the 2025 Stack Overflow Developer Survey, all respondents reported web framework use of Next.js 20.8%, ASP.NET Core 19.7%, FastAPI 14.8%, Spring Boot 14.7%, Django 12.6%, Laravel 8.9%, NestJS 6.7%, Rails 5.9%.
   - Source: https://survey.stackoverflow.co/2025/technology
   - Publisher: Stack Overflow
   - pub_date: 2025 (page gives no exact date)
   - confidence: high (primary page; a fetch summarizer was used)
   - class: fact (survey)
   - Caveat: this is usage across all respondents, not internal line-of-business apps. It says nothing on hiring or productivity.

2. Claim: In the same survey, databases used were PostgreSQL 55.6%, MySQL 40.5%, SQL Server 30.1%.
   - Source: https://survey.stackoverflow.co/2025/technology
   - Publisher: Stack Overflow
   - pub_date: 2025
   - confidence: high
   - class: fact (survey)

3. Claim: In the same survey, cloud platform use was AWS 43.3%, Azure 26.3%, Google Cloud 24.6%, Cloudflare 20.1%.
   - Source: https://survey.stackoverflow.co/2025/technology
   - Publisher: Stack Overflow
   - pub_date: 2025
   - confidence: high
   - class: fact (survey)
   - Caveat: the 2026 survey may exist and was not checked.

4. Claim: PostgreSQL row-level locks block only writers and lockers of the same row, not plain reads, and are released at transaction end.
   - Claim: SELECT ... FOR UPDATE locks the rows until the transaction ends. Under REPEATABLE READ or SERIALIZABLE it errors if the row changed after the transaction started.
   - Claim: The docs warn against holding transactions open while waiting for user input, so an approver should not hold a row lock while reviewing. They advise locking rows in a consistent order and retrying on deadlock.
   - Source: https://www.postgresql.org/docs/current/explicit-locking.html
   - Publisher: PostgreSQL Global Development Group
   - pub_date: current docs (undated)
   - confidence: high (the guidance lines come from the fetch summarizer; verify the exact wording)
   - class: vendor-doc
   - Note: the SKIP LOCKED text was not on this page. Check the SELECT reference.

5. Claim: AWS Asia Pacific (Mumbai) opened June 2016 with 2 AZs at launch. AWS Hyderabad opened 22 Nov 2022 with 3 AZs. AWS says it lets customers with data residency preferences store data in India.
   - Source: https://press.aboutamazon.com/2022/11/aws-launches-second-infrastructure-region-in-india (found via search, not fetched). Also https://aws.amazon.com/tw/about-aws/whats-new/2016/06/announcing-the-aws-asia-pacific-mumbai-region/ (found via search, not fetched).
   - Publisher: Amazon / AWS
   - pub_date: 2022-11 and 2016-06
   - confidence: med (search summary only)
   - class: vendor-doc
   - Caveat: Mumbai's current AZ count was not retrieved.

6. Claim: Azure India regions: Central India (Pune, 3 AZs), India South Central (Hyderabad, 3 AZs), South India (Chennai, no AZs), West India (Mumbai, no AZs).
   - Source: https://learn.microsoft.com/en-us/azure/reliability/regions-list
   - Publisher: Microsoft
   - pub_date: updated 2026-09-23
   - confidence: high
   - class: vendor-doc

7. Claim: Google Cloud India regions are Mumbai (asia-south1) and Delhi (asia-south2). Zone counts were not stated on the page.
   - Source: https://cloud.google.com/about/locations
   - Publisher: Google Cloud
   - pub_date: undated
   - confidence: med
   - class: vendor-doc

8. Claim: Render's listed regions are Oregon, Ohio, Virginia, Frankfurt and Singapore. None is in India.
   - Source: https://render.com/docs/regions
   - Publisher: Render
   - pub_date: undated
   - confidence: med (single fetch)
   - class: vendor-doc

9. Claim: Fly.io's regions page lists 17 regions, none in India (no Mumbai/bom).
   - Source: https://docs.fly.io/reference/regions
   - Publisher: Fly.io
   - pub_date: undated
   - confidence: med (single fetch, summarizer-reported)
   - class: vendor-doc
   - Implication: for India data residency, Render and Fly would serve from Singapore or elsewhere, outside India.

10. Claim: AWS Fargate Linux/x86 example rates (US East N. Virginia) are about $0.000011244 per vCPU-second (about $0.0405/hour) and about $0.000001235 per GB-second (about $0.00445/hour). The hourly figures are the summarizer's conversion.
    - Source: https://aws.amazon.com/fargate/pricing/
    - Publisher: AWS
    - pub_date: undated
    - confidence: low-med (one source; this is the US region, not Mumbai or Hyderabad; cost numbers need two sources)
    - class: vendor-doc

11. Claim: Small-team regret evidence on Kubernetes is mostly anecdote and vendor content. Examples: Rock Arch spent about 2 years on EKS experiments and chose not to migrate, citing opacity and immature CI/CD and ops. A DEV.to author moved a small service to ECS Fargate in 3 days and self-reported about 60% lower cost. In The Pocket moved off Kubernetes to ECS, but at 50 microservices.
    - Source: search summary only, pages not fetched. https://blog.rockarch.org/not-choosing-kubernetes ; https://dev.to/stevenstuartm/why-i-migrated-from-kubernetes-to-ecs-48ed ; https://www.inthepocket.com/blog/moving-away-from-kubernetes-to-aws-ecs-a-seamless-transition
    - Publisher: various blogs
    - pub_date: unknown
    - confidence: low
    - class: anecdote
    - Caveat: the search found no source tracking teams 6 to 12 months after adoption.

## Leads (not retrieved or not verified)

- Stack Overflow 2025 pages on "most admired" and professional-developer sections returned 404 or nothing useful. Try https://survey.stackoverflow.co/2025/ and check whether a 2026 survey exists.
- JetBrains Developer Ecosystem survey and State of JS were not fetched.
- Cloud Run pricing page fetch was truncated. AWS Mumbai Fargate prices and RDS PostgreSQL costs are still needed.
- PostgreSQL SELECT reference for SKIP LOCKED, and the transaction isolation chapter (13.2).
- India data residency law (DPDP Act and rules) and any RBI/sector rules, not researched.
- Azure App Service and Cloud Run Mumbai availability and pricing.
- Fetch the Rock Arch and DEV.to posts directly to verify their claims.

## Looked for and could not find

- Survey data on adoption, hiring or productivity specific to internal line-of-business apps.
- Any hiring-market data for India by stack.
- Observability, backup and CI/CD cost evidence for small teams (not searched, budget).
- Audit-table patterns (triggers vs application-level), not searched.
- Reports of regrets at 6 to 12 months for Django, NestJS, Spring Boot, .NET, Laravel or Rails. No such source found.
- Cost order of magnitude for Render, Railway, Azure App Service or Cloud Run.
- Railway regions, and any current-year (2026) survey data.
