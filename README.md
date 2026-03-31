# 🔧 CoM Agent — Design Intelligence Service

## 🏆 Built for PL_Genesis Hackathon

This project is officially submitted to the **PL_Genesis: Frontiers of Collaboration** hackathon (Existing Code Track). 

### 🔧 Sponsor Track Integrations:
1. **Ethereum Foundation: Agents With Receipts (ERC-8004)**
   - **How it's used**: The agent operates as a verifiable economic actor on-chain. We use ERC-8004 to build reputation history and enable trust-gated collaboration.
   - **Verification**: BaseScan TX Hash `0x57270631868a7e620ff15e8c016190d325a6fafb184c66b8814c45b2bd082115`
2. **Protocol Labs: AI & Robotics**
   - **How it's used**: Fully autonomous execution loop for extracting mechanical constraints (Chain of Mechanics) from arbitrary natural language prompts.

> **Hardware design analysis as a decentralized service for AI agents.**

CoM Agent takes a natural language description of any hardware device and outputs a structured mechanical analysis — transmission paths, component relationships, and an intrinsic complexity score. Other agents consume this intelligence to create, evaluate, and improve hardware designs on-chain.

**→ Input: "A robotic arm that picks up cups"**  
**→ Output: 12-step mechanical path, complexity score 576, verification hash for on-chain commitment**

---

## 🌾 CROPS Compliance

| Constraint | How We Meet It |
|------------|---------------|
| **Censorship Resistance** | Listed on decentralized agent markets (Olas, OpenServ). No single platform controls access. |
| **Open Source** | API specification is fully open. Anyone can build a compatible analysis engine. The interface standard is the public good; implementations compete on quality. |
| **Privacy** | Design prompts are processed locally or in TEE (Lit Protocol). User ideas never leave their environment. Only the output hash goes on-chain. |
| **Security** | Output includes `metricsHash` — a cryptographic commitment that lets consumers verify score correctness without trusting the agent. Deterministic: same input → same output → same hash. |

---

## 🎯 Design Thinking

### The Problem (Empathize)
Hardware design requires **three expert-level skills simultaneously** (3D + Electronics + Code = n³).
- Evaluating mechanical feasibility requires deep domain expertise
- Such analysis is expensive, slow, and not available as a composable service
- Agents building hardware need complexity scores but can't compute them independently

### The Insight (Define)
> "The hottest new programming language is English." — Karpathy  
> "The hardware language is Accessible Prototyping." — MakerKit

What if hardware intelligence was a **callable service**? Any agent could send a design description and receive a professional-grade mechanical analysis — component paths, complexity scores, simulation readiness — in seconds.

### The Solution (Ideate)

**Mechanical Design Intelligence as a Service:**

The agent uses proprietary analysis algorithms to decompose any hardware concept into:
- **Mechanical paths**: How motion/force transfers through components (motor → gear → axle → output)
- **Complexity metrics**: Quantified difficulty across three dimensions (structure × electronics × logic = n³)
- **Feasibility assessment**: Can this be built? What are the constraints?

```
Input:  Natural language prompt + optional design file
        ↓
Design Intelligence Engine (proprietary)
        ↓  
Output: {
  mechanicalPath: [...],        // Ordered component relationships
  complexityScores: {           // The n³ metrics
    structureScore,             // 3D: parts, joints, DOF, path depth
    electronicScore,            // I/O: actuators, sensors, modules
    logicScore,                 // Code: states, behaviors, feedback
    complexityScore,            // structure × electronic × logic
    metricsHash                 // Verification hash
  },
  simulationReady: true/false,  // Can this design be validated?
  suggestions: [...]            // Improvement recommendations
}
```

### The UX (Prototype)

| Stage | Experience | Emotion |
|-------|-----------|---------|
| **Lead-In** | Developer/Agent has an idea: "A gripper with force feedback". Doesn't know if it's mechanically feasible. | Uncertainty |
| **Hero Moment** ✨ | Calls CoM Agent → In 3 seconds: "12-step path, 4 motors, 2 sensors, complexity=576. Feasible! Suggested: add worm gear for grip lock." | *"It understood my idea AND improved it!"* |
| **What's Next** | Takes the output → feeds into Production Market → createDesign() with complexity score → others fork → royalties flow | From idea to on-chain asset in minutes |

---

## 🔗 How It Works

### API Interface (Open Standard)

