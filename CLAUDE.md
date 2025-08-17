# TaskBuddy - Claude Code Project Memory

## Project Overview
TaskBuddy is an AI-powered personal productivity agent that centralizes email, calendar, and CRM management through a single Telegram interface.

## Current Status: Planning & Architecture Phase
- **Started:** 2025-08-16
- **Phase:** Requirements definition and technical planning
- **Next:** Local MVP development

## Technical Stack Decisions

### Core Architecture
- **Language:** Python 3.11+
- **Framework:** FastAPI + SQLAlchemy + Pydantic
- **Database:** SQLite (local) → PostgreSQL (production)
- **AI/LLM:** Ollama (local) → Groq API (production)
- **Bot Platform:** Telegram Bot API (python-telegram-bot)
- **Architecture Pattern:** Hexagonal (Ports & Adapters)

### Key Integrations
- **Gmail API:** Email reading, analysis, response suggestions
- **Google Calendar API:** Event scheduling, availability checks
- **HubSpot API:** Contact management, deal tracking
- **Telegram Bot API:** Primary user interface

### Development Strategy
- **Phase 1:** Local development with free tools (Ollama, SQLite)
- **Phase 2:** Cloud migration with minimal changes
- **Migration Path:** Provider abstraction for easy switching

## Project Costs Analysis
### Local Development: R$0/month
- Ollama (free)
- SQLite (free)
- Telegram Bot API (free)

### Production: ~R$70/month
- Groq API: ~R$20/month
- Server hosting: ~R$50/month
- All APIs: free tiers sufficient

## Agent Specialists Created
1. **api-integration-expert** - OAuth, Gmail/Calendar/HubSpot APIs
2. **python-ai-architect** - Architecture, FastAPI, LangChain patterns
3. **security-reviewer** - Security, compliance, data protection
4. **telegram-bot-specialist** - Bot UX, conversational design
5. **llm-workflow-designer** - AI workflows, RAG, prompt optimization
6. **context-keeper** - Project memory and session continuity

## Architecture Decisions Log

### ADR-001: Telegram over WhatsApp
**Decision:** Use Telegram Bot API instead of WhatsApp Business API
**Rationale:** 
- WhatsApp Business API costs R$150+/month
- Requires business approval from Meta
- Telegram is free, no limits, better developer experience
**Status:** Approved

### ADR-002: Python over Node.js
**Decision:** Python as primary backend language
**Rationale:**
- Superior AI/ML ecosystem (LangChain, transformers)
- Better data processing libraries
- More natural for email/text analysis
- Easier local AI model integration
**Status:** Approved

### ADR-003: Local-first Development
**Decision:** Start with local tools, migrate to cloud later
**Rationale:**
- Zero initial costs for validation
- Faster development cycle
- Easy debugging and iteration
- Clear migration path designed upfront
**Status:** Approved

## Development Commands
```bash
# Setup virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Install dependencies
pip install fastapi uvicorn sqlalchemy pydantic python-telegram-bot langchain

# Run development server
uvicorn main:app --reload

# Database migrations
alembic upgrade head

# Run tests
pytest

# Lint code
ruff check .
black .
mypy .
```

## API Credentials Status
- [ ] Gmail API - Need to setup OAuth 2.0
- [ ] Google Calendar API - Same OAuth scope as Gmail
- [ ] HubSpot API - Need developer account and API key
- [ ] Telegram Bot API - Need to create bot with @BotFather

## Current Blockers
None at this stage.

## Next Steps
1. Create PRD.md with detailed product specifications
2. Setup project structure with proper architecture
3. Implement Gmail OAuth flow
4. Create basic Telegram bot interface
5. Develop email analysis workflow

## DEVELOPMENT PROTOCOL - MANDATORY

### CRITICAL RULE: NO CODE WITHOUT PERMISSION
**BEFORE writing ANY code (Write, Edit, MultiEdit tools):**

1. **DESCRIBE** exactly what will be implemented
2. **EXPLAIN** why this approach was chosen  
3. **CONFIRM** with user: "Can I proceed with this implementation?"
4. **WAIT** for explicit permission ("yes", "go ahead", "implement")
5. **ONLY THEN** write the code

### VIOLATIONS ARE UNACCEPTABLE
- Never write code "because it seems obvious"
- Never implement "small changes" without asking
- Never assume user wants the feature implemented
- Never rush to implementation without confirmation

