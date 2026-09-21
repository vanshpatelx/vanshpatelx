<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/vanshpatelx/vanshpatelx/main/assets/header-dark.svg">
    <img src="https://raw.githubusercontent.com/vanshpatelx/vanshpatelx/main/assets/header-light.svg" alt="Vansh Patel — founder and engineer" width="100%">
  </picture>
</p>

<p align="center">
  <a href="https://oceanlab.in"><img src="https://img.shields.io/badge/Oceanlab-oceanlab.in-161B22?style=flat-square" alt="Oceanlab"></a>
  <a href="https://xocket.sh"><img src="https://img.shields.io/badge/Xocket-xocket.sh-161B22?style=flat-square" alt="Xocket"></a>
  <a href="https://watermelon.sh"><img src="https://img.shields.io/badge/Watermelon-watermelon.sh-161B22?style=flat-square" alt="Watermelon"></a>
  <a href="mailto:remotevansh@gmail.com"><img src="https://img.shields.io/badge/Email-remotevansh@gmail.com-161B22?style=flat-square&logo=gmail&logoColor=EA4335" alt="Email"></a>
</p>

I run three companies and still write the code. Backend services and the infrastructure under them — order matching in Go, event pipelines, Kubernetes, and lately native macOS in Swift. Most of what is on this profile is me taking a system apart to find out what it costs to keep it running.

---

## Ventures

### [Oceanlab](https://oceanlab.in) &nbsp;·&nbsp; enterprise software engineering, human + AI

We design, build and operate enterprise-grade software for organisations that cannot afford to get it wrong — the velocity of AI prototyping with the rigour of senior human engineers, and compliance-ready from day one: SOC 2, HIPAA, ISO 27001, GDPR, PCI DSS.

### [Xocket](https://xocket.sh) &nbsp;·&nbsp; the execution layer for modern teams

AI-native developers who operate *inside* a team rather than alongside it — people who understand the product, talk to non-technical stakeholders in their own language, and ship materially faster than a traditional contract team. Building, not polishing.

### [Watermelon](https://watermelon.sh) &nbsp;·&nbsp; design infrastructure for startups

Startups move fast until design becomes the bottleneck: fragmented tools, inconsistent UI, velocity dying at the worst possible moment. Watermelon replaces the stitched-together stack with one ecosystem — Studio, UI, Native, Showcase and AI.

---

## Products

### [Black Hole](https://github.com/vanshpatelx/blackhole) &nbsp;·&nbsp; `SwiftUI` &nbsp;·&nbsp; [getblackhole.app](https://getblackhole.app)

Your whole day, one hover away. Tasks, a focus timer, a daily notepad and today's calendar live inside the MacBook notch. Press <kbd>⌥</kbd><kbd>Space</kbd> anywhere and type *"call mika tomorrow at 3pm"* — the date and time get lifted out of the sentence and it becomes a task with a reminder. During a focus session the notch turns into a live island with a progress ring and countdown. Reads iCloud, Google, Outlook and subscribed calendars; unfinished tasks roll over on their own. Free, open source, and no data leaves the machine.

### [Otter](https://github.com/vanshpatelx/Otter) &nbsp;·&nbsp; `TypeScript`

A local-first control center for AI coding agents spread across several machines. Rather than remote-controlling a computer, you reconnect to a persistent workspace that still holds its agents, dev servers, browser sessions and project context. A Worker runs on each machine; the desktop app is the console. Transport is direct and encrypted — Tailscale, WireGuard, LAN or an SSH tunnel — with an optional stateless relay. No source, prompts or conversations are uploaded anywhere.

---

## How the flagship works

