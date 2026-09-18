# CV

## Summary
Name: Vasiliy Tolstov (Толстов Василий Георгиевич)  
Date of birth: 31.07.1986  
Phone: +7xxx994xx54  
Email: v.tolstov[at]selfip.ru (preferred contact method)  
Skype: vtolstov (rarely checked, by prior arrangement only)  
Telegram: @vtolstov  
Location: Saint Petersburg, Russia  
Citizenship: Russia  
Relocation: not open to business travel, not open to relocating to Moscow  
Target role: CTO, technical lead, head of development  
Focus: technical leadership, engineering management, platform-level architecture;
I consider individual-contributor roles only in combination with a technical lead function  
Employment: flexible hours, remote (preferred)  
Preferred commute: no more than one hour  
Years in the field: 21  

## Profile
Technical leader with 21+ years in software development and engineering management.
I specialise in designing high-load distributed systems in Go and microservice
architectures. I combine deep technical expertise with management experience: hiring and
evaluating developers, establishing processes (DOR/DOD), platform-level architectural
decisions. Maintainer of open-source projects (go-micro, go-ovn).
In parallel I build my own commercial AI product — unistock.cloud
(https://unistock.cloud), a MOEX stock market analytics platform where I own everything
from architecture to monetisation. That is also where my hands-on LLM/RAG engineering
experience comes from (embeddings, vector search, MCP servers for AI agents), along with
language-engine work — I wrote a Pine Script v6 compiler and VM from scratch.

## Experience

### unistock.cloud
  Saint Petersburg, remote — https://unistock.cloud  
  Founder, architect, developer

  **Product and architecture:**
  * MOEX stock market analytics and trading-signal platform: web application, Telegram Mini
    App and an API for AI agents; a live commercial service with paid subscriptions
  * Microservice architecture: 33 Go 1.26 services (`go.unistack.org/micro/v5`), NATS
    JetStream as the event bus, PostgreSQL 18 / TimescaleDB (hypertables and continuous
    aggregates for 1h/4h/1d/1w/1mo candles), Redis, pgvector
  * Designed and built everything single-handedly: backend, frontend (React 18 +
    TypeScript + Vite, ECharts 6, i18next), infrastructure and billing

  **AI and LLM:**
  * Built a RAG pipeline over the news feed: when scoring an item, the prompt is enriched
    with similar past events — same ticker and sector — together with how the price reacted
    back then; embeddings live in pgvector and also drive semantic deduplication of the feed
  * Deployed my own embedding service (SGLang, llama.cpp) instead of an external API
  * Three interchangeable LLM backends behind a single interface: Claude API, a LiteLLM
    gateway (self-hosted Qwen3) and Ollama; request/reply over NATS JetStream
  * LLM sentiment scoring of news, AI digests per issuer, measurement of price reaction to
    an event, parsing of issuers' RAS/IFRS PDF reports
  * Built a realtime in-browser AI assistant with client-side tool calling: the LLM returns
    a tool call, the tool executes on the page itself and returns its result — so the
    assistant sees the state of that specific page and can navigate the site
  * Developed an MCP server (Model Context Protocol) with OAuth 2.1 and Dynamic Client
    Registration — external AI agents (Claude, ChatGPT) get market data, analytics and
    trading as ~28 tools, with a scope-based permission model and a fail-closed gate on
    anything touching real money
  * Designed the site for AI agents as a distinct audience: llms.txt and agent-skills are
    generated from the tool registry, and realtime subscription is reachable by agents that
    cannot send custom frames or headers
  * Adopted AI-assisted development as the primary process: spec → plan → implementation
    through subagent chains (Claude Code / Superpowers)

  **Virtual machine for Pine Script:**
  * Wrote a compiler and virtual machine for Pine Script v6 from scratch in Go
    (TradingView's scripting language, https://www.tradingview.com/pine-script-docs/):
    lexer → parser → semantic analysis → lowering → bytecode → VM, with bytecode
    serialisation and compilation caches
  * Optimised the hot execution path: the main levels script went from 530ms to 216ms and
    allocations dropped threefold; benchmarks on real data are pinned in tests
  * Assembled a parity corpus of 116 real Pine scripts (standard TradingView indicators,
    harmonic patterns) and verify results against reference output
  * Implemented `strategy.*` and backtesting: a Pine-faithful position model (net per
    symbol, trade journal, equity curve) and a bridge from strategies to real brokers
  * Language coverage: user types and functions, collections, drawing primitives, requesting
    data for another symbol and timeframe, v4 compatibility; user scripts run in a sandbox
    with execution limits
  * Users write their own indicators and strategies directly in the browser (CodeMirror 6
    editor); the platform's own trading logic also lives in Pine scripts behind preset
    flags rather than in Go

  **Market analytics:**
  * Volume Profile (POC/VAH/VAL), automatic support and resistance levels, swing and
    trendline detection, multi-timeframe analysis (daily + 4h + 1h), market context
    classification, presets per instrument liquidity
  * Harmonic pattern recognition (Gartley/Bat/Butterfly/Crab) on an ATR-adaptive zigzag
    with Fibonacci ratio bands and a win rate calibrated against history
  * Backtesting engine over as-of state snapshots with A/B re-checks of logic behind flags;
    found and fixed a dividend lookahead bug where reference data was being adjusted for
    *future* ex-dividend dates, turning one instrument's result from +73k into -393k
  * MOEX integration: historical candles, realtime order book over STOMP/WebSocket, futures
    open interest, AlgoPack premium datasets
  * Screener, market heatmap, issuer comparison, dividend calendar, sector analytics, and
    order-flow analysis (aggressor buy/sell split, order-book imbalance, anomaly alerts)

  **Brokers and trading:**
  * Integrations with 7 brokers, one service each: VTB, Sber, BCS, PSB, KIT Finance,
    GoInvest and a virtual one (paper trading), plus a QUIK/WebQuik client; for GoInvest I
    reverse-engineered its closed binary protocol
  * Implemented order types the brokers themselves do not offer: conditional orders on
    candle *close* (unlike an exchange stop, which triggers on any intrabar touch) and
    iceberg orders with my own slicing
  * Pre-trade risk control: buying power, sufficiency-of-funds ratio, risk coverage norms,
    margin headroom

  **Infrastructure, security, monetisation:**
  * Cloudflare: WAF, Cache Rules, R2 for static assets and bundles, Zaraz analytics fanning
    out to GA4 and Yandex Metrica, nonce-based CSP, a separate test contour
  * Authentication and authorisation: OAuth (Google / VK / Mail.ru), Telegram MTProto and
    initData, WebAuthn/passkeys, API tokens, Casbin RBAC; sessions as a Redis cache on top
    of Postgres as the source of truth
  * Notifications: Web Push, DKIM-signed email, Telegram (Bot API and MTProto) through a
    shared dispatcher
  * Paid subscriptions via YooKassa: a daily debit model against an internal balance,
    idempotency through a debits hypertable, a monthly consolidated receipt, refund
    handling, and compliance with Russian fiscal-receipt law (54-FZ)
  * SEO/GEO optimisation for both search engines and AI answers: server-rendered shell,
    sitemaps including Google News, an IndexNow pinger; i18n (ru/en) with translations on CDN

### ForteBank.kz
  Almaty (Kazakhstan), remote  
  Technical lead of the development function

  **Leadership and process:**
  * Conducted 35+ technical interviews of Go and DevOps engineers; defined the candidate
    evaluation criteria and the technical assignment templates
  * Wrote the Definition of Ready (DOR) and Definition of Done (DOD) for the team's
    services — standardising both task acceptance and the path to production
  * Led a team of 2 engineers: task decomposition, code review, mentoring, and enforcement
    of architectural consistency

  **Technical achievements:**
  * Designed and implemented (together with the team) a high-load API Gateway in Go:
    - serves 200+ microservices at 1,200 RPS
    - translates synchronous REST/gRPC requests into Kafka topics and returns the response
      to the client (async-to-sync bridge over a message queue)
    - gRPC Streaming support over Kafka
    - transparent gRPC↔gRPC and REST↔gRPC proxying
    - a hook system at every request-processing stage (pre/post-processing pipeline)
    - smart routing and response caching
    - despite the service being stateful, a fault-tolerant 4-pod cluster with client
      connection state synchronised across nodes
  * Built an OAuth2-compatible authorisation service supporting a custom flow (an
    authentication process configurable to the bank's requirements)
  * Designed a dynamic configuration loading architecture (hot reload without restarting
    services — log level, routing parameters and more)
  * Designed the interaction architecture between the platform and the mobile application
  * Ran R&D on adopting HTTP/3 (QUIC + gRPC) for mobile clients: protocol evaluation,
    prototyping, performance analysis
  * Introduced AI-assisted development into the team's workflow: using LLM agents (Claude /
    Superpowers) to draft plans and technical specifications, implement tasks through
    subagent chains, write unit tests, find bugs in the framework and develop new framework
    features

### portals.tg
  Remote  
  CTO (consulting)

  * Ran a system performance audit: identified bottlenecks, restored the project to stable
    operation, optimised critical code paths
  * Built a PostgreSQL library on top of Yandex HA-SQL and pgxpool: implemented smart query
    routing that considers not only the node role (primary/standby) but also its current
    load and response latency
  * Designed and executed a plan to reduce server infrastructure CAPEX in Google Cloud by
    moving part of the load onto dedicated servers
  * Conducted technical interviews of DevOps engineers and developers, onboarded new team
    members

### BerekeBank.kz (formerly Sberbank Kazakhstan)
  Almaty (Kazakhstan)  
  Head of microservice development, technology development department

  * Developed an authentication service
  * Contributed to planning the OpenShift-based microservice platform architecture
  * Developed a microservice for automated acquiring enrollment
  * Developed a microservice for push notifications on card transactions
  * Developed a synchronisation microservice from qpragma (Progress) into Oracle with
    intermediate processing (micro + Kafka)
  * Developed a card-processing microservice (Way4, ISO 8583)
  * Developed an API gateway microservice (JWT validation, routing to microservices,
    message auditing into Kafka, asynchronous messaging over WebSocket)
  * Modified the micro framework to watch configuration changes (Consul/Vault) and
    reconfigure services at runtime (e.g. log level)
  * Interviewed DevOps engineers and Go developers
  * Trained the bank's Java developers to write microservices on top of micro

### [xxx]bank.ru
  Moscow  
  Microservice development consultant, go-micro (micro) framework

  * Built a converter service migrating client data from Oracle to PostgreSQL
    (XML → JSON using protobuf, XPath, Go)
  * Developed services and advised on migrating banking processes from Siebel and Oracle
    to PostgreSQL and microservices
  * Made numerous fixes to go-micro and go-plugins to reduce memory consumption and
    improve throughput
  * Wrote a go-micro plugin for the Kafka broker based on segmentio/kafka-go
  * Delivered many framework improvements (encoding/decoding, batch processing, metrics,
    performance)
  * Built a card-processing service (Tieto, ISO 8583)
  * Trained the bank's developers to write microservices on top of micro and helped them
    resolve performance problems

### unistack.org
  Saint Petersburg  
  Owner, system administrator, lead developer

  * Forked go-micro (micro) and began actively developing and maintaining it
  * Wrote a generator for the libvirt D-Bus library (Go)
  * Fixed and improved go-ovn, the Open vSwitch OVN (Open Virtual Network) management
    library (Go)
  * Became an official maintainer of the go-ovn repository alongside engineers from eBay
  * Wrote a library for reading Ceph CRUSH map files in json/text/binary form (Go)
  * Building a server management system on microservices (Go)
  * Revived maintenance of go-rfb, a VNC library (Go)
  * Bug fixes and improvements to go-micro
  * Became an official maintainer of go-micro
  * Improved various go-micro subsystems (logger, api, gRPC client/server, Prometheus
    wrapper and others)

### clodo.ru / simplecloud.ru
  Saint Petersburg  
  System administrator, lead developer, chief software specialist

  * Deployed an OpenStack Swift segment in Saint Petersburg for geo-distributed object
    storage
  * Single-handedly administered 420+ servers of every kind (databases, virtualisation,
    PHP applications, backup, networking, CI/CD) across 4 data centres in two Russian cities
  * Reviewed and tested Opscode Chef recipes, verified fixes and wrote my own (Ruby)
  * Migrated running production services onto new hardware and software with no downtime
  * Rewrote the entire server configuration system from Opscode Chef to SaltStack, rolling
    SaltStack out incrementally on live servers still managed by Chef (Python, Ruby)
  * Planned and built the VM hosting infrastructure for mass-market use
    (clodo.ru / simplecloud.ru)
  * Designed and tested live migration of customer VMs between two data centres (Oversun
    Mercury → IXcellerate) over GRE tunnels and NBD with no downtime
  * Carried out a fleet-wide hypervisor migration (Xen → KVM) with automated VM conversion
    (Bash)
  * Built read-only mounting of an http/https address into a local path for rclone (FUSE,
    supporting Apache/nginx directory listing formats, Go)
  * Wrote Tight PNG encoding support for node-rfb2 (Node.js)
  * Added DHCP packet support to the Ogo OpenFlow controller and fixed its OpenFlow 1.0
    packet parsing (Go)
  * Added DHCP packet support to gopacket and wrote initial OpenFlow support (Go)
  * Wrote an automated OS installer for customer VMs that decompressed the image on the fly
    and skipped its zero blocks to cut provisioning time (used before QEMU learned to
    ignore or unmap zero writes) (Go)
  * Wrote many fixes for Packer's QEMU builder plus several post-processors that were
    merged upstream (Go)
  * Integrated Packer into the image build system for both customer and internal servers
    (databases, virtualisation, web applications, etc.)
  * Wrote a Linux kernel module for dynamic VM memory management (a VM's maximum memory
    changed with its actual usage) (C)
  * Built online VM disk resizing in both directions at boot time (Bash, initramfs)
  * Wrote a VNC proxy with http/https client authorisation a year before DigitalOcean
    announced the same capability, and added Supermicro ATEN encoding support with automatic
    conversion to raw encoding for ordinary VNC clients (Go)
  * Wrote an IPv4 DHCP and IPv6 RA server integrated with libvirt through domain metadata (Go)
  * Ported coreos-cloudinit to FreeBSD, added a CGO-free build and FreeBSD slice resizing (Go)
  * Started integrating the JUJU application deployment system to give customers
    ready-configured, extensible applications
  * Contributed fixes to the Sheepdog software-defined storage (C)
  * Developed a Raft cluster driver for Sheepdog as a corosync replacement (C)
  * Worked with Open vSwitch, participated in mailing list discussions, helped fix and test
    other people's patches
  * Wrote many build scripts for Exherbo Linux
  * Added tap device creation support to libvirt, along with the ability to specify IP
    addresses and routes through libvirt (C)
  * Wrote a dracut module for PXE + squashfs boot with overlayfs support (Bash)
  * Wrote an FTP server backed by OpenStack Swift with http/https API authorisation (Go)
  * Wrote many Opscode Chef recipes for server configuration (Ruby)
  * Wrote and upstreamed several patches to Opscode Chef (Ruby)
  * Wrote and upstreamed several patches to SaltStack (Python)
  * Designed and rolled out an encrypted VM offering for customers to meet Russian personal
    data law 152-FZ (ALT Linux, Bash, C)
  * Managed the technical support department: hiring, and handling escalated customers
    personally in crisis situations
  * Conducted many interviews for technical support and system administrator positions
  * Have experience handling serious disciplinary situations, including dismissals during a
    period critical for the company, and covering more junior roles myself — I worked for a
    month combining system administrator, head of support and support agent duties, which
    earned appreciative customer feedback

### timeweb.ru
  Saint Petersburg  
  System administrator

  * Sped up the mail system by putting nginx in front of it, reducing resource usage, with
    client authorisation over http/https
  * Began rolling out bogofilter as a spam defence in place of SpamAssassin
  * Wrote a patch exposing the currently processed request in the Apache process list
    (setproctitle) (C)
  * Wrote a PHP patch overriding the built-in mail function with a custom one that logged a
    full backtrace to syslog before calling the original (C)

### vk.com
  Saint Petersburg  
  System administrator

  * Helped administer 2,500+ servers across multiple data centres
  * Replicated databases (master-slave) and restored them from backups
  * Attempted a rewrite of the video transcoding system for the vkadre.ru project (PHP)

### peterhost.ru
  Saint Petersburg  
  System administrator, head of the shared hosting department

  * Monitored shared hosting services (MySQL, nginx, Apache, Exim) and wrote Nagios plugins
  * Tracked bugs in the open-source products the company relied on, applied patches and
    liaised with upstream developers
  * Fixed customers' scripts and answered their questions
  * Built a system for moving customer files between servers — an analogue of live migration
    before containers and virtualisation
  * Migrated the shared hosting platform from FreeBSD to Gentoo Linux
  * Trained new technical support staff
  * Evaluated cluster filesystems for shared hosting (GFS2, OpenAFS)

## Education
* Higher education, ITMO University, graduated 2009, software engineer
* Postgraduate studies (not completed), Peter the Great St. Petersburg Polytechnic
  University, 3 years; dissertation topic: "Security analysis in a multi-agent system"
* Professional development: Inspiring Management, 2008

## Key skills
* **Management and process:** conducting technical interviews, establishing DOR/DOD, task
  decomposition, code review, mentoring developers, managing technical debt
* **Architecture:** microservices, event-driven architecture (Kafka, NATS JetStream), API
  Gateway patterns, OAuth2/OIDC/OAuth 2.1, gRPC, HTTP/3 (QUIC), configuration hot reload,
  stateful clusters, time-series data (TimescaleDB)
* **AI/LLM:** RAG pipelines, embeddings and vector search (pgvector), MCP servers and OAuth
  for AI agents, LLM orchestration (Claude API, LiteLLM, Ollama), self-hosted inference
  (SGLang, llama.cpp), AI-assisted development through subagent chains
* **Languages and translators:** Pine Script v6 compiler and VM from scratch (lexer,
  parser, semantic analysis, bytecode, hot-path optimisation)
* **Programming languages:** Go (primary, 10+ years), C, Python, Ruby, Bash,
  TypeScript/React
* **Infrastructure:** Kubernetes/OpenShift, Consul, Vault, PostgreSQL/TimescaleDB, Oracle,
  Kafka, NATS, Redis, Cloudflare (WAF, R2, Zaraz)
* **Open Source:** maintainer of go-micro / go-ovn, contributor to Packer, SaltStack,
  Opscode Chef
* **Spoken languages:** Russian (native), English (intermediate — technical documentation,
  mailing lists)

## About me
I am looking for a CTO, technical lead or head of development position.
I am ready to combine deep technical work with team management and building out the
development process.  
I prefer remote work and dislike spending time commuting.  
I follow developments in high-load systems, distributed databases and network protocols.  
I have worked with many Linux distributions: Gentoo, Fedora, CentOS, Debian, Ubuntu,
Exherbo, Slackware, Arch Linux — as well as FreeBSD.  
I prefer to program in Go; I can also work in Ruby, Python, C and PHP.  
My live product — a MOEX market analytics platform with AI analytics and an API for AI
agents: https://unistock.cloud  
GitHub profile with some of my work: https://github.com/unistack-org  
