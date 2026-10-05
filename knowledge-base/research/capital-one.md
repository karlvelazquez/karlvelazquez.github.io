# Capital One — Software Engineer Intern (June – Aug 2024)

**Role:** Software Engineer Intern, Capital One, McLean, VA
**Dates:** June – August 2024

## What Karl did (resume-sourced)

- Added Zelle event data publishing into Capital One's in-house data lakes.
- Built this using Java and Spring Boot.
- Wrote and used Snowflake and Splunk queries to work with the resulting data.
- Used Capital One's in-house CI/CD tooling to ship the work.

## Background context (web research)

**Capital One's engineering stack.** Per job postings and Capital One's own hiring materials, the company's backend stack centers heavily on Java and Spring Boot microservices, often paired with Kafka for event messaging, AWS for cloud infrastructure, and a mix of SQL/NoSQL datastores. Capital One has positioned itself publicly as an all-in-cloud bank (it was one of the first major US banks to exit its own data centers in favor of AWS) and markets its engineering culture as oriented around "makers, breakers, doers and disruptors," with heavy internal investment in open-source tooling and, more recently, AI-assisted development tools. This matches the shape of Karl's internship: a Java/Spring Boot service publishing structured events into larger company-wide data infrastructure.

**Zelle.** Zelle is a peer-to-peer payments network operated by Early Warning Services, LLC, a company jointly owned by seven major US banks including Capital One, Bank of America, JPMorgan Chase, PNC, Truist, US Bank, and Wells Fargo. It lets enrolled bank customers send money to each other using just a phone number or email, with funds typically appearing within minutes. Despite its "instant" feel, much of Zelle's underlying settlement has historically ridden on traditional ACH rails with real-time messaging layered on top (some flows now move over newer real-time rails like RTP or FedNow); banks front the apparent instancy to the end user. Because Capital One is a Zelle owner-bank, instrumenting and publishing Zelle transaction events into internal systems (fraud monitoring, reconciliation, analytics) is meaningful plumbing work, not just a minor feature — it's exactly the kind of event-data pipeline a bank needs to build and keep observable.

**Data lakes, Snowflake, and Splunk.** A "data lake" is a centralized repository that stores large volumes of data — often in fairly raw form — so it can later be queried, modeled, and analyzed, as distinct from a traditional data warehouse that only holds cleaned, structured data. Snowflake is a cloud data platform that has increasingly blurred the line between data warehouse and data lake, offering scalable storage and SQL-based analytics; banks use it to centralize financial and behavioral data for purposes like fraud detection, credit risk modeling, and compliance reporting. Splunk, by contrast, is primarily an observability and log-analytics platform used to index and search machine-generated data (application logs, metrics, security events) in near real time. A common pattern — relevant to Karl's described work — is to send the full dataset to Snowflake for durable storage and deep analytics while routing the time-sensitive subset to Splunk for real-time monitoring and alerting, sometimes federating queries between the two.

**McLean, VA headquarters.** Capital One's headquarters sits in McLean, Virginia, about 30 minutes outside Washington, D.C., on a campus redeveloped starting in 2018 specifically to co-locate engineers, designers, and data scientists (the "Capital One Tower" and surrounding campus blocks). It functions as the company's primary engineering and corporate hub, distinct from Capital One's various standalone "Capital One Café" retail/tech-brand locations elsewhere.