[**Opinex**](https://github.com/vanshpatelx/Opinex) is a real-time opinion trading platform: ten services across three languages, on Kubernetes. The interesting part isn't the service count — it's that the order path and the market-data path are deliberately separate, so a slow fan-out to thousands of WebSocket clients can never back-pressure the matching engine.

```mermaid
flowchart LR
  C(["Client"]) -->|place order| O["Order<br/>Py"]
  O -->|queue| E["Engine<br/>Go"]
  V["Event<br/>Py"] -->|market events| E
  subgraph settle["order path — durable, must not lose a fill"]
    T["Trade<br/>TS"] --> S["Settlement<br/>TS"] --> H["Holding<br/>Go"]
  end
  subgraph fan["market-data path — lossy, must not block"]
    M["WS Manager<br/>TS"] --> W["WS<br/>TS"]
  end
  E -->|fill| T
  E -->|ticks| M
  H --> D[("DB<br/>Server")]
  W -->|live book| C
  classDef hot stroke:#58A6FF,stroke-width:2.5px
  class E hot
```

Go for the hot path (matching, holdings), Python where the logic changes often (orders, market events), TypeScript at the edges. Docker Compose locally, unit → integration → E2E in CI, Kubernetes in cloud.

---

## Selected work

| Project | What it is | Stack |
| :--- | :--- | :--- |
| **[TradeEngine 2.0](https://github.com/vanshpatelx/TradeEngine2.0)** | Order matching engine rebuilt for throughput — the second attempt, after the first taught me where the time actually went | `Go` |
| **[benchmark](https://github.com/vanshpatelx/benchmark)** | Go vs Node under identical API load. Measured, rather than argued about | `Go` `Node` |
| **[multi-lang-turborepo](https://github.com/vanshpatelx/multi-lang-turborepo)** | One Turborepo driving Go, Rust, Python and TypeScript together — shared tasks, one `turbo dev` | `Turborepo` |
| **[AWS-K8s](https://github.com/vanshpatelx/AWS-K8s)** | Cluster bring-up on AWS from scratch, scripted | `Shell` `AWS` |
| **[CICD](https://github.com/vanshpatelx/CICD)** | Fully automated CI/CD environment, infrastructure as code | `Terraform` |
| **[Automated Blog System](https://github.com/vanshpatelx/AutomatedBlogCreationSystemWithApproval)** | Multi-agent writing pipeline: agents draft, Notion stores, a Telegram bot holds the approval gate before anything publishes | `Python` `AutoGen` `Gemini` |
| **[Learning Assistant](https://github.com/vanshpatelx/learningAssistant)** | Upload a book, get a tutor for it — retrieval over your own material | `LangChain` `FAISS` |
| **[xocket-website](https://github.com/vanshpatelx/xocket-website)** | Marketing site for Xocket — React 19, Vite, Tailwind v4, shadcn/ui | `React` `Vite` |
| **[MetaOffice](https://github.com/vanshpatelx/metaoffice)** | 2D metaverse office — own desks, meeting rooms, custom avatars | `TypeScript` |

---

## Toolkit

**Languages**&nbsp;&nbsp;
<img src="https://img.shields.io/badge/TypeScript-161B22?style=flat-square&logo=typescript&logoColor=3178C6" alt="TypeScript">
<img src="https://img.shields.io/badge/Go-161B22?style=flat-square&logo=go&logoColor=00ADD8" alt="Go">
<img src="https://img.shields.io/badge/Python-161B22?style=flat-square&logo=python&logoColor=FFD43B" alt="Python">
<img src="https://img.shields.io/badge/Swift-161B22?style=flat-square&logo=swift&logoColor=F05138" alt="Swift">
<img src="https://img.shields.io/badge/Java-161B22?style=flat-square&logo=openjdk&logoColor=white" alt="Java">
<img src="https://img.shields.io/badge/C++-161B22?style=flat-square&logo=cplusplus&logoColor=649AD2" alt="C++">

**Services & UI**&nbsp;&nbsp;
<img src="https://img.shields.io/badge/Node.js-161B22?style=flat-square&logo=nodedotjs&logoColor=5FA04E" alt="Node.js">
<img src="https://img.shields.io/badge/FastAPI-161B22?style=flat-square&logo=fastapi&logoColor=009688" alt="FastAPI">
<img src="https://img.shields.io/badge/React-161B22?style=flat-square&logo=react&logoColor=61DAFB" alt="React">
<img src="https://img.shields.io/badge/Next.js-161B22?style=flat-square&logo=nextdotjs&logoColor=white" alt="Next.js">
<img src="https://img.shields.io/badge/SwiftUI-161B22?style=flat-square&logo=swift&logoColor=F05138" alt="SwiftUI">
<img src="https://img.shields.io/badge/Tailwind-161B22?style=flat-square&logo=tailwindcss&logoColor=06B6D4" alt="Tailwind CSS">
<img src="https://img.shields.io/badge/Turborepo-161B22?style=flat-square&logo=turborepo&logoColor=EF4444" alt="Turborepo">
<img src="https://img.shields.io/badge/Bun-161B22?style=flat-square&logo=bun&logoColor=FBF0DF" alt="Bun">

**Infrastructure**&nbsp;&nbsp;
<img src="https://img.shields.io/badge/Docker-161B22?style=flat-square&logo=docker&logoColor=2496ED" alt="Docker">
<img src="https://img.shields.io/badge/Kubernetes-161B22?style=flat-square&logo=kubernetes&logoColor=326CE5" alt="Kubernetes">
<img src="https://img.shields.io/badge/AWS-161B22?style=flat-square&logo=amazonwebservices&logoColor=FF9900" alt="AWS">
<img src="https://img.shields.io/badge/Terraform-161B22?style=flat-square&logo=terraform&logoColor=844FBA" alt="Terraform">
<img src="https://img.shields.io/badge/GitHub_Actions-161B22?style=flat-square&logo=githubactions&logoColor=2088FF" alt="GitHub Actions">
<img src="https://img.shields.io/badge/Kafka-161B22?style=flat-square&logo=apachekafka&logoColor=white" alt="Apache Kafka">
<img src="https://img.shields.io/badge/RabbitMQ-161B22?style=flat-square&logo=rabbitmq&logoColor=FF6600" alt="RabbitMQ">
<img src="https://img.shields.io/badge/NGINX-161B22?style=flat-square&logo=nginx&logoColor=009639" alt="NGINX">

**Data & AI**&nbsp;&nbsp;
<img src="https://img.shields.io/badge/PostgreSQL-161B22?style=flat-square&logo=postgresql&logoColor=4169E1" alt="PostgreSQL">
<img src="https://img.shields.io/badge/MongoDB-161B22?style=flat-square&logo=mongodb&logoColor=47A248" alt="MongoDB">
<img src="https://img.shields.io/badge/Redis-161B22?style=flat-square&logo=redis&logoColor=FF4438" alt="Redis">
<img src="https://img.shields.io/badge/LangChain-161B22?style=flat-square&logo=langchain&logoColor=white" alt="LangChain">
<img src="https://img.shields.io/badge/Gemini-161B22?style=flat-square&logo=googlegemini&logoColor=8E75B2" alt="Gemini">

---

<details>
<summary><b>The numbers</b></summary>
<br>

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=vanshpatelx&label=Profile%20views&color=161b22&style=flat-square" alt="Profile views">
</p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=vanshpatelx&theme=github_dark">
    <img src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=vanshpatelx&theme=github" alt="Profile summary">
  </picture>
</p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=vanshpatelx&theme=github_dark">
    <img height="200" src="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=vanshpatelx&theme=github" alt="Repos per language">
  </picture>
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=vanshpatelx&theme=github_dark">
    <img height="200" src="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=vanshpatelx&theme=github" alt="Most committed languages">
  </picture>
</p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://streak-stats.demolab.com?user=vanshpatelx&hide_border=true&background=00000000&ring=58A6FF&fire=F85149&currStreakLabel=58A6FF&stroke=30363D&dates=8B949E&sideLabels=C9D1D9&currStreakNum=C9D1D9&sideNums=C9D1D9">
    <img src="https://streak-stats.demolab.com?user=vanshpatelx&hide_border=true&background=00000000&ring=0969DA&fire=CF222E&currStreakLabel=0969DA&stroke=D0D7DE&dates=57606A&sideLabels=1F2328&currStreakNum=1F2328&sideNums=1F2328" alt="Contribution streak">
  </picture>
</p>

<p align="center"><sub>Language breakdown reflects what my public code happens to be written in — not what I'm good at.</sub></p>

<!--
  The classic github-readme-stats cards are intentionally not used here: the public
  instance at github-readme-stats.vercel.app currently returns 503 DEPLOYMENT_PAUSED
  for every user, so those cards render as broken images. To bring them back, deploy
  your own instance (https://github.com/anuraghazra/github-readme-stats#deploy-on-your-own-vercel-instance)
  and point these URLs at it.
-->

</details>

<details>
<summary><b>The back catalogue</b> — 117 repos, and what they're for</summary>
<br>

Most of this profile is deliberate practice, kept public on purpose. Roughly:

- **Distributed systems** — [trading-system](https://github.com/vanshpatelx/trading-system), [exchange](https://github.com/vanshpatelx/exchange), [Microservices-Event-driven](https://github.com/vanshpatelx/Microservices-Event-driven), [Kafka](https://github.com/vanshpatelx/Kafka), [rabbitMQ](https://github.com/vanshpatelx/rabbitMQ), [websockets](https://github.com/vanshpatelx/websockets)
- **Infra & DevOps** — [devenv](https://github.com/vanshpatelx/devenv), [devOpsInfra](https://github.com/vanshpatelx/devOpsInfra), [DevSecOps](https://github.com/vanshpatelx/DevSecOps), [civoK8s](https://github.com/vanshpatelx/civoK8s), [etoepipeline](https://github.com/vanshpatelx/etoepipeline)
- **AI & ML** — [virtual-ai](https://github.com/vanshpatelx/virtual-ai), [MeetingAI](https://github.com/vanshpatelx/MeetingAI), [Movie-recommendation-system-ML](https://github.com/vanshpatelx/Movie-recommendation-system-ML), [SP-500-Market-Prediction](https://github.com/vanshpatelx/SP-500-Market-Prediction), [FaceMask-Detection-using-CNN](https://github.com/vanshpatelx/FaceMask-Detection-using-CNN)
- **SDKs & libraries** — [hashnodeSDK](https://github.com/vanshpatelx/hashnodeSDK), [E-commerce-SDK](https://github.com/vanshpatelx/E-commerce-SDK), [ReactLib](https://github.com/vanshpatelx/ReactLib)
- **Fundamentals** — [Data-Structures](https://github.com/vanshpatelx/Data-Structures), [Algos](https://github.com/vanshpatelx/Algos), [Question-Pattens](https://github.com/vanshpatelx/Question-Pattens), [DSA-Roadmap](https://github.com/vanshpatelx/DSA-Roadmap)

</details>

---

<p align="center">
  <a href="https://oceanlab.in"><b>Oceanlab</b></a> &nbsp;·&nbsp; <a href="https://xocket.sh"><b>Xocket</b></a> &nbsp;·&nbsp; <a href="https://watermelon.sh"><b>Watermelon</b></a><br><br>
  Building something hard, or want to build it together?<br>
  <a href="mailto:remotevansh@gmail.com"><b>remotevansh@gmail.com</b></a>
</p>