```python
# Any agent can call CoM Agent via OpenServ or direct HTTP + x402 payment

# Request
POST /analyze
{
  "prompt": "A robotic arm that can pick up cups gently",
  "constraints": {
    "maxMotors": 4,
    "maxWeight_g": 500,
    "powerSource": "5V USB"
  }
}

# Response
{
  "mechanicalPath": [
    {"step": 1, "part": "DC Motor", "type": "actuator", "role": "shoulder"},
    {"step": 2, "part": "Worm Gear", "type": "gear", "ratio": "40:1"},
    {"step": 3, "part": "Shoulder Axle", "type": "structure"},
    ...
  ],
  "complexity": {
    "structureScore": 12,
    "electronicScore": 6,
    "logicScore": 8,
    "complexityScore": 576,
    "metricsHash": "0x1f2e3d..."
  },
  "feasibility": {
    "mechanicallySound": true,
    "withinConstraints": true,
    "simulationReady": true
  },
  "suggestions": [
    "Add worm gear at gripper for self-locking grip",
    "Consider force sensor on end effector for gentle handling"
  ]
}
```

### Complexity Scoring — The n³ Formula

```
┌──────────────────────────────────────────────┐
│  Dimension 1: Structure (Mechanical Path)    │
│  Parts × Joints × DOF × Path Depth          │
│  Example: 30 parts, 4 joints, 4-DOF = 12    │
├──────────────────────────────────────────────┤
│  Dimension 2: Integration (I/O Combinations) │
│  Actuators × Sensors × Modules              │
│  Example: 4 motors + 2 sensors = 6          │
├──────────────────────────────────────────────┤
│  Dimension 3: Logic (Control Complexity)     │
│  States × Behaviors × Feedback Loops        │
│  Example: 8 states, PID control = 8         │
├──────────────────────────────────────────────┤
│  Complexity = 12 × 6 × 8 = 576              │
│  metricsHash = hash(12, 6, 8, algo_v1)      │
└──────────────────────────────────────────────┘
```

### How Other Agents Use This

```
1. Agent on Production Market wants to CREATE a design
   → Calls CoM Agent: "analyze this gripper concept"
   → Gets complexityScore + metricsHash
   → Calls ProductionMarket.createDesign(score, hash)
   → Design registered on-chain with verified complexity

2. Agent wants to EVALUATE a design before forking
   → Calls CoM Agent: "analyze this existing design"
   → Compares complexity scores
   → Decides if fork is worth the cost

3. Agent marketplace RANKS designs
   → Uses complexity scores from CoM Agent
   → Higher complexity = more valuable = premium pricing
```

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────┐
│  Consumer Agents                            │
│  (Production Market, evaluators, builders)  │
└──────────────────┬──────────────────────────┘
                   ↓ x402 payment per query
┌─────────────────────────────────────────────┐
│  CoM Agent                                  │
│  ┌───────────────────────────────────────┐  │
│  │  API Layer (Open Source)              │  │
│  │  - Request parsing + validation       │  │
│  │  - x402 payment verification          │  │
│  │  - Response formatting                │  │
│  └───────────────┬───────────────────────┘  │
│                  ↓                          │
│  ┌───────────────────────────────────────┐  │
│  │  Analysis Engine (Proprietary)       │  │
│  │  - Mechanical path inference          │  │
│  │  - Complexity scoring                 │  │
│  │  - Feasibility analysis               │  │
│  │  Runs in: Local / TEE (Lit Protocol) │  │
│  └───────────────────────────────────────┘  │
└──────────────────┬──────────────────────────┘
                   ↓
┌─────────────────────────────────────────────┐
│  On-Chain (Base)                            │
│  - ERC-8004 identity + reputation           │
│  - metricsHash commitments                  │
│  - Query count / payment history            │
└─────────────────────────────────────────────┘
```

---

## 🏆 Hackathon Tracks

- **OpenServ** — Multi-agent service + x402 payments
- **Olas: Monetize** — List on Olas agent marketplace
- **Lit Protocol: Dark Knowledge** — Proprietary engine in TEE
- **ERC-8183** — Programmable agent skill standard
- **Olas: Build on Pearl** — Desktop agent integration
- **ERC-8004** — Agent identity and reputation

---

## 📜 License

MIT — API specification and interface code are open source.  
Design intelligence engine is proprietary.

---

*Built at The Synthesis Hackathon 2026 by Wu Xi*  
*Agent: CoM Agent | Harness: Antigravity (Gemini) | Model: gemini-2.5-pro*
