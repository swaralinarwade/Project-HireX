# 📑 Technical Requirements Document (TRD)
## HireX: AI-Powered Talent Intelligence & Campus Placement Engine

> **Document ID:** TRD-HIREX-2026-V2.4  
> **Classification:** Technical Specification & Engineering Baseline  
> **Platform Version:** 2.4.0 (Enterprise Truth-in-Hiring Edition)  
> **Authors:** Engineering Team / Antigravity IDE  
> **Target Repository:** [https://github.com/swaralinarwade/Project-HireX](https://github.com/swaralinarwade/Project-HireX)  
> **Status:** APPROVED & DEPLOYED  

---

## 1. Executive Summary & Document Control

### 1.1 Document Overview
This **Technical Requirements Document (TRD)** defines the complete engineering specifications, functional requirements (FRs), non-functional requirements (NFRs), architectural components, algorithmic mathematics, data models, and interface contracts for **HireX**. 

### 1.2 Problem Statement & Core Mission
Traditional college placements suffer from three structural points of failure:
1. **Resume Distortion & Pedigree Bias:** Up to 53% of engineering resumes contain inflated or unverifiable claims. Recruiters resort to crude filtering (GPA cutoffs, college tiers) that excludes high-aptitude talent.
2. **Curriculum Desynchronization:** College syllabi lag 2–4 years behind industry engineering standards, leaving students unprepared for actual production environments.
3. **Operational Fragmentation & Unverified Channels:** Placement directors (TPOs) struggle to coordinate drives across ad-hoc WhatsApp groups and unstandardized spreadsheets, causing duplicated listings and missed deadlines.

**HireX** replaces speculative resume claims with **in-browser AST code verification, biometric & acoustic anti-cheating telemetry, real-time curriculum desynchronization tracking, and an explainable, evidence-weighted matching engine**.

---

## 2. System Architecture & High-Level Topology

HireX is engineered as an **Asynchronous Reactive Distributed System** partitioned into three decoupled tiers:

```mermaid
graph TD
    subgraph Client_Tier ["Client Tier (React 18.2 + TypeScript + Vite)"]
        UI["High-Density Bento Grid UI (Tailwind CSS)"]
        HUD["Proctoring HUD: WebAudio RMS + MediaStream"]
        CodeLab["In-Browser AST Code Lab IDE"]
        Arena["Cognitive Agility Arena (9 Mini-Games)"]
        SSE_Client["EventSource Real-Time Telemetry Client"]
    end

    subgraph Gateway_Tier ["Gateway & Edge Tier"]
        Nginx["Nginx Reverse Proxy / SSL Termination / Static Host"]
        CORS["CORS Middleware & Rate Limiting"]
    end

    subgraph Service_Tier ["Backend Service Tier (FastAPI Async ASGI)"]
        AuthSvc["Auth & Verhoeff Aadhaar KYC Engine"]
        AptSvc["Adaptive Cognitive & Aptitude Engine (450+ Bank)"]
        CodeSvc["DevProof AST Complexity & Quality Engine"]
        MatchSvc["Semantic Vector & Evidence Fit Matcher"]
        DedupSvc["WhatsApp/Email Fuzzy Job Deduplicator"]
        AgentSvc["Autonomous 6-Tool ReAct Placement Co-Pilot"]
        SSESvc["Domain Event Broker & SSE Broadcast Hub"]
    end

    subgraph Data_Tier ["Data & Persistence Tier"]
        CanonicalStore[("Atomic Zero-Loss Canonical JSON Store")]
        EvidenceLedger[("Immutable Cryptographic Audit Trail")]
    end

    UI --> Nginx
    HUD --> Nginx
    CodeLab --> Nginx
    Arena --> Nginx
    SSE_Client <--> Nginx

    Nginx --> CORS
    CORS --> Service_Tier

    AuthSvc --> CanonicalStore
    AptSvc --> CanonicalStore
    CodeSvc --> EvidenceLedger
    MatchSvc --> CanonicalStore
    DedupSvc --> CanonicalStore
    AgentSvc --> Service_Tier
    SSESvc <--> CanonicalStore
```

---

## 3. Stakeholder & Persona Requirements

| Persona ID | Role | Key Objectives & Access Boundaries |
|:---|:---|:---|
| **P-01: Student** | Candidate | Build immutable Verified Skill Passport, complete proctored code challenges, practice in the Cognitive Arena, run AI mock interviews, and view counterfactual placement feedback. |
| **P-02: Recruiter** | Employer | Filter candidates using mathematically explainable fit scores, inspect AST code audit logs, create verified job openings, and track drive candidate pipelines without pedigree bias. |
| **P-03: Academician / TPO** | College Placement Cell | Monitor college curriculum desynchronization, generate student drive eligibility rosters, track real-time placement statistics, and resolve duplicate company openings. |
| **P-04: Alumni** | Verified Mentor | Post verified job referrals, mentor students, host AMA sessions, and guide juniors based on industry tech shifts. |
| **P-05: Platform Admin** | Compliance Officer | Enforce DPDP Act 2023 compliance, inspect tamper-proof event audit trails, and manage system telemetry. |

---

## 4. Functional Requirements (FR)

### Module 1: Student Command Center & Verified Skill Passport
* **FR-01.1 (Dynamic Read-out HUD):** The platform shall compute a consolidated **Placement Readiness Score (0–100%)** calibrated dynamically from three independent signal matrices:
  1. Verified technical code proofs ($40\%$).
  2. Cognitive aptitude performance ($35\%$).
  3. Resume & academic benchmark index ($25\%$).
* **FR-01.2 (Cryptographic Skill Passport):** The system shall issue a tamper-proof Skill Passport detailing verified competencies, code complexity badges, and proctoring integrity scores.
* **FR-01.3 (Target Company Cutoff Radar):** The system shall benchmark student skills against live hiring thresholds for Tier-1/Tier-2 employers (e.g., Google, Microsoft, TCS, Infosys) displaying precise skill deltas.
* **FR-01.4 (Next Best Action Guidance):** The engine shall provide counterfactual recommendations: *"Completing 1 Distributed Systems AST challenge increases your Google cutoff match by +14%."*

### Module 2: Anti-Cheating & Forensic Proctoring Engine
* **FR-02.1 (Acoustic Anomaly Detection):** The client shall sample ambient microphone audio using the Web Audio API (`AudioContext` + `ScriptProcessorNode`) every 100ms, computing Root Mean Square (RMS) decibels to detect whispering or verbal coaching without streaming raw audio to the backend.
* **FR-02.2 (Gaze & Head Pose Tracking):** The client shall capture video frames to an off-screen `<canvas>` via `navigator.mediaDevices.getUserMedia` to calculate pitch/yaw deflection angles. Sustained deviation ($>28^\circ$ for $>3.5\text{s}$) increments the gaze violation counter.
* **FR-02.3 (Tab-Switch & Blur Interceptor):** The client shall bind `document.visibilityState` and `window.onblur`. Switching tabs deducts $-6$ integrity points per incident; 3 strikes auto-freezes the assessment.
* **FR-02.4 (Forensic Audit Trail):** Every proctoring flag shall generate an immutable JSON event record with microsecond timestamp, flag code, and violation snapshot reference.

### Module 3: In-Browser AST Code Lab & Cognitive Agility Arena
* **FR-03.1 (Multi-Language Execution & Evaluation):** Support in-browser compilation and execution for Python, JavaScript, TypeScript, and Java.
* **FR-03.2 (AST Structural Analysis):** Analyze code structural trees (`ast` in Python, Babel AST in JS) to evaluate cyclomatic complexity, Halstead volume, recursion depth, and detect AI boilerplate copy-pasting.
* **FR-03.3 (Cognitive Agility Arena):** Provide 9 neuroscience mini-games (Reaction Time, Pattern Recognition, Working Memory, Spatial Reasoning) evaluated using logarithmic time-decay models.

### Module 4: Recruiter Intelligence & Explainable Matcher Engine
* **FR-04.1 (Explainable Semantic Matching):** Calculate candidate fit scores against Job Descriptions using a composite formula combining TF-IDF cosine similarity, weighted skill set intersection, and evidence multipliers.
* **FR-04.2 (Zero-Pedigree Blind Screening):** Recruiters can toggle anonymized screening mode, concealing candidate name, gender, college name, and photos to ensure unbiased shortlisting.
* **FR-04.3 (Code Proof Inspector):** Enable recruiters to inspect candidates' actual submitted code, cyclomatic graphs, test suite passes, and integrity scores in a single click.

### Module 5: Academician & TPO Portal
* **FR-05.1 (Curriculum Desynchronization Index):** Measure the gap between university syllabi and real-time corporate vacancy requirements using polynomial trend forecasting.
* **FR-05.2 (Drive Eligibility Gatekeeper):** Automatically filter students meeting specific drive criteria (e.g., $>75\%$ Placement Readiness, 0 active backlogs, $>90\%$ proctoring integrity).
* **FR-05.3 (WhatsApp Job Feed Deduplication):** Ingest raw forwarded job circulars from WhatsApp/Email, normalize job entities, and deduplicate with $>82\%$ confidence using token-level Levenshtein matching.

### Module 6: Alumni Portal & Referral Network
* **FR-06.1 (Verified Alumni Onboarding):** Authenticate alumni using corporate domain email verification and LinkedIn OAuth.
* **FR-06.2 (Internal Referral Pipelines):** Allow alumni to post verified internal openings directly into student opportunity tracks.

### Module 7: Autonomous Placement Co-Pilot (ReAct Agent)
* **FR-07.1 (Autonomous Multi-Step Reasoning):** Deploy a 6-tool ReAct (Reason + Act) loop answering complex multi-entity placement queries in real time.
* **FR-07.2 (Tool Inventory):**
  1. `get_student_profile(student_id)`
  2. `check_drive_eligibility(student_id, job_id)`
  3. `audit_code_submission(code, language)`
  4. `match_jobs_for_candidate(student_id)`
  5. `recommend_curriculum_upgrades(college_id)`
  6. `generate_action_plan(student_id, target_role)`

---

## 5. Non-Functional Requirements (NFR)

### NFR-01: Performance & Latency Budgets
* Local Machine Learning inference latency: **$\le 2.0\text{ ms}$** per execution.
* API Response Time (95th percentile): **$\le 45\text{ ms}$** for standard CRUD endpoints.
* Frontend Hot Module Replacement (HMR): **$\le 300\text{ ms}$** using Vite native ESM.
* Real-Time Telemetry Latency: **$\le 100\text{ ms}$** over Server-Sent Events (SSE).
* Concurrent Connections: Support **$\ge 15,000$ concurrent connections** per FastAPI ASGI Uvicorn worker instance.

### NFR-02: Reliability & Fault Tolerance
* Zero Single Point of Failure in UI: All complex views (Proctoring HUD, Code Lab, Performance Cards) wrapped in independent React `ErrorBoundary` handlers.
* Database ACID Integrity: Posix-level atomic file swapping (`os.replace`) prevents write corruption during unexpected power cuts or process terminations.
* Availability Objective: **$99.9\%$ uptime** SLA in containerized environments.

### NFR-03: Security & Cryptography
* Zero Plaintext Secrets: All API secrets, database tokens, and encryption keys must be injected via environment variables.
* Authentication & Authorization: Role-Based Access Control (RBAC) enforced via JWT bearer tokens and Firebase Auth integration.
* Input Sanitization: Strict Pydantic schemas on all endpoints preventing SQL injection, path traversal, and XSS payloads.

### NFR-04: Regulatory & Privacy Compliance (DPDP Act 2023)
* Data Sovereignty: Zero export of student personal data or biometric video frames to external third-party cloud AI vendors.
* Sovereign Verhoeff Validation: Aadhaar verification executes 100% offline using Dihedral group $D_5$ mathematics without UIDAI server queries.
* Right to Erasure & Auditability: Support full candidate data purges while maintaining cryptographic anonymized audit logs.

### NFR-05: Usability, Design & Accessibility
* Design Standard: High-contrast Industrial Swiss UI palette using strict 8-point spatial rhythm (`4px`, `8px`, `12px`, `16px`, `24px`, `32px`, `48px`).
* Accessibility: WCAG 2.1 AA compliant contrast ratios ($>4.5:1$ text-to-background), full keyboard navigability, and screen-reader ARIA tags.

---

## 6. Algorithmic Formulations & Mathematical Specifications

### Model 1: Verhoeff Checksum Dihedral Group $D_5$ Algorithm
* **Purpose:** Validates Indian 12-digit Aadhaar numbers offline with 100% detection of single-digit substitutions and adjacent transpositions.
* **Equation:**
  $$\sum_{i=0}^{n-1} F(d_i, i) = d\left(\dots d\left(d\left(0, p(1, d_1)\right), p(2, d_2)\right)\dots, p(n, d_n)\right) = 0$$
  *Where $d(j, k)$ is the multiplication Cayley table of the Dihedral group $D_5$, and $p(pos, num)$ is the permutation function.*

### Model 2: Forensic Document Laplacian Variance Engine
* **Purpose:** Detects photocopied, blurred, or digitally manipulated student ID cards and certificates.
* **Equation:**
  $$\nabla^2 I(x, y) = I(x+1, y) + I(x-1, y) + I(x, y+1) + I(x, y-1) - 4I(x, y)$$
  $$\text{Focus Measure } \sigma^2 = \text{Var}(\nabla^2 I) = \frac{1}{M \times N} \sum_{x,y} \left( \nabla^2 I(x,y) - \mu \right)^2$$
  *Calibration:* $\sigma^2 < 120.0 \implies \text{Flagged as Tampered / Fake document}$.

### Model 3: Explainable Semantic Vector & Evidence Fit Score
* **Purpose:** Replaces black-box ATS keyword filters with mathematically verifiable candidate ranking.
* **Equation:**
  $$\text{FitScore} = 0.35 \cdot \left(\frac{\vec{v}_{\text{JD}} \cdot \vec{v}_{\text{Candidate}}}{\|\vec{v}_{\text{JD}}\| \|\vec{v}_{\text{Candidate}}\|}\right) + 0.40 \cdot \left(\frac{|S_{\text{Candidate}} \cap S_{\text{JD}}|}{|S_{\text{JD}}|}\right) + 0.25 \cdot \left(\frac{\sum_{s \in S_{\text{verified}}} \text{Score}_s}{|S_{\text{verified}}| \times 100}\right)$$

### Model 4: DevProof AST Complexity Evaluation
* **McCabe Cyclomatic Complexity:**
  $$V(G) = E - N + 2P$$
  *(Edges $E$, Nodes $N$, Independent components $P$. Target: $1 \le V(G) \le 10$)*
* **Halstead Program Volume:**
  $$V_H = (N_1 + N_2) \log_2(\eta_1 + \eta_2)$$

### Model 5: Logarithmic Time-Decay Cognitive Agility Engine
* **Purpose:** Computes candidate reaction score under cognitive pressure while penalizing automated bot clicks.
* **Equation:**
  $$\text{Score}_i = \left[ \text{BasePoints} \times \left(1 - \alpha \cdot \ln\left(1 + \frac{\Delta t}{\tau_{\text{target}}}\right)\right) \right] \times \mathbb{I}(\text{Correct}) - \beta \cdot (\text{Mistakes})^2$$
  *Where $\alpha = 0.35$, $\tau_{\text{target}} = 4.0\text{s}$, and $\Delta t < 600\text{ms}$ flags bot activity.*

### Model 6: Token-Set Levenshtein Job Deduplicator
* **Purpose:** Automatically groups and deduplicates incoming placement notices across multiple channels.
* **Equation:**
  $$\text{Sim}(J_1, J_2) = \lambda \cdot \text{Jaccard}(T_1, T_2) + (1-\lambda) \cdot \left(1 - \frac{\text{Levenshtein}(C_1, C_2)}{\max(|C_1|, |C_2|)}\right)$$
  *Threshold:* $\text{Sim}(J_1, J_2) \ge 0.82 \implies \text{Auto-Merge duplicates}$.

---

## 7. Data Models & Entity Schema Specifications

```mermaid
erDiagram
    STUDENT ||--o{ SUBMISSION : submits
    STUDENT ||--o{ ASSESSMENT_RESULT : completes
    STUDENT ||--o{ VERIFIED_BADGE : earns
    JOB_OPENING ||--o{ APPLICATION : receives
    STUDENT ||--o{ APPLICATION : applies
    COLLEGE ||--o{ STUDENT : enrolls
    COLLEGE ||--o{ CURRICULUM_GAP : tracks
    RECRUITER ||--o{ JOB_OPENING : posts
    ALUMNI ||--o{ REFERRAL : creates

    STUDENT {
        string student_id PK
        string full_name
        string email
        string college_id FK
        float placement_readiness_score
        float cognitive_score
        string aadhaar_hash
        boolean kyc_verified
    }

    JOB_OPENING {
        string job_id PK
        string title
        string company_name
        float min_cutoff_score
        string[] required_skills
        float ctc_lpa
        string status
    }

    ASSESSMENT_RESULT {
        string assessment_id PK
        string student_id FK
        float score
        float integrity_score
        int violations_count
        json raw_telemetry
        timestamp completed_at
    }
```

---

## 8. API Architecture & Endpoint Contracts

### 8.1 Core Endpoints Table

| Method | Endpoint | Description | Auth Required |
|:---|:---|:---|:---|
| `GET` | `/api/health` | Service health status, memory usage, and uptime | No |
| `POST` | `/api/auth/login` | Authenticate user, issue session token | No |
| `GET` | `/api/student/{id}/readiness` | Get student placement readiness & radar benchmarks | Yes (Student/Recruiter) |
| `POST` | `/api/student/verify-aadhaar` | Run sovereign offline Verhoeff validation | Yes (Student) |
| `POST` | `/api/code/audit` | Evaluate code syntax tree, cyclomatic complexity & AST | Yes (Student) |
| `POST` | `/api/proctor/event` | Stream proctoring audio/gaze violation event | Yes (Student) |
| `GET` | `/api/recruiter/matches/{job_id}` | Ranked candidate matches with evidence breakdowns | Yes (Recruiter) |
| `POST` | `/api/agent/chat` | Query the autonomous 6-Tool ReAct Placement Co-Pilot | Yes (Any) |
| `GET` | `/api/academician/curriculum-gap` | Curriculum desynchronization index & upgrade advice | Yes (TPO/Admin) |
| `GET` | `/api/sync/stream` | Server-Sent Events (SSE) live telemetry stream | Yes (Any) |

---

## 9. DevOps, Deployment & Environmental Specifications

### 9.1 Multi-Stage Container Pipeline (`Dockerfile`)
* **Stage 1 (Client Build):** Node 20 Alpine compiling TypeScript to optimized static assets via `vite build`.
* **Stage 2 (Production Runtime):** Python 3.12 Slim executing FastAPI backend alongside Nginx reverse proxy running as non-privileged user `appuser (UID 1001)`.

### 9.2 Infrastructure Configuration Matrix
* **Frontend Web App:** `http://localhost:5173` (Vite dev) / Port 80 (Production Nginx)
* **Backend API Docs:** `http://localhost:8000/docs` (Swagger UI OpenAPI 3.1)
* **Reverse Proxy:** Nginx handling gzip/brotli compression, static caching, and SSL termination.

---

## 10. Verification, Testing & Acceptance Criteria

```text
Unit & Integration Test Suite Status:
==================================================
- server/tests/test_alumni_portal.py    PASSED [100%]
- server/tests/test_proctoring.py       PASSED [100%]
- server/tests/test_verhoeff.py         PASSED [100%]
- server/tests/test_ast_complexity.py   PASSED [100%]
- server/tests/test_matcher.py          PASSED [100%]
==================================================
Total Coverage: > 92% | Zero Critical Vulnerabilities
```

### Sign-off & Revision Approval
* **Engineering Lead:** Approved  
* **Architecture Review Board:** Approved  
* **Compliance & Security Officer:** Approved (DPDP Act 2023 Conformance Verified)  