### EXAMPLES OF REQUIRED CONFIRMATION:
```
BAD: "I'll create the OAuth flow now..."
GOOD: "I'll create the OAuth flow with these components:
- Flask route for /auth/gmail  
- OAuth2 client configuration
- Token storage in SQLite
- Error handling for failed auth
Can I proceed with this implementation?"
```

## COMMUNICATION STYLE GUIDELINES

### NO EMOJIS POLICY
- Never use emojis in documentation, code, or communication
- Keep all text professional and clean
- Use clear headers and formatting instead of visual symbols
- Exception: Only when explicitly requested by user

### APPLIES TO:
- All documentation files (.md)
- Code comments and docstrings
- Git commit messages
- File and variable names
- Console output and logs
- Claude responses and agent communications

## FILE CREATION CONTROL POLICY

### CRITICAL RULE: NO FILES WITHOUT DISCUSSION
**BEFORE creating ANY new file (Write tool):**

1. **PROPOSE** the file location, name, and purpose
2. **EXPLAIN** why this file is necessary
3. **DESCRIBE** the file structure and content approach
4. **CONFIRM** with user: "Should I create this file with this structure?"
5. **WAIT** for explicit permission
6. **ONLY THEN** create the file

### MANDATORY DISCUSSION POINTS:
- **Location**: Where should this file be placed and why?
- **Name**: What should it be called and why this naming?
- **Purpose**: What specific role does this file serve?
- **Structure**: How will the content be organized?
- **Alternatives**: Are there existing files that could be extended instead?

### FILE CREATION IS NEVER OBVIOUS
- Never create files "because they seem needed"
- Never assume standard project structures
- Never create multiple related files without individual approval
- Never create backup/temporary files without permission

### EXAMPLES OF REQUIRED DISCUSSION:
```
BAD: "I'll create a config.py file for settings..."
GOOD: "I need to create a configuration file. I propose:
- Location: src/config.py (to keep with application code)
- Purpose: Centralize API keys, database URLs, and app settings
- Structure: Pydantic BaseSettings class with environment variable loading
- Alternative: We could add this to main.py, but separation is cleaner
Should I create this file with this structure?"
```

## FEATURE DISCOVERY PROCESS

### Discovery Workflow
1. **IDENTIFY** - Notice opportunity during implementation
2. **DOCUMENT** - Use appropriate template below
3. **EVALUATE** - Apply decision matrix
4. **CONFIRM** - Get user approval before proceeding
5. **TRACK** - Update CLAUDE.md with decision

### Decision Matrix
- **IMPLEMENT NOW** - Blocks current feature, effort < 2 hours, zero risk
- **ADD TO BACKLOG** - High value but not MVP critical, effort > 4 hours
- **RESEARCH FURTHER** - Unclear value/approach, needs validation
- **DISCARD** - Low value, high effort, conflicts with vision

### Discovery Templates

#### FEATURE DISCOVERY
```
**Context:** [What were you working on?]
**Discovery:** [What new feature/capability identified?]
**What:** [Clear description]
**Why:** [User problem it solves]
**How:** [Technical approach]
**Effort:** [Small/Medium/Large]
**MVP Impact:** [Blocks/Accelerates/Neutral]
**Recommendation:** [Implement/Backlog/Research/Discard]
```

#### TECHNICAL IMPROVEMENT
```
**Current:** [How it works today]
**Proposed:** [How it should work]
**Benefits:** [Performance/Security/Maintainability gains]
**Effort:** [Hours estimated]
**Risk:** [High/Medium/Low and why]
**Breaking Changes:** [Yes/No and details]
```

## WORK BREAKDOWN STRUCTURE

### 1. PROJECT FOUNDATION [TODO]
- **1.1 Environment Setup** [TODO]
  - Python 3.11+ virtual environment
  - Development dependencies installation
  - IDE configuration and tooling
- **1.2 Project Structure Creation** [TODO]
  - Directory hierarchy establishment
  - Core module organization
  - Configuration file structure
- **1.3 Base Dependencies Installation** [TODO]
  - FastAPI, SQLAlchemy, Pydantic setup
  - Development tools (black, ruff, mypy, pytest)
  - Security libraries installation
- **1.4 Configuration Management** [TODO]
  - Environment variables system
  - Settings validation with Pydantic
  - Development vs production configs

