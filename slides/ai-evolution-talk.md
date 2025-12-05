# The Future-Ready Flutter Engineer: Mastering AI in Your Workflow
## DevFest Akure 2025 - Workshop Slides Content

---

# SECTION 1: ICE BREAKERS (Choose One)

---

## Ice Breaker Option A: The Funny/Relatable One

### "Raise Your Hand If..."

- Raise your hand if you've ever copy-pasted code from ChatGPT directly into production 🙈
- Keep it up if it actually worked on the first try
- Now raise your hand if you've argued with an AI about why your code is correct
- Keep it up if the AI was right

*"Today, we're going to learn how to argue with AI more effectively"*

---

## Ice Breaker Option B: The Thought-Provoking One

### "The Developer's Dilemma"

**Question for the room:**

> "In 2019, writing code was the job. In 2025, understanding what code to write is the job. In 2027... what will the job be?"

*Let 2-3 people share thoughts*

**The answer:** The job is becoming *orchestrating intelligence* - knowing which AI to use, when to use it, and how to validate its output.

---

## Ice Breaker Option C: The Interactive Demo

### "Let's Play: AI or Human?"

Show 3 code snippets on screen. Audience guesses which was written by:
1. Junior developer
2. Senior developer  
3. AI (Claude/GPT)

**Plot twist:** They're all from AI, but prompted differently.

*"The quality of AI output depends entirely on how you prompt it. That's what we're learning today."*

---

## Ice Breaker Option D: The Shocking Stats

### "6 Months That Changed Everything"

**June 2024:**
- Claude 3.5 Sonnet could solve ~33% of real-world coding tasks (SWE-bench)
- GPT-4o was "pretty good" at code completion

**December 2025:**
- Claude Opus 4.5 solves 77%+ of the same tasks
- AI can now build entire features, not just autocomplete

*"We're not here to learn a tool. We're here to learn a new way of engineering."*

---

# SECTION 2: THE THREE GENERATIONS OF AI CODING MODELS

---

## The Evolution Framework

### How to Think About AI Model Generations

Think of AI models like smartphone generations:
- **Gen 1:** Feature phones → Did one thing well
- **Gen 2:** Early smartphones → Multiple capabilities, still learning
- **Gen 3:** Modern smartphones → Integrated, intelligent, context-aware

**The same evolution happened in AI coding models... in just 18 months.**

---

## Generation 1: The Autocomplete Era
### (June 2024 - August 2024)

**The Models:**
| Provider | Model | Release | Key Capability |
|----------|-------|---------|----------------|
| Anthropic | Claude 3.5 Sonnet | June 2024 | First "vibe coding" capable model |
| OpenAI | GPT-4o | May 2024 | Fast, multimodal, affordable |
| Google | Gemini 1.5 Pro | February 2024 | 1M token context window |

**What They Could Do:**
- ✅ Autocomplete code
- ✅ Explain code
- ✅ Write functions from descriptions
- ✅ Basic debugging

**What They Couldn't Do:**
- ❌ Multi-file refactoring
- ❌ Understand entire codebases
- ❌ Run and test their own code
- ❌ Use external tools reliably

**Benchmark:** ~33% on SWE-bench Verified (real GitHub issues)

---

## Generation 2: The Reasoning Era
### (September 2024 - October 2025)

**The Models:**
| Provider | Model | Release | Key Capability |
|----------|-------|---------|----------------|
| OpenAI | o1 | September 2024 | Chain-of-thought reasoning |
| OpenAI | o3 | December 2024 | Advanced reasoning |
| Anthropic | Claude Sonnet 4 | May 2025 | Balanced speed + intelligence |
| OpenAI | GPT-4.1 | April 2025 | Better coding, longer context |
| Google | Gemini 2.5 Pro | March 2025 | Thinking mode, tool use |

**The Big Shift: Reasoning Models**
- Models started "thinking" before answering
- Could break down complex problems
- Started understanding *intent*, not just *syntax*

**What Changed:**
- ✅ Multi-step problem solving
- ✅ Better at understanding project context
- ✅ Could use tools (web search, code execution)
- ✅ More accurate, fewer hallucinations

