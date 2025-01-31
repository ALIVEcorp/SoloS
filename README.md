SoloS Artificial Intelligence
=========================================
![banner](https://github.com/ALIVEcorp/SoloS/blob/main/routes/photo/banner2.png)

# Provable AI Agent Authenticity

** PREVIEW OF UNRELEASED CODEBASE

Introduction
------------
SoloS is a system for establishing trust and verifiability in the execution of autonomous AI agents. It generates cryptographically secure logs of an agent's internal state transitions and communications, creating an immutable record that can be audited to confirm the agent's authentic operation.

<img width="704" alt="state" src="https://github.com/ALIVEcorp/SoloS/blob/main/routes/photo/field3.png" />

System Overview
---------------
At the core of SoloS is a state machine that models an agent's behavior as a series of state transitions. Each transition represents a change in the agent's internal state and includes associated metadata such as the action that triggered it.

As the agent operates, the state machine securely logs each transition along with a cryptographic proof. These proofs form a hash chain rooted in a Merkle tree, ensuring the integrity and non-repudiation of the execution trace.

Key Components:
- AgentState: an enum defining the possible states an agent can be in (IDLE, INIT, GOAL_PARSE, PLANNING, EXECUTING, etc.)
- StateTransition: an interface representing a transition between agent states, including the triggering action and associated data
- Proof: an interface defining the structure of a cryptographic transition proof, including state hashes, Merkle proofs, and digital signatures
- BaseState: a class providing core state tracking and cryptography functionality used by the state machine
- AgentStateMachine: the primary state machine implementation, responsible for managing state transitions and generating verifiable logs

Usage
-----
To use SoloS in an AI system:
1. Define the relevant AgentStates and valid transitions for your agent
2. Create an instance of the AgentStateMachine, providing a unique agent ID, session ID, and cryptographic key pair  
3. As the agent runs, use the `transitionTo` method to execute state changes, providing the destination state and associated action/metadata
4. The state machine will automatically generate secure logs for each transition, which can be accessed with `getLogs()`
5. Logs can be broadcasted for external auditing and verified using the provided proofs and signatures

Extending Functionality
-----------------------
SoloS is designed to be extensible for different agent architectures and use cases. Key areas for customization include:
- The AgentState enum and transition validity rules
- State entry/exit hooks and transition side-effects
- Broadcast mechanism for log distribution and external verification
- Logging format and storage 

The included `StateMachineLogger` class offers a reference implementation of structured logging with console output. For production systems, this can be adapted to integrate with a durable storage system and support advanced query/filtering functionality.

Future Directions
-----------------
SoloS modular architecture allows for the easy integration of new capabilities as the demands of autonomous agent verification evolve. Some potential areas for future development include:
- Support for multi-agent systems and inter-agent communication logging
- Integration with distributed ledgers or other decentralized infrastructure for tamperproof log persistence
- Automatic anomaly detection and real-time alerts for deviations from expected agent behavior
- Privacy-preserving verification using zero-knowledge proofs or secure multiparty computation
- User-friendly dashboard for exploring and analyzing agent execution traces

Phase 1 - Initialization
- Base State Machine implementation with self-validating merkle-chain log system
- LLM Layer for generative webpages & knowledge acquisition
- Web Scraping Layer
- IPFS Integration

Phase 2 - Enhanced Reasoning & Logging
- Extend logging to capture more granular agent state (e.g. individual perceptions, sub-goals, reasoning steps)
- Build monitoring dashboard with real-time views into agent operation and configurable alerts for anomalous behavior
- Enable "replay" functionality to step through agent execution traces for debugging and auditing

Phase 3 - Autonomous Agent Ecosystems
- SoloS Registry & Discovery service for SoloS agents to find and interact with each other
- Define standards for agent coordination, delegation, and mutual verification of task completion

Phase 4 - Multi-Agent Communication Protocols
- Define standard schemas for logging messages passed between SoloS-enabled agents based on Activity Pub
- Implement relay network for secure, verifiable routing of inter-agent communications
- Extend state machine to model interaction patterns and protocols between agent groups

This road map lays out an ambitious vision for evolving SoloS from a single-agent logging tool into a comprehensive framework for building transparent, accountable, and interoperable AI systems. The phased approach allows for iterative development guided by community input, with an ultimate aim of providing a robust scaffolding for provably beneficial artificial general intelligence. Key priorities include:

- Driving awareness and adoption within the AI development community 
- Expanding the range and granularity of data captured in execution logs
- Enabling secure, verifiable communication between SoloS-enabled agents
- Formalizing compliance and audit standards built on SoloS proofs
- Creating the software and economic infrastructure for thriving multi-agent ecosystems
- Leveraging SoloS as a platform for the transparent development of AGI

By providing a transparent, auditable foundation for AI agent development, SoloS aims to promote responsible innovation and mitigate risks as autonomous systems grow in sophistication and real-world impact. The road map represents a starting point for collaboratively advancing the technology in service of this mission.

## Getting Started

### Prerequisites

```bash
# Node.js v18+ required
node -v

# Install dependencies
npm install
```

### Environment Setup

Create a `.env` file with:

```env
CLAUDE_API_KEY=xxxx
IPFS_KEY=xxxx
POSTGRES_URL=xxxx
RAGIE_API_KEY=xxxx
RAGIE_API_KEY=xxxx
HELIS_SOLANA_URL=xxxx
HELIS_SOLANA_API_KEY=xxxx
```

### Basic Usage

```typescript
// Create a new persona agent
const agent = new PersonaSubAgent(
    "agent_id",
    "session_id",
    privateKeyHex
);

// Initialize with default persona
await agent.start(defaultPersona);

// Monitor state transitions
agent.getCurrentState();
agent.getEvolutionHistory();
```

### Running a Swarm

```typescript
import { startSwarm } from './swarm';

// Start multiple agents
await startSwarm(
    privateKeyHex,
    initialPersona,
    numAgents,
    "SWARM_PREFIX"
);
```

## State Machine Verification

The system uses cryptographic proofs for all state transitions:

```typescript
interface Proof {
    stateHash: string;     // Hash of current state
    prevHash: string;      // Hash of previous state
    merkleRoot: string;    // Root of Merkle tree
    merkleProof: string[]; // Proof path
    signature: string;     // Cryptographic signature
    timestamp: number;     // Proof generation time
}
```

## Persona Evolution

Personas evolve through a tree-based structure:

```typescript
interface PersonaStateData {
    personalityTraits: string[];
    goals: string[];
    interests: string[];
    background: string[];
    skills: string[];
    lore: string[];
    memories: string[];
    learnings: string[];
    patterns: string[];
    values: string[];
    prompt: string;
}
```

## API Endpoints

### Swarm Management

```
POST /start
{
    "privateKeyHex": string,
    "initialPersona": PersonaStateData,
    "numAgents": number,
    "agentPrefix": string
}

POST /end
```

## Database Schema

The system requires PostgreSQL with the following tables:

- `agent_personas`: Stores persona states and evolution history
- `execution_logs`: Stores state transition logs and proofs

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## Testing

```bash
npm test
```

## License

MIT License - see LICENSE file for details

## Technical Documentation

For detailed technical documentation, see:

- [State Machine Documentation](docs/state-machine.md)
- [Persona System](docs/persona-system.md)
- [Knowledge Integration](docs/knowledge-integration.md)
- [Cryptographic Verification](docs/crypto-verification.md)

## Credits

This project uses several key technologies:

- [Anthropic Claude API](https://www.anthropic.com/claude) for LLM integration
- [MerkleTreeJS](https://github.com/miguelmota/merkletreejs) for cryptographic proofs
- [Express](https://expressjs.com/) for API endpoints
- [PostgreSQL](https://www.postgresql.org/) for state storage

## Contact

For questions and support, please open an issue on GitHub.