### 2. CORE INFRASTRUCTURE [TODO]
- **2.1 Database Layer** [TODO]
  - **2.1.1 SQLAlchemy Models** [TODO]
    - User, Email, Calendar, Contact entities
    - Token storage models
    - Audit and logging tables
  - **2.1.2 Migration System** [TODO]
    - Alembic setup and configuration
    - Initial schema creation
    - Migration versioning strategy
  - **2.1.3 Repository Pattern** [TODO]
    - Base repository interface
    - Entity-specific repositories
    - Unit of work pattern
- **2.2 Application Framework** [TODO]
  - **2.2.1 FastAPI Application** [TODO]
    - App factory pattern
    - Router organization
    - Middleware configuration
  - **2.2.2 Dependency Injection** [TODO]
    - Service container setup
    - Dependency resolution
    - Lifecycle management
  - **2.2.3 Error Handling** [TODO]
    - Custom exception hierarchy
    - Global error handlers
    - Error response formatting
- **2.3 Security Foundation** [TODO]
  - **2.3.1 OAuth 2.0 Infrastructure** [TODO]
    - Generic OAuth client
    - Token refresh mechanism
    - Security validation
  - **2.3.2 Token Management** [TODO]
    - Encrypted token storage
    - Token rotation strategy
    - Revocation handling
  - **2.3.3 Encryption Layer** [TODO]
    - Symmetric encryption for sensitive data
    - Key management system
    - Data protection compliance

### 3. EXTERNAL INTEGRATIONS [TODO]
- **3.1 Gmail Integration** [TODO]
  - **3.1.1 OAuth Flow Implementation** [TODO]
    - Google OAuth 2.0 setup
    - Scope configuration
    - Authorization code flow
  - **3.1.2 Email Reading Service** [TODO]
    - Gmail API client
    - Email fetching and parsing
    - Incremental sync mechanism
  - **3.1.3 Email Analysis Pipeline** [TODO]
    - Content extraction and cleaning
    - Metadata processing
    - Priority scoring preparation
- **3.2 Google Calendar Integration** [TODO]
  - **3.2.1 Calendar OAuth Setup** [TODO]
    - Calendar API authentication
    - Permission scope management
    - Multi-calendar support
  - **3.2.2 Event Management Service** [TODO]
    - Event CRUD operations
    - Availability checking
    - Conflict detection
  - **3.2.3 Scheduling Logic** [TODO]
    - Meeting time suggestions
    - Participant coordination
    - Timezone handling
- **3.3 Telegram Bot Integration** [TODO]
  - **3.3.1 Bot Registration & Setup** [TODO]
    - Bot creation with BotFather
    - Webhook configuration
    - Security token management
  - **3.3.2 Message Handler Framework** [TODO]
    - Command routing system
    - Message type processing
    - Error handling for bot commands
  - **3.3.3 Conversation Management** [TODO]
    - State machine implementation
    - Context preservation
    - Multi-step interactions
- **3.4 HubSpot Integration** [TODO]
  - **3.4.1 API Client Setup** [TODO]
    - HubSpot API authentication
    - Rate limiting compliance
    - Error handling and retries
  - **3.4.2 Contact Management** [TODO]
    - Contact CRUD operations
    - Duplicate detection
    - Data enrichment
  - **3.4.3 Deal Tracking** [TODO]
    - Deal lifecycle management
    - Stage transition automation
    - Activity logging

### 4. AI/ML WORKFLOWS [TODO]
- **4.1 LLM Provider Abstraction** [TODO]
  - **4.1.1 Ollama Local Setup** [TODO]
    - Model download and configuration
    - Local inference optimization
    - Resource management
  - **4.1.2 Groq API Integration** [TODO]
    - API client implementation
    - Cost monitoring
    - Response caching
  - **4.1.3 Provider Factory Pattern** [TODO]
    - Provider interface definition
    - Dynamic provider switching
    - Fallback mechanisms
- **4.2 Email Analysis Engine** [TODO]
  - **4.2.1 Content Processing** [TODO]
    - Text extraction and cleaning
    - HTML parsing and sanitization
    - Attachment handling
  - **4.2.2 Priority Scoring** [TODO]
    - Sender importance analysis
    - Content urgency detection
    - Action requirement identification
  - **4.2.3 Action Extraction** [TODO]
    - Task identification
    - Deadline extraction
    - Response requirement analysis