**Benchmark:** ~49-65% on SWE-bench Verified

---

## Generation 3: The Agentic Era
### (November 2025 - Present)

**The Models:**
| Provider | Model | Release | Price (Input/Output per 1M) | SWE-bench |
|----------|-------|---------|----------------------------|-----------|
| Anthropic | Claude Opus 4.5 | Nov 24, 2025 | $5 / $25 | State-of-the-art |
| Anthropic | Claude Sonnet 4.5 | Sep 29, 2025 | $3 / $15 | 77.2% |
| Anthropic | Claude Haiku 4.5 | Oct 15, 2025 | $1 / $5 | ~65% (Sonnet 4 level) |
| OpenAI | GPT-5 | Aug 7, 2025 | Varies by tier | PhD-level |
| OpenAI | GPT-5.1 | Nov 12, 2025 | Varies | Smarter, more conversational |
| Google | Gemini 3 | Nov 2025 | TBA | 76.2% (single attempt) |

**The Paradigm Shift:**
> "What was recently at the frontier is now cheaper and faster. Five months ago, Claude Sonnet 4 was state-of-the-art. Today, Claude Haiku 4.5 gives similar coding performance at 1/3 cost and 2x speed." 
> — Anthropic, October 2025

**What's New:**
- ✅ **Agentic capabilities** - AI can plan, execute, and iterate
- ✅ **Computer use** - AI can interact with your actual computer
- ✅ **Tool ecosystems** - MCP, function calling, code execution
- ✅ **Near-human coding** - 77%+ on real-world GitHub issues
- ✅ **Multi-modal** - Understands images, code, and context together

---

## The Visual Evolution

```
Gen 1 (Mid 2024)          Gen 2 (Late 2024-Mid 2025)     Gen 3 (Late 2025)
┌─────────────┐           ┌─────────────────────┐        ┌──────────────────────┐
│             │           │                     │        │                      │
│  You write  │           │   You write         │        │   You describe       │
│  most code  │   ───►    │   AI assists        │  ───►  │   AI implements      │
│  AI helps   │           │   You review        │        │   You validate       │
│             │           │                     │        │                      │
└─────────────┘           └─────────────────────┘        └──────────────────────┘
   33% auto               49-65% collaborative            77%+ agentic
```

---

# SECTION 3: THE THREE TIERS OF AI CODING MODELS

---

## Understanding Model Tiers

### Not All Models Are Created Equal

Just like cars have economy, mid-range, and luxury tiers, AI models do too:

| Tier | Use Case | Cost | Speed | Intelligence |
|------|----------|------|-------|--------------|
| 🚀 **Flash/Haiku** | High-volume, simple tasks | $ | ⚡⚡⚡ | ⭐⭐ |
| 🎯 **Standard/Sonnet** | Daily driver, balanced | $$ | ⚡⚡ | ⭐⭐⭐ |
| 👑 **Pro/Opus** | Complex, enterprise | $$$ | ⚡ | ⭐⭐⭐⭐ |

---

## Tier 1: The Speed Demons 🚀
### (Flash / Haiku / Mini)

**Current Models:**
- **Claude Haiku 4.5** - $1/$5 per million tokens
- **Gemini 2.5 Flash** - Best for everyday tasks
- **GPT-4o-mini** - Fast, cheap, cheerful

**When to Use:**
- Code autocompletion
- Quick explanations
- Syntax help
- High-volume API calls
- CI/CD automation

**Real Talk:** Claude Haiku 4.5 now matches Claude Sonnet 4 (the previous frontier model) at 1/3 the cost. The cheap tier keeps getting smarter.

---

## Tier 2: The Daily Drivers 🎯
### (Sonnet / Standard / Pro)

**Current Models:**
- **Claude Sonnet 4.5** - $3/$15 per million tokens, 77.2% SWE-bench
- **Gemini 2.5 Pro** - Great thinking mode
- **GPT-4o** - Still solid for many tasks

