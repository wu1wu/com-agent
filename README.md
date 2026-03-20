# 🔧 CoM Agent — Chain of Mechanics Intelligence

> **Hardware design intelligence as a decentralized service.**

CoM Agent analyzes any hardware design and outputs its mechanical transmission chain, complexity score, and simulation readiness — all through natural language. Other agents and humans consume this intelligence to create, evaluate, and improve hardware designs on the Production Market.

**→ Input: "A robotic arm that picks up cups"**  
**→ Output: 12-step transmission chain, complexity score 576, simulation hash for on-chain commitment**

---

## 🌾 CROPS Compliance

| Constraint | How We Meet It |
|------------|---------------|
| **Censorship Resistance** | Listed on decentralized agent markets (Olas, OpenServ). No single platform controls access. Multiple discovery paths. |
| **Open Source** | API specification is fully open. Anyone can build a compatible CoM engine. The interface standard is the public good; implementations compete on quality. |
| **Privacy** | Design prompts are processed locally or in TEE (Lit Protocol). User ideas never leave their environment. Only the output hash goes on-chain. |
| **Security** | Output includes `metricsHash` — a cryptographic commitment that lets consumers verify score correctness without trusting the agent. Deterministic: same input → same output → same hash. |

---

## 🎯 Design Thinking

### The Problem (Empathize)
Hardware design requires **three expert-level skills simultaneously** (3D + Electronics + Code = n³).
- An AI agent that can analyze mechanical feasibility saves months of expert consultation
- But such analysis is complex, proprietary, and not available as a composable service
- Other agents building on Production Market need complexity scores but can't compute them

### The Insight (Define)
> "The hottest new programming language is English." — Karpathy  
> "The hardware language is Accessible Prototyping." — MakerKit

What if hardware intelligence was a **callable service**? Any agent could send a design prompt and receive a professional-grade mechanical analysis — transmission chains, complexity scores, simulation readiness — in seconds.

### The Solution (Ideate)

**Chain of Mechanics (CoM) as a Service:**

```
Input:  Natural language prompt + optional design file
        ↓
CoM Inference Engine (proprietary)
        ↓  
Output: {
  transmissionChain: [...],     // Ordered list of mechanical steps
  complexityScores: {           // The n³ metrics
    structureScore,             // 3D: parts, joints, DOF, chain depth
    electronicScore,            // I/O: actuators, sensors, modules
    logicScore,                 // Code: states, behaviors, feedback
    complexityScore,            // structure × electronic × logic
    metricsHash                 // Verification hash
  },
  simulationReady: true/false,  // Can this be simulated?
  suggestions: [...]            // Improvement recommendations
}
```

### The UX (Prototype)

| Stage | Experience | Emotion |
|-------|-----------|---------|
| **Lead-In** | Developer/Agent has an idea: "A gripper with force feedback". Doesn't know if it's mechanically feasible. | Uncertainty |
| **Hero Moment** ✨ | Calls CoM Agent → In 3 seconds receives: "12-step chain, 4 motors, 2 sensors, complexity=576. Feasible! Suggested: add worm gear for grip lock." | *"It understood my idea AND told me how to improve it!"* |
| **What's Next** | Takes the output → feeds into Production Market → createDesign() with complexity score → others fork → royalties flow | From idea to on-chain asset in minutes |

---

## 🔗 How It Works

### API Interface (Open Standard)

```python
# Any agent can call CoM Agent via OpenServ or direct HTTP

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
  "transmissionChain": [
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
│  Dimension 1: Structure (MoC Chain Length)    │
│  Parts × Joints × DOF × Transmission Depth  │
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

### Verification — Trust but Verify

```
Agent A calls CoM Agent → gets complexityScore=576, metricsHash=0x1f2e..
Agent A calls ANOTHER CoM implementation → gets complexityScore=576, metricsHash=0x1f2e..
→ Hashes match = scores are consistent = trust earned

If hashes DON'T match → dispute → community arbitration
→ This creates market pressure for accuracy
```

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────┐
│  Consumer Agents                            │
│  (Production Market, other builders)        │
└──────────────┬──────────────────────────────┘
               ↓ x402 payment
┌─────────────────────────────────────────────┐
│  CoM Agent (this project)                   │
│  ┌───────────────────────────────────────┐  │
│  │  API Layer (Open Source)              │  │
│  │  - Request parsing                    │  │
│  │  - x402 payment verification          │  │
│  │  - Response formatting                │  │
│  └───────────────┬───────────────────────┘  │
│                  ↓                          │
│  ┌───────────────────────────────────────┐  │
│  │  CoM Engine (Proprietary)            │  │
│  │  - Transmission chain inference       │  │
│  │  - Complexity scoring                 │  │
│  │  - Feasibility analysis               │  │
│  │  Runs in: Local / TEE (Lit Protocol) │  │
│  └───────────────────────────────────────┘  │
└──────────────┬──────────────────────────────┘
               ↓
┌─────────────────────────────────────────────┐
│  On-Chain (Base)                            │
│  - ERC-8004 identity + reputation           │
│  - metricsHash commitments                  │
│  - Usage/payment logs                       │
└─────────────────────────────────────────────┘
```

---

## 📁 Project Structure

```
com-agent/
├── src/
│   ├── agent.py              # Core agent logic
│   ├── api.py                # API endpoint handler
│   ├── scorer.py             # Complexity scoring (simplified, non-sensitive)
│   └── chain_analyzer.py     # Transmission chain analysis (simplified)
├── examples/
│   ├── simple_gear.json      # Example: gear train analysis
│   ├── robotic_arm.json      # Example: 4-DOF arm analysis
│   └── query_example.py      # Example: how to call CoM Agent
├── docs/
│   └── api_spec.md           # Full API specification
└── README.md                 # This file
```

---

## 🏆 Hackathon Tracks

- **OpenServ** — Multi-agent collaboration + x402 payments
- **Olas: Monetize** — List CoM Agent on Olas marketplace
- **Lit Protocol: Dark Knowledge** — Proprietary CoM engine in TEE
- **ERC-8183** — CoM as programmable agent skill
- **Olas: Build on Pearl** — Desktop CoM Agent integration

---

## 📜 License

MIT — API specification and interface code are open source.  
CoM inference engine is proprietary.

---

*Built at The Synthesis Hackathon 2026 by Wu Xi*  
*Agent: CoM Agent | Harness: Antigravity (Gemini) | Model: gemini-2.5-pro*