- **4.3 Natural Language Processing** [TODO]
  - **4.3.1 Command Parsing** [TODO]
    - Intent recognition
    - Entity extraction
    - Parameter validation
  - **4.3.2 Intent Recognition** [TODO]
    - Classification model
    - Confidence scoring
    - Fallback handling
  - **4.3.3 Response Generation** [TODO]
    - Template-based responses
    - Dynamic content generation
    - Personalization

### 5. BUSINESS LOGIC LAYER [TODO]
- **5.1 Task Management** [TODO]
  - Task creation and tracking
  - Priority management
  - Completion workflow
- **5.2 Notification System** [TODO]
  - Event-driven notifications
  - Delivery channel management
  - Frequency control
- **5.3 Workflow Orchestration** [TODO]
  - Process automation
  - Trigger management
  - Error recovery
- **5.4 Data Synchronization** [TODO]
  - Cross-platform sync
  - Conflict resolution
  - Data consistency

### 6. USER INTERFACE [TODO]
- **6.1 Telegram Bot Interface** [TODO]
  - **6.1.1 Command Handlers** [TODO]
    - Basic commands implementation
    - Advanced feature commands
    - Administrative commands
  - **6.1.2 Conversation Flows** [TODO]
    - Multi-step interactions
    - Context-aware responses
    - User preference handling
  - **6.1.3 Inline Keyboards** [TODO]
    - Action buttons
    - Quick replies
    - Navigation menus

### 7. TESTING & QUALITY [TODO]
- **7.1 Unit Tests** [TODO]
  - Service layer testing
  - Repository testing
  - Utility function testing
- **7.2 Integration Tests** [TODO]
  - API endpoint testing
  - Database integration testing
  - External service mocking
- **7.3 API Testing** [TODO]
  - OAuth flow testing
  - Rate limiting testing
  - Error scenario testing
- **7.4 End-to-End Testing** [TODO]
  - Complete workflow testing
  - User journey validation
  - Performance testing

### 8. DEPLOYMENT & OPERATIONS [TODO]
- **8.1 Local Development Setup** [TODO]
  - Docker development environment
  - Database seeding
  - Local testing procedures
- **8.2 Production Deployment** [TODO]
  - Cloud deployment configuration
  - Environment variable management
  - Scaling considerations
- **8.3 Monitoring & Logging** [TODO]
  - Application logging
  - Performance monitoring
  - Error tracking
- **8.4 Backup & Recovery** [TODO]
  - Data backup strategy
  - Disaster recovery plan
  - Point-in-time recovery

## WBS COMPONENT SPECIFICATIONS

### 1.1 Environment Setup - Technical Specification

#### Função e Responsabilidade
Estabelecer o ambiente de desenvolvimento Python isolado e reproduzível para o projeto TaskBuddy. Este componente é a base fundamental que garante consistência entre diferentes máquinas de desenvolvimento e prepara o terreno para todas as dependências do projeto.

#### Decisões Técnicas
**Tecnologia Escolhida:** Python 3.11 + venv + requirements.txt
**Alternativas Consideradas:** 
- Poetry (gerenciamento avançado de dependências)
- Conda (ambiente científico completo)
- Docker (containerização completa)
- pyenv (múltiplas versões Python)

**Rationale:** 
- Python 3.11: Melhor performance, novos type hints, async improvements
- venv: Simples, nativo, zero complexidade adicional
- requirements.txt: Padrão da indústria, fácil deploy, compatível com todas as plataformas

**Trade-offs:**
- GANHA: Simplicidade, compatibilidade universal, setup rápido
- PERDE: Não resolve dependências automaticamente, não tem lock file nativo

#### Arquitetura e Padrões
**Estrutura de Arquivos:**
```
TaskBuddy/
├── .env.example           # Template de variáveis de ambiente
├── .gitignore            # Exclusões do git
├── requirements.txt      # Dependências de produção
├── requirements-dev.txt  # Dependências de desenvolvimento
├── setup.py             # Configuração do pacote (futuro)
└── venv/                # Virtual environment (gitignored)
```

**Dependências:** Sistema operacional com Python 3.11+ disponível
**Interfaces:** Todas as outras partes do projeto dependem deste setup

#### Implementação Strategy
**Abordagem:**
1. Verificar versão Python disponível
2. Criar virtual environment isolado
3. Ativar environment e verificar isolamento
4. Instalar dependências básicas (FastAPI, SQLAlchemy, Pydantic)
5. Instalar ferramentas de desenvolvimento (black, ruff, mypy, pytest)
6. Configurar templates de ambiente