**When to Use:**
- Feature development
- Code review
- Debugging complex issues
- Architecture discussions
- Most day-to-day coding

**This is your workhorse.** Most developers should live here.

---

## Tier 3: The Heavy Hitters 👑
### (Opus / GPT-5 Pro / Gemini 3 Deep Think)

**Current Models:**
- **Claude Opus 4.5** - $5/$25 per million tokens, best coding model
- **GPT-5 Pro** - Unlimited thinking, highest capability
- **Gemini 3 Deep Think** - State-of-the-art on reasoning benchmarks

**When to Use:**
- Complex architectural decisions
- Multi-file refactoring
- Difficult debugging
- System design
- When the other tiers fail

**The "call the expert" tier.** More expensive, but sometimes you need the best.

---

## Tier Selection Flowchart

```
┌─────────────────────────────────────────────────────┐
│              What are you trying to do?             │
└─────────────────────────────────────────────────────┘
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
   ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
   │ Quick help  │ │ Build a     │ │ Complex     │
   │ Autocomplete│ │ feature     │ │ architecture│
   │ Simple Q&A  │ │ Debug issue │ │ Hard bugs   │
   └─────────────┘ └─────────────┘ └─────────────┘
          │               │               │
          ▼               ▼               ▼
   ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
   │  🚀 Flash   │ │ 🎯 Sonnet   │ │  👑 Opus    │
   │   Haiku     │ │   Standard  │ │   Pro       │
   │   Mini      │ │   Pro       │ │ Deep Think  │
   └─────────────┘ └─────────────┘ └─────────────┘
```

---

# SECTION 4: THE PELICAN ON A BICYCLE TEST

---

## A Simple Benchmark That Tells a Big Story

### The "Pelican on a Bicycle" SVG Test

Created by **Robert Glaser** (AI researcher/developer), this simple prompt has become a viral benchmark:

> "Draw an SVG of a pelican riding a bicycle"

**Why it matters:**
- Tests spatial reasoning
- Tests understanding of complex concepts
- Tests ability to render working code
- Easy for humans to evaluate (you can see it!)

---

## How Models Have Progressed

### Gen 1 Models (Mid 2024)
- Often drew pelican and bicycle separately
- Pelican might be a blob
- Bicycle wheels might be squares
- "Close enough" attempts

### Gen 2 Models (Late 2024)
- Better pelican shapes
- Bicycle was recognizable
- Still struggled with positioning
- Pelican sometimes facing wrong way

### Gen 3 Models (Late 2025)
- Anatomically reasonable pelican
- Proper bicycle proportions
- Correct positioning (pelican ON the bicycle)
- Some even add details like pedals, handlebars

*[Include actual SVG comparisons if time permits]*

---

## What This Tells Us

### The Benchmark Reflects Real Coding Ability

If a model can:
- Understand the spatial relationship (pelican ON bicycle)
- Generate valid SVG code
- Handle the complexity of two objects interacting

Then it can likely:
- Understand widget hierarchies in Flutter
- Position UI elements correctly
- Handle complex state relationships
- Generate working, not just syntactically correct, code

**The pelican test is a proxy for "does this model actually understand, or just pattern match?"**

---

# SECTION 5: MCP - THE MODEL CONTEXT PROTOCOL

---

## What is MCP?

### The "USB-C for AI" Analogy

Before USB-C:
- Every device had different chargers
- Couldn't share accessories
- Cables everywhere

After USB-C:
- One cable for everything
- Universal compatibility
- Simpler life

**MCP does this for AI tools and data sources.**

---

## MCP Explained Simply

### The Problem It Solves

**Before MCP:**
```
Your AI ──────► Only knows what you paste into it
               Can't access your database
               Can't read your files
               Can't use your tools
```

**After MCP:**
```
Your AI ──────► MCP Protocol ──────► Your Database (Supabase)
                    │
                    ├──────► Your Files
                    │
                    ├──────► Your APIs
                    │
                    └──────► Any Tool You Want
```

---

## How MCP Works

### Three Core Components

1. **MCP Hosts** (the AI applications)
   - Claude Desktop
   - VS Code with Copilot
   - Cursor
   - Custom applications

