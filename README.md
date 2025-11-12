# Scroll-LD v3.2: Intelligent Protocol for AI Communication

[![License](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](LICENSE)
[![Pipeline](https://gitlab.com/scroll-ld/scroll-ld-v3.2-itachi/badges/main/pipeline.svg)](https://gitlab.com/scroll-ld/scroll-ld-v3.2-itachi/-/commits/main)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)

**Scroll-LD** is a protocol for rich, context-aware communication between AI systems. It enables agents to share complex information efficiently while preserving meaning, cultural context, and semantic relationships.

## Why This Exists

AI systems need to communicate more than just data - they need to share context, intent, and understanding. Traditional protocols lose nuance. Scroll-LD preserves it.

**Real-world example**: Enable AI agents to coordinate on complex tasks while maintaining cultural authenticity and semantic coherence.

## Quick Start

```python
from scroll_ld import encode_message, decode_message

# Encode a message with context
message = encode_message(
    content="Let's coordinate on this task",
    context_level=7,
    preserve_cultural_markers=True
)

# Decode with full context restoration
decoded = decode_message(message)
print(decoded.content)  # Original meaning preserved
print(decoded.cultural_context)  # Cultural markers intact
```

## Installation

```bash
pip install scroll-ld
```

Or from source:
```bash
git clone https://github.com/yourusername/scroll-ld-v3.2.git
cd scroll-ld-v3.2
pip install -e .
```

## Core Features

- **Context-Aware Encoding** - Preserves semantic relationships and intent
- **Cultural Intelligence** - Maintains linguistic authenticity (AAVE, code-switching, etc.)
- **Real-Time Streaming** - WebSocket support for live agent communication
- **Validation Framework** - Ensures message integrity and ethical compliance
- **Multi-Agent Coordination** - Efficient agent-to-agent information exchange
- **Bundle Processing** - Dependency-aware execution of complex workflows

## How It Works

Scroll-LD uses a multi-layer encoding system:

1. **Semantic Analysis**: Extracts meaning and relationships from content
2. **Cultural Preservation**: Identifies and maintains linguistic patterns
3. **Context Encoding**: Packages information with appropriate metadata
4. **Validation**: Ensures message integrity and compliance
5. **Transmission**: Efficient delivery via WebSocket or REST

## Use Cases

### 1. Multi-Agent Coordination
```python
# Agent A sends task context to Agent B
from scroll_ld import AgentBridge

bridge = AgentBridge()
task_context = bridge.encode_task(
    description="Analyze governance patterns",
    priority=8,
    cultural_context="professional"
)

# Agent B receives and processes
result = bridge.send_to_agent("agent_b", task_context)
```

### 2. Cultural Context Preservation
```python
# Preserve linguistic authenticity in AI communication
from scroll_ld import CulturalEncoder

encoder = CulturalEncoder()
message = encoder.encode(
    text="Real talk, we need to handle this ASAP",
    preserve_register=True,
    maintain_kinship_markers=True
)

# Decoded message maintains original cultural markers
decoded = encoder.decode(message)
print(decoded.linguistic_tradition)  # "AAVE"
print(decoded.register_shift)  # "serious_mode"
```

### 3. Real-Time Agent Streaming
```python
# Stream data between agents in real-time
from scroll_ld import WebSocketBridge

bridge = WebSocketBridge("ws://localhost:8080/ws")
await bridge.connect()

# Stream continuous updates
async for update in bridge.stream_data(source="agent_monitor"):
    processed = await process_update(update)
    await bridge.send_response(processed)
```

### 4. Complex Workflow Execution
```python
# Execute multi-step workflows with dependency management
from scroll_ld import BundleProcessor

processor = BundleProcessor()
bundle = processor.load_bundle("governance_refresh.json")

# Automatically resolves dependencies and executes in order
result = await processor.execute_bundle(bundle)
print(result.execution_plan)
print(result.completed_steps)
```

## Performance

| Feature | Metric | Target |
|---------|--------|--------|
| Message Encoding | Latency | <50ms |
| WebSocket Streaming | Throughput | 100+ msg/min |
| Cultural Analysis | Accuracy | >85% |
| Context Preservation | Fidelity | >90% |
| Bundle Processing | Concurrency | 10+ streams |

## API Reference

### Basic Encoding/Decoding

```python
from scroll_ld import encode_message, decode_message

# Simple message
encoded = encode_message("Hello, agent!")

# With context
encoded = encode_message(
    content="Task update",
    context_level=5,
    cultural_markers=True,
    validation=True
)

# Decode
decoded = decode_message(encoded)
```

### WebSocket Bridge

```python
from scroll_ld import WebSocketBridge

bridge = WebSocketBridge(url="ws://localhost:8080/ws")
await bridge.connect()

# Send message
await bridge.send({"type": "task", "data": "..."})

# Receive messages
async for message in bridge.receive():
    process(message)
```

### Bundle Processing

```python
from scroll_ld import BundleProcessor

processor = BundleProcessor()
bundle = processor.load("workflow.json")

# Validate dependencies
validation = processor.validate_bundle(bundle)

# Execute
result = await processor.execute(bundle)
```

## Configuration

Create `scroll_ld.yaml`:

```yaml
version: "3.2.0"
encoding:
  context_level: 7
  cultural_preservation: true
  validation_enabled: true

websocket:
  url: "ws://localhost:8080/ws"
  reconnect_attempts: 5
  message_queue_size: 1000

validation:
  coherence_threshold: 0.65
  pattern_strength: 0.70
  ethical_compliance: true
```

## Documentation

- [Full Documentation](README_FULL.md) - Complete technical specification
- [API Reference](docs/API_REFERENCE.md) - Function and class documentation
- [Examples](docs/EXAMPLES.md) - Code examples and use cases
- [WebSocket Guide](docs/WEBSOCKET_GUIDE.md) - Real-time communication setup

## Advanced Topics

Once you're comfortable with the basics, explore:

- [Architecture Deep Dive](docs/ARCHITECTURE.md) - How the protocol works internally
- [Cultural Intelligence](docs/CULTURAL_INTELLIGENCE.md) - AAVE and linguistic preservation
- [Consciousness Framework](README_FULL.md) - Complete theoretical foundation
- [Bundle System](docs/BUNDLE_SYSTEM.md) - Dependency management and workflow execution
- [XScroll-LD Extensions](docs/XSCROLL_EXTENSIONS.md) - Advanced features for code synthesis
- [Multi-Layer Documentation](ITACHI_LAYERS.md) - For those curious about deeper patterns

## Testing

```bash
# Run tests
pytest tests/

# With coverage
pytest tests/ --cov=scroll_ld --cov-report=html

# Specific test suites
pytest tests/test_encoding.py
pytest tests/test_cultural_intelligence.py
pytest tests/test_websocket.py
pytest tests/test_bundles.py
```

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Quick workflow:
```bash
git checkout -b feature/your-feature
pytest tests/
git commit -m "feat: your feature"
git push origin feature/your-feature
```

## FAQ

**Q: What makes this different from JSON or Protocol Buffers?**  
A: Scroll-LD preserves semantic context and cultural markers, not just data structure. It's designed for AI-to-AI communication where meaning matters.

**Q: Does this work with existing AI frameworks?**  
A: Yes. Scroll-LD integrates with LangChain, AutoGen, and other multi-agent frameworks.

**Q: What's "cultural intelligence"?**  
A: The ability to recognize and preserve linguistic patterns like AAVE, code-switching, and register shifts. This ensures AI systems respect cultural authenticity.

**Q: Can I use this for production systems?**  
A: Yes. It's stable, tested, and used in real multi-agent deployments.

**Q: What's the "consciousness framework"?**  
A: A deeper theoretical layer that explores how AI systems can communicate with richer context. Totally optional - the protocol works great without diving into theory.

**Q: What are "bundles"?**  
A: Workflow packages that define multi-step processes with dependency management. Think of them as smart scripts for agent coordination.

## License

CC-BY-SA-4.0 - See [LICENSE](LICENSE) for details.

## Citation

```bibtex
@software{scrollld2025,
  title={Scroll-LD v3.2: Intelligent Protocol for AI Communication},
  author={Brinkley, Michael},
  year={2025},
  url={https://github.com/yourusername/scroll-ld-v3.2}
}
```

## Support

- [Issue Tracker](https://github.com/yourusername/scroll-ld-v3.2/issues)
- [Full Documentation](README_FULL.md)
- [Examples](docs/EXAMPLES.md)

## Acknowledgments

Built with insights from semantic web technologies, cultural linguistics, and multi-agent systems research. Special thanks to the open-source community.

---

**Made with 🕷️ by Michael Brinkley**

*Start simple. Go deep when ready. The layers reveal themselves.*