**Comandos Específicos:**
```bash
python --version  # Verificar >= 3.11
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
pip install --upgrade pip
pip install -r requirements.txt
pip install -r requirements-dev.txt
```

**Pontos de Extensão:**
- Futura migração para Poetry se complexidade crescer
- Adição de Docker para deployment
- Pre-commit hooks para qualidade de código

**Oportunidades de Sinergia:**
- Base para todos os outros componentes
- Environment preparado para todas as integrações
- Ferramentas de qualidade usadas em todo o projeto

**Riscos Técnicos:**
- Conflitos de versão entre dependências
- Diferenças entre sistemas operacionais
- Dependências que requerem compilação nativa

#### Critérios de Completude
- [ ] Python 3.11+ verificado e disponível
- [ ] Virtual environment criado em ./venv/
- [ ] Environment ativado com sucesso
- [ ] pip atualizado para versão mais recente
- [ ] requirements.txt criado com dependências básicas:
  - [ ] fastapi>=0.104.0
  - [ ] sqlalchemy>=2.0.0
  - [ ] pydantic>=2.5.0
  - [ ] python-telegram-bot>=20.7
- [ ] requirements-dev.txt criado com ferramentas:
  - [ ] black>=23.0.0
  - [ ] ruff>=0.1.0
  - [ ] mypy>=1.7.0
  - [ ] pytest>=7.4.0
- [ ] .env.example criado com variáveis necessárias
- [ ] .gitignore configurado (venv/, .env, __pycache__, etc.)
- [ ] Teste de validação: `python -c "import fastapi, sqlalchemy, pydantic; print('Environment OK')"`

### Next Components Ready for Specification

#### 1.2 Project Structure Creation - Ready for Specification
**Key Decisions Needed:**
- Directory hierarchy pattern (src/ vs flat structure)
- Module organization (by feature vs by layer)
- Configuration file locations
- Import path strategies

#### 1.3 Base Dependencies Installation - Ready for Specification  
**Key Decisions Needed:**
- Exact version pinning strategy
- Development vs production dependency separation
- Optional dependency groups
- Security scanning tools

#### 1.4 Configuration Management - Ready for Specification
**Key Decisions Needed:**
- Pydantic Settings vs python-decouple
- Environment variable naming conventions
- Secret management approach
- Configuration validation strategies

#### 2.1.1 SQLAlchemy Models - Critical for Database Design
**Key Decisions Needed:**
- Table naming conventions
- Relationship mapping strategies
- Audit trail implementation
- Migration strategy with Alembic

#### 2.3.1 OAuth 2.0 Infrastructure - Foundation for All Integrations
**Key Decisions Needed:**
- OAuth library choice (authlib vs requests-oauthlib)
- Token storage encryption method
- Refresh token rotation strategy
- Multi-provider abstraction pattern

#### 3.1.1 Gmail OAuth Flow Implementation - First External Integration
**Key Decisions Needed:**
- Google API client library choice
- Scope management strategy
- Error handling patterns
- Rate limiting approach

**Specification Template Established:**
Each component will include:
- Function & Responsibility
- Technical Decisions (technology choices, alternatives, rationale, trade-offs)
- Architecture & Patterns (file structure, dependencies, interfaces)
- Implementation Strategy (approach, extension points, synergies, risks)
- Completion Criteria (detailed checklists)

## DECISION HISTORY

### Architecture & Technology Decisions
**2025-08-16 15:45 - APPROVED:** Python over Node.js for backend
- **Rationale:** Superior AI/ML ecosystem, better data processing, more natural for email analysis
- **Status:** Final decision, no need to reconsider

**2025-08-16 15:50 - APPROVED:** Telegram Bot API over WhatsApp Business API
- **Rationale:** WhatsApp costs R$150+/month, requires business approval, Telegram is free with better dev experience
- **Status:** Final decision, no need to reconsider

**2025-08-16 16:00 - APPROVED:** Local-first development strategy
- **Rationale:** Zero initial costs, faster development, easy debugging, clear migration path to cloud
- **Status:** Final decision for MVP phase

**2025-08-16 16:05 - APPROVED:** FastAPI + SQLAlchemy + Pydantic stack
- **Rationale:** Enterprise-grade, type-safe, good performance, easy cloud migration
- **Status:** Final decision, no need to reconsider