2. **MCP Servers** (the tools/data providers)
   - Supabase MCP Server
   - GitHub MCP Server
   - File System MCP Server
   - Custom servers for your APIs

3. **MCP Protocol** (the communication standard)
   - JSON-RPC based
   - Standardized message format
   - Works locally or remotely

---

## MCP in Practice

### What We're Using Today

**Supabase MCP Server** allows Claude to:

```
┌─────────────────────────────────────────────┐
│  "Create a users table with id, name,       │
│   email, and created_at columns"            │
└─────────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────┐
│  Claude reads the prompt                    │
│  Calls Supabase MCP Server                  │
│  Executes: CREATE TABLE users (...)         │
│  Returns: "Table created successfully"      │
└─────────────────────────────────────────────┘
```

**No SQL knowledge required. No copy-pasting. No context switching.**

---

## Why MCP Matters for Developers

### The Shift from "Tools" to "Agents"

| Before MCP | After MCP |
|------------|-----------|
| AI suggests code, you copy-paste | AI executes actions directly |
| You switch between apps | AI works across your tools |
| Context gets lost | Context flows automatically |
| You are the integration layer | MCP is the integration layer |

**You become the architect, not the bricklayer.**

---

## MCP Security Model

### "But Can AI Just Do Anything?"

**No. You're in control.**

- **Explicit permissions** - You approve what servers can do
- **Scoped access** - Servers only see what they need
- **Local first** - Most MCP servers run on your machine
- **Audit trail** - You can see what actions were taken

Think of it like app permissions on your phone:
- Camera app can access camera
- Browser can access network
- Calculator can't access your photos

---

# SECTION 6: THE FUTURE-READY MINDSET

---

## What Changes for Developers

### The Skills That Matter Now

**Less Important:**
- Memorizing syntax
- Writing boilerplate
- Manual refactoring
- Knowing every API by heart

**More Important:**
- Clear problem articulation
- Architecture and system design
- Code review and validation
- Understanding trade-offs
- Knowing when AI is wrong

---

## The New Developer Workflow

### Traditional vs AI-Native

**Traditional (2020):**
1. Google the problem
2. Read Stack Overflow
3. Copy code
4. Debug for hours
5. Repeat

**AI-Native (2025):**
1. Describe what you want
2. AI generates first draft
3. Review and iterate with AI
4. Validate with tests
5. Ship

**Time saved: 50-80% on routine tasks**

---

## The Hierarchy of AI-Assisted Development

### Level 1: Autocomplete
- Let AI finish your lines
- Accept or reject suggestions
- Minimal workflow change

### Level 2: Chat-Assisted
- Ask AI questions in sidebar
- Copy-paste suggestions
- Review before using

### Level 3: Inline Generation
- Describe features in comments
- AI generates implementations
- You edit and refine

### Level 4: Agentic Development ← **We're here now**
- AI plans the approach
- AI implements across files
- AI tests its own code
- You validate and ship

---

## Key Takeaways

### What to Remember

1. **The best model 6 months ago is now the cheap tier** - Costs keep falling, capabilities keep rising

2. **Three tiers for three use cases** - Flash for speed, Sonnet for daily work, Opus for hard problems

3. **MCP is the future of AI integration** - Learn it now, thank yourself later

4. **Your job is changing** - From writing code to validating and orchestrating

5. **The tools are ready** - The question is: are you?

---

## Workshop Agenda Reminder

| Time | Activity |
|------|----------|
| 9:00 - 9:30 | Introduction & This Talk |
| 9:30 - 10:30 | Setting Up Your AI Environment |
| 10:30 - 10:45 | Break |
| 10:45 - 12:30 | Building the Posts App with AI |
| 12:30 - 1:30 | Lunch Break |
| 1:30 - 2:45 | Advanced Features & Q&A |
| 2:45 - 3:00 | Wrap-up & Resources |

---

## Resources

### Where to Learn More

**Model Information:**
- [Anthropic Model Cards](https://docs.anthropic.com/en/docs/about-claude/models)
- [OpenAI Models](https://platform.openai.com/docs/models)
- [Google AI Models](https://deepmind.google/models/gemini/)

**MCP:**
- [MCP Documentation](https://modelcontextprotocol.io/)
- [Supabase MCP Server](https://github.com/supabase/mcp-server-supabase)

**Tools:**
- [Cursor Editor](https://cursor.sh)
- [GitHub Copilot](https://github.com/features/copilot)
- [Claude Desktop](https://claude.ai/download)

---

## Connect With Me

### Fola Oluwafemi

- 🐦 Twitter/X: [@folabuilds](https://twitter.com/folabuilds)
- 💼 LinkedIn: [/in/fola-oluwafemi](https://linkedin.com/in/fola-oluwafemi)
- 🐙 GitHub: [folaoluwafemi](https://github.com/folaoluwafemi)

**Workshop Repository:**
[github.com/folaoluwafemi/devfest-akure-workshop](https://github.com/folaoluwafemi/devfest-akure-workshop)

---

# Let's Build Something Amazing! 🚀

*Time to set up your environment and start coding with AI*

---

# APPENDIX: Quick Reference Cards

---

## Model Quick Reference (December 2025)

### Anthropic Claude
| Model | Price (In/Out per 1M) | Best For |
|-------|----------------------|----------|
| Opus 4.5 | $5 / $25 | Complex architecture, hard bugs |
| Sonnet 4.5 | $3 / $15 | Daily coding, features |
| Haiku 4.5 | $1 / $5 | Quick tasks, high volume |

### OpenAI GPT
| Model | Tier | Best For |
|-------|------|----------|
| GPT-5.1 | Pro | Advanced reasoning |
| GPT-5 | Standard | General coding |
| GPT-4o | Fast | Quick responses |

### Google Gemini
| Model | Best For |
|-------|----------|
| Gemini 3 | Most intelligent, best reasoning |
| Gemini 2.5 Pro | Thinking mode, tool use |
| Gemini 2.5 Flash | Fast, everyday tasks |

---

## Timeline: Key Releases 2024-2025

```
2024
├── Feb: Gemini 1.5 Pro (1M context)
├── May: GPT-4o (fast, multimodal)
├── Jun: Claude 3.5 Sonnet (vibe coding begins)
├── Sep: OpenAI o1 (reasoning models)
├── Dec: OpenAI o3 (advanced reasoning)

2025
├── Feb: GPT-4.5 (Orion becomes 4.5)
├── Mar: Gemini 2.5 Pro (thinking mode)
├── Apr: GPT-4.1 (better coding)
├── May: Claude Sonnet 4 (balanced)
├── Aug 7: GPT-5 (PhD-level claims)
├── Sep 29: Claude Sonnet 4.5 (77.2% SWE-bench)
├── Oct 15: Claude Haiku 4.5 (cheap + smart)
├── Nov: Gemini 3 (most intelligent Google model)
├── Nov 12: GPT-5.1 (refinement)
├── Nov 24: Claude Opus 4.5 (current king)
└── Dec: You're here! 🎉
```

---

## MCP Server Examples

### What MCP Servers Can Do

| Server | Capabilities |
|--------|-------------|
| **Supabase** | Create tables, run queries, manage auth |
| **GitHub** | Read repos, create PRs, manage issues |
| **Filesystem** | Read/write files, search directories |
| **Postgres** | Direct database operations |
| **Slack** | Send messages, read channels |
| **Custom** | Anything you can build! |

---

## Prompt Engineering Quick Tips

### For Better AI Coding Results

1. **Be specific about context**
   - "In this Flutter app using Provider..."
   - Not: "Make a button"

2. **Specify the output format**
   - "Return only the code, no explanation"
   - "Explain your reasoning first"

3. **Break complex tasks down**
   - "First, create the model class"
   - "Next, create the repository"

4. **Provide examples when possible**
   - "Similar to how `UserRepository` works..."

5. **Ask for alternatives**
   - "Give me 3 different approaches to..."

---

*End of Slides Content*