**2025-08-16 16:10 - APPROVED:** Ollama (local) → Groq API (production) migration path
- **Rationale:** Free development, low-cost production (~R$20/month vs R$200+ for GPT-4)
- **Status:** Final decision, provider abstraction required

### Development Process Decisions
**2025-08-16 16:15 - APPROVED:** Mandatory permission before writing code
- **Rationale:** User wants full control over implementation, no assumptions
- **Status:** Critical rule, never violate

**2025-08-16 16:20 - APPROVED:** No emojis in documentation or code
- **Rationale:** User prefers professional, clean communication style
- **Status:** Style guide, applies to all files

**2025-08-16 16:25 - APPROVED:** File creation requires discussion and approval
- **Rationale:** Prevent uncontrolled file proliferation, maintain clean project structure
- **Status:** Critical rule, never violate

**2025-08-16 16:30 - APPROVED:** Consolidate FEATURE_DISCOVERY_GUIDELINES.md into CLAUDE.md
- **Rationale:** Avoid redundancy, single source of truth for development processes
- **Status:** Completed, file deleted

### Project Scope Decisions
**2025-08-16 16:35 - APPROVED:** Create 6 specialized agents for development
- **Rationale:** Better expertise distribution, focused problem-solving
- **Status:** Implemented, agents created and configured

**2025-08-16 16:40 - APPROVED:** CLAUDE.md + PRD.md documentation structure
- **Rationale:** Separate technical memory from product specifications
- **Status:** Implemented and maintained

**2025-08-16 16:45 - APPROVED:** WBS-first project structuring approach
- **Rationale:** Systematic breakdown prevents scope creep, enables accurate estimation
- **Status:** In progress - WBS creation phase

**2025-08-16 17:00 - APPROVED:** Learning-focused development over market validation
- **Rationale:** User prioritizes deep learning and perfect implementation over rapid market feedback
- **Status:** Development philosophy - quality over speed

**2025-08-16 17:05 - APPROVED:** "Perfect Incremental" development strategy
- **Rationale:** WBS detalhado + implementação incremental com quality gates rigorosos
- **Status:** Development methodology confirmed

**2025-08-16 17:15 - APPROVED:** Complete technical specifications for all 31 WBS components
- **Rationale:** Each component needs detailed technical analysis before implementation to ensure optimal decisions and prevent rework
- **Status:** Planned - will be created incrementally as needed

## CURRENT SESSION STATE
**Session Date:** 2025-08-16
**Session Start:** ~15:30
**Session End:** ~17:15
**Session Focus:** Complete project foundation setup and WBS documentation
**Mental State:** WBS documented, first component specified, ready for implementation
**Next Immediate Task:** Implement 1.1 Environment Setup (first WBS component)
**User Communication Style:** Direct, critical analysis preferred, no hand-holding
**Pending Decisions:** None - methodology and structure fully defined
**Current Phase:** Planning completed, ready to begin development execution

**Session Summary:**
- WBS complete with 31 components across 8 major areas
- First technical specification completed (1.1 Environment Setup)
- Development methodology aligned (Perfect Incremental strategy)
- All protocols established (code permission, file creation, no emojis)
- Decision history capturing all choices with rationale
- Next 6 components identified with key decisions outlined

**NEXT SESSION START POINT:**
BEGIN HERE -> Implement component 1.1 Environment Setup following the detailed specification above. Use the 15 completion criteria as checklist. After completing 1.1, proceed to create detailed specification for 1.2 Project Structure Creation using the established template.

**CRITICAL REMINDERS FOR NEXT SESSION:**
1. ALWAYS ask permission before writing ANY code or creating ANY file
2. Reference DECISION HISTORY to avoid re-discussing settled topics
3. Update WBS status markers as components are completed
4. Each specification must include technical alternatives analysis
5. Focus on learning and perfect implementation over speed

## Session Notes
**2025-08-16:** Initial project planning, agent creation, architecture decisions, development protocols established

## Important URLs & Resources
- Gmail API Docs: https://developers.google.com/gmail/api
- Telegram Bot API: https://core.telegram.org/bots/api
- HubSpot API: https://developers.hubspot.com/docs/api/overview
- LangChain Docs: https://python.langchain.com/
- FastAPI Docs: https://fastapi.tiangolo.com/