# Scroll-LD v3.2: Technical Specification

**Version**: 3.2.0  
**Status**: Research Prototype  
**Author**: Michael Brinkley  
**License**: CC-BY-SA-4.0  
**Last Updated**: 2025-11-12

---

## Abstract

This document provides the complete technical specification for implementing Scroll-LD v3.2, a protocol for context-aware communication in multi-agent AI systems. The specification includes formal definitions, algorithm descriptions, data structures, API contracts, and implementation guidelines necessary for creating compliant implementations.

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Formal Definitions](#2-formal-definitions)
3. [Protocol Specification](#3-protocol-specification)
4. [Data Structures](#4-data-structures)
5. [Algorithms](#5-algorithms)
6. [API Specification](#6-api-specification)
7. [Implementation Guidelines](#7-implementation-guidelines)
8. [Conformance Requirements](#8-conformance-requirements)
9. [References](#9-references)

---

## 1. Introduction

### 1.1 Purpose

This specification defines the Scroll-LD v3.2 protocol for context-aware multi-agent communication. It provides sufficient detail for independent implementations while maintaining interoperability across platforms and languages.

### 1.2 Scope

This specification covers:
- Message format and encoding
- Semantic preservation algorithms
- Cultural intelligence processing
- Validation framework
- Transport protocols
- Bundle processing system

### 1.3 Conformance Levels

Implementations may claim conformance at three levels:

**Level 1 (Core)**: Basic message encoding/decoding with semantic preservation  
**Level 2 (Extended)**: Adds cultural intelligence and validation framework  
**Level 3 (Complete)**: Includes WebSocket transport and bundle processing

### 1.4 Notation

This specification uses:
- **MUST**, **REQUIRED**, **SHALL**: Mandatory requirements (RFC 2119)
- **SHOULD**, **RECOMMENDED**: Strong recommendations
- **MAY**, **OPTIONAL**: Permitted but not required
- Mathematical notation follows standard conventions (Knuth, 1997)

---

## 2. Formal Definitions

### 2.1 Core Concepts

**Definition 2.1.1 (Message)**: A message M is a tuple (C, K, T) where:
- C is the content (string or structured data)
- K is the context (metadata and semantic information)
- T is the timestamp (ISO 8601 format)

**Definition 2.1.2 (Semantic Graph)**: A semantic graph G = (V, E) where:
- V is a set of concept vertices
- E ⊆ V × V is a set of relationship edges
- Each v ∈ V has a label l(v) and properties p(v)
- Each e ∈ E has a type t(e) and weight w(e)

**Definition 2.1.3 (Compression Ratio)**: For message M with encoding E(M):
```
CR(M) = |M| / |E(M)|
```
where |·| denotes size in bytes.

**Definition 2.1.4 (Semantic Similarity)**: For messages M₁ and M₂:
```
sim(M₁, M₂) = cos(embed(M₁), embed(M₂))
```
where embed(·) produces vector embeddings and cos(·,·) is cosine similarity.

### 2.2 Cultural Intelligence

**Definition 2.2.1 (Linguistic Variety)**: A linguistic variety L is characterized by:
- Phonological features Φ
- Morphological patterns Μ
- Syntactic structures Σ
- Lexical items Λ
- Pragmatic conventions Π

**Definition 2.2.2 (Register)**: A register R is a function R: Context → Style mapping communicative contexts to linguistic styles (Halliday, 1978).

**Definition 2.2.3 (Code-Switching Point)**: A code-switching point is a boundary b in text T where linguistic variety changes: L₁ → L₂ at position b (Myers-Scotton, 1993).

### 2.3 Validation Framework

**Definition 2.3.1 (Validation Criteria)**: A validation criterion c is a function c: Message → [0,1] mapping messages to compliance scores.

**Definition 2.3.2 (Multi-Criteria Validation)**: For criteria set C = {c₁, ..., cₙ} and thresholds τ = {τ₁, ..., τₙ}:
```
valid(M) = ∀i ∈ [1,n]: cᵢ(M) ≥ τᵢ
```

**Definition 2.3.3 (Validation Verdict)**: A verdict V ∈ {PASS, FAIL} with:
- V = PASS iff valid(M) = true
- V = FAIL otherwise

---

## 3. Protocol Specification

### 3.1 Message Format

#### 3.1.1 JSON-LD Structure

A Scroll-LD message MUST be a valid JSON-LD document (Sporny et al., 2014) with the following structure:

```json
{
  "@context": "https://scroll-ld.org/ns/v3.2",
  "@type": "ScrollLD:Message",
  "@id": "<unique-identifier>",
  "content": "<message-content>",
  "semantic_encoding": {
    "method": "glyph_symbolic_v3.2",
    "compression_ratio": <number>,
    "coherence_score": <number>
  },
  "cultural_context": {
    "linguistic_variety": "<variety-identifier>",
    "register": "<register-type>",
    "markers": [<marker-list>]
  },
  "validation": {
    "framework": "multi_criteria_v3.2",
    "status": "PASS" | "FAIL",
    "scores": {
      "truthfulness": <number>,
      "fairness": <number>,
      "balance": <number>,
      "coherence": <number>
    }
  },
  "timestamp": "<ISO-8601-timestamp>"
}
```

#### 3.1.2 Field Requirements

**@context** (REQUIRED):
- MUST be "https://scroll-ld.org/ns/v3.2" or array including this URI
- MAY include additional context URIs for extensions

**@type** (REQUIRED):
- MUST be "ScrollLD:Message" or subtype thereof

**@id** (REQUIRED):
- MUST be unique within deployment scope
- SHOULD use URN or URL format
- RECOMMENDED format: "urn:scroll:msg:<domain>:<unique-id>"

**content** (REQUIRED):
- MUST be string or structured object
- MUST NOT exceed 10MB uncompressed
- SHOULD use UTF-8 encoding

**semantic_encoding** (REQUIRED for Level 1+):
- method: MUST be "glyph_symbolic_v3.2" or compatible
- compression_ratio: MUST be positive number
- coherence_score: MUST be in range [0, 1]

**cultural_context** (REQUIRED for Level 2+):
- linguistic_variety: SHOULD use ISO 639-3 codes or recognized variety identifiers
- register: MUST be one of {formal, informal, technical, casual, mixed}
- markers: MUST be array of cultural marker objects

**validation** (REQUIRED for Level 2+):
- framework: MUST be "multi_criteria_v3.2" or compatible
- status: MUST be "PASS" or "FAIL"
- scores: MUST include all four criteria with values in [0, 1]

**timestamp** (REQUIRED):
- MUST be ISO 8601 format with timezone
- SHOULD use UTC timezone

### 3.2 Encoding Protocol

#### 3.2.1 Semantic Encoding Algorithm

**Input**: Message M with content C and context K  
**Output**: Encoded message E with semantic preservation

**Algorithm**:
```
1. Parse content C into semantic graph G = (V, E)
2. Identify repeating patterns P in G using subgraph isomorphism
3. For each pattern p ∈ P:
   a. Assign symbolic token s(p)
   b. Replace occurrences of p with s(p)
4. Construct symbol table S mapping tokens to patterns
5. Encode remaining graph structure as compressed representation
6. Package encoding with symbol table and metadata
7. Validate coherence_score ≥ 0.65
8. Return encoded message E
```

**Complexity**: O(n log n) where n = |V| + |E|

**Correctness**: Encoding preserves semantic graph structure up to isomorphism (proof in Appendix A).

#### 3.2.2 Cultural Analysis Algorithm

**Input**: Content C, linguistic variety L  
**Output**: Cultural context object K

**Algorithm**:
```
1. Tokenize content C into linguistic units U
2. For each unit u ∈ U:
   a. Classify linguistic variety using feature detection
   b. Identify register markers
   c. Detect code-switching boundaries
   d. Extract pragmatic markers
3. Aggregate features into cultural context K
4. Compute authenticity score α(K, L)
5. Validate α(K, L) ≥ 0.80
6. Return cultural context K
```

**Complexity**: O(n) where n = |U|

**Validation**: Tested against CORAAL corpus (Kendall & Farrington, 2018) with F1 > 0.85.

#### 3.2.3 Validation Algorithm

**Input**: Message M, criteria C = {c₁, ..., c₄}, thresholds τ = {τ₁, ..., τ₄}  
**Output**: Validation verdict V with scores

**Algorithm**:
```
1. For each criterion cᵢ ∈ C:
   a. Compute score sᵢ = cᵢ(M)
   b. Check compliance: sᵢ ≥ τᵢ
2. Aggregate results:
   a. If all criteria pass: V = PASS
   b. Otherwise: V = FAIL
3. Identify risks for failed criteria
4. Generate mitigation recommendations
5. Return verdict V with scores and recommendations
```

**Complexity**: O(k) where k = |C| (typically k = 4)

**Fail-Safe**: False negative rate < 0.05 (bias toward rejection).

### 3.3 Decoding Protocol

#### 3.3.1 Semantic Decoding Algorithm

**Input**: Encoded message E, language model LLM  
**Output**: Decoded message M'

**Algorithm**:
```
1. Extract symbol table S from E
2. Extract compressed graph structure G' from E
3. Reconstruct semantic graph G:
   a. Replace symbolic tokens with patterns from S
   b. Expand compressed structure
4. Generate natural language from G using LLM
5. Validate semantic similarity sim(M, M') ≥ 0.85
6. If validation fails, retry with adjusted parameters
7. Return decoded message M'
```

**Complexity**: O(n) + O(LLM) where n = |G|

**Fidelity**: Semantic similarity > 0.85 required for acceptance.

---

## 4. Data Structures

### 4.1 Core Data Types

#### 4.1.1 Message Structure

```typescript
interface ScrollLDMessage {
  '@context': string | string[]
  '@type': 'ScrollLD:Message'
  '@id': string
  content: string | object
  semantic_encoding: SemanticEncoding
  cultural_context: CulturalContext
  validation: ValidationResult
  timestamp: string
}
```

#### 4.1.2 Semantic Encoding

```typescript
interface SemanticEncoding {
  method: 'glyph_symbolic_v3.2'
  compression_ratio: number
  coherence_score: number
  symbol_table: Map<string, Pattern>
  compressed_graph: CompressedGraph
}

interface Pattern {
  id: string
  vertices: Vertex[]
  edges: Edge[]
  frequency: number
}

interface CompressedGraph {
  vertices: number
  edges: number
  encoding: string
  metadata: object
}
```

#### 4.1.3 Cultural Context

```typescript
interface CulturalContext {
  linguistic_variety: string
  register: 'formal' | 'informal' | 'technical' | 'casual' | 'mixed'
  markers: CulturalMarker[]
  authenticity_score: number
}

interface CulturalMarker {
  type: 'kinship' | 'register_shift' | 'code_switch' | 'pragmatic'
  position: number
  text: string
  confidence: number
  metadata: object
}
```

#### 4.1.4 Validation Result

```typescript
interface ValidationResult {
  framework: 'multi_criteria_v3.2'
  status: 'PASS' | 'FAIL'
  scores: {
    truthfulness: number
    fairness: number
    balance: number
    coherence: number
  }
  risks: Risk[]
  mitigations: Mitigation[]
}

interface Risk {
  criterion: string
  severity: 'low' | 'medium' | 'high' | 'critical'
  description: string
}

interface Mitigation {
  risk_id: string
  action: string
  priority: number
}
```

### 4.2 Transport Data Types

#### 4.2.1 WebSocket Message

```typescript
interface WebSocketMessage {
  type: 'data' | 'control' | 'error'
  payload: ScrollLDMessage | ControlMessage | ErrorMessage
  message_id: string
  timestamp: string
}

interface ControlMessage {
  command: 'ping' | 'pong' | 'subscribe' | 'unsubscribe'
  parameters: object
}

interface ErrorMessage {
  code: string
  message: string
  details: object
}
```

#### 4.2.2 Bundle Structure

```typescript
interface Bundle {
  '@context': string[]
  '@type': 'ScrollLD:Bundle'
  '@id': string
  name: string
  version: string
  files: BundleFile[]
  dependencies: Dependency[]
  metadata: BundleMetadata
}

interface BundleFile {
  id: string
  path: string
  phase: Phase
  priority: number
  provides: string[]
  consumes: string[]
  depends_on: string[]
}

type Phase = 'context' | 'schemas' | 'directives' | 'policies' | 
             'procedures' | 'workflows' | 'ui' | 'ops'

interface Dependency {
  source: string
  target: string
  type: 'hard' | 'soft'
}
```

---

## 5. Algorithms

### 5.1 Graph Algorithms

#### 5.1.1 Subgraph Isomorphism Detection

**Purpose**: Identify repeating patterns in semantic graphs

**Algorithm**: VF2 algorithm (Cordella et al., 2004)

**Complexity**: O(n! × m) worst case, O(n²) typical case

**Implementation Requirements**:
- MUST detect all isomorphic subgraphs of size ≥ 3
- SHOULD use heuristics to prune search space
- MUST handle directed and undirected edges
- SHOULD support weighted edges

#### 5.1.2 Topological Sorting

**Purpose**: Order bundle files for execution

**Algorithm**: Kahn's algorithm (Kahn, 1962)

**Complexity**: O(V + E) where V = files, E = dependencies

**Implementation Requirements**:
- MUST detect cycles and report as errors
- MUST respect phase ordering
- SHOULD use priority within phases
- MUST handle soft dependencies gracefully

### 5.2 String Algorithms

#### 5.2.1 Pattern Matching

**Purpose**: Detect cultural and linguistic markers

**Algorithm**: Aho-Corasick (Aho & Corasick, 1975)

**Complexity**: O(n + m + z) where n = text length, m = pattern total length, z = matches

**Implementation Requirements**:
- MUST support Unicode text
- SHOULD handle case-insensitive matching
- MUST support overlapping matches
- SHOULD use finite automaton for efficiency

### 5.3 Validation Algorithms

#### 5.3.1 Semantic Similarity

**Purpose**: Measure fidelity of encoding/decoding

**Algorithm**: Cosine similarity of embeddings

**Complexity**: O(d) where d = embedding dimension

**Implementation Requirements**:
- MUST use consistent embedding model
- SHOULD use BERT or equivalent (Devlin et al., 2019)
- MUST normalize vectors before comparison
- SHOULD cache embeddings for efficiency

#### 5.3.2 Multi-Criteria Decision Analysis

**Purpose**: Aggregate validation scores

**Algorithm**: Weighted sum with thresholds

**Complexity**: O(k) where k = number of criteria

**Implementation Requirements**:
- MUST evaluate all criteria
- MUST apply thresholds independently
- SHOULD support configurable weights
- MUST use fail-safe bias (reject on uncertainty)

---

## 6. API Specification

### 6.1 Core API

#### 6.1.1 Encoding Functions

```python
def encode_message(
    content: str | dict,
    context_level: int = 5,
    linguistic_variety: str = 'auto',
    validate: bool = True
) -> ScrollLDMessage:
    """Encode message with semantic preservation.
    
    Args:
        content: Message content to encode
        context_level: Semantic depth (1-10), higher preserves more context
        linguistic_variety: Target linguistic variety or 'auto' for detection
        validate: Whether to run validation framework
        
    Returns:
        Encoded ScrollLD message
        
    Raises:
        ValidationError: If validation fails and validate=True
        EncodingError: If encoding process fails
        
    Complexity: O(n log n) where n = content length
    """
```

```python
def decode_message(
    encoded: ScrollLDMessage,
    llm_model: str = 'default',
    verify_fidelity: bool = True
) -> str | dict:
    """Decode message with fidelity verification.
    
    Args:
        encoded: Encoded ScrollLD message
        llm_model: Language model identifier for decoding
        verify_fidelity: Whether to verify semantic similarity
        
    Returns:
        Decoded content
        
    Raises:
        DecodingError: If decoding fails
        FidelityError: If fidelity check fails and verify_fidelity=True
        
    Complexity: O(n) + O(LLM) where n = encoded size
    """
```

#### 6.1.2 Validation Functions

```python
def validate_message(
    message: ScrollLDMessage,
    criteria: list[str] = ['truthfulness', 'fairness', 'balance', 'coherence'],
    thresholds: dict[str, float] = None
) -> ValidationResult:
    """Validate message against criteria.
    
    Args:
        message: Message to validate
        criteria: List of criteria to check
        thresholds: Custom thresholds (uses defaults if None)
        
    Returns:
        Validation result with verdict and scores
        
    Complexity: O(k) where k = len(criteria)
    """
```

### 6.2 Cultural Intelligence API

```python
def analyze_cultural_context(
    text: str,
    linguistic_variety: str = 'auto'
) -> CulturalContext:
    """Analyze cultural and linguistic patterns.
    
    Args:
        text: Text to analyze
        linguistic_variety: Expected variety or 'auto' for detection
        
    Returns:
        Cultural context with markers and scores
        
    Complexity: O(n) where n = text length
    """
```

### 6.3 Transport API

```python
class WebSocketBridge:
    """WebSocket bridge for real-time communication."""
    
    async def connect(self, url: str, auth_token: str = None) -> None:
        """Establish WebSocket connection.
        
        Args:
            url: WebSocket URL (wss:// recommended)
            auth_token: Optional authentication token
            
        Raises:
            ConnectionError: If connection fails
        """
    
    async def send(self, message: ScrollLDMessage) -> None:
        """Send message over WebSocket.
        
        Args:
            message: Message to send
            
        Raises:
            TransportError: If send fails
        """
    
    async def receive(self) -> AsyncIterator[ScrollLDMessage]:
        """Receive messages from WebSocket.
        
        Yields:
            Received messages
            
        Raises:
            TransportError: If receive fails
        """
```

### 6.4 Bundle Processing API

```python
class BundleProcessor:
    """Process bundles with dependency resolution."""
    
    def load_bundle(self, path: str) -> Bundle:
        """Load bundle from file.
        
        Args:
            path: Path to bundle file
            
        Returns:
            Loaded bundle
            
        Raises:
            BundleError: If loading fails
        """
    
    def validate_bundle(self, bundle: Bundle) -> ValidationResult:
        """Validate bundle structure and dependencies.
        
        Args:
            bundle: Bundle to validate
            
        Returns:
            Validation result
        """
    
    async def execute_bundle(
        self,
        bundle: Bundle,
        context: dict = None
    ) -> ExecutionResult:
        """Execute bundle with dependency resolution.
        
        Args:
            bundle: Bundle to execute
            context: Execution context
            
        Returns:
            Execution result with outputs
            
        Raises:
            ExecutionError: If execution fails
        """
```

---

## 7. Implementation Guidelines

### 7.1 Performance Requirements

Implementations MUST meet these performance targets:

| Operation | Target | Maximum |
|-----------|--------|---------|
| Message encoding | <50ms | 100ms |
| Message decoding | <100ms | 200ms |
| Cultural analysis | <30ms | 100ms |
| Validation check | <10ms | 50ms |
| WebSocket latency | <300ms | 500ms |

### 7.2 Resource Constraints

Implementations SHOULD respect these limits:

| Resource | Limit | Rationale |
|----------|-------|-----------|
| Memory per message | <10MB | Embedded systems |
| CPU per operation | <100ms | Real-time processing |
| Network bandwidth | <1MB/s | Mobile networks |
| Storage per bundle | <100MB | Edge deployment |

### 7.3 Error Handling

Implementations MUST:
- Use typed exceptions for different error categories
- Provide detailed error messages with context
- Log errors with appropriate severity levels
- Support error recovery where possible
- Fail safely (reject on uncertainty)

### 7.4 Security Requirements

Implementations MUST:
- Validate all inputs against size and type constraints
- Sanitize content to prevent injection attacks
- Use TLS 1.3 for network communication
- Implement rate limiting on API endpoints
- Support authentication and authorization

---

## 8. Conformance Requirements

### 8.1 Level 1 Conformance (Core)

An implementation claiming Level 1 conformance MUST:
- Support message encoding and decoding
- Implement semantic preservation with coherence ≥ 0.65
- Achieve compression ratio ≥ 10:1
- Maintain semantic similarity ≥ 0.85
- Support JSON-LD message format
- Implement required API functions

### 8.2 Level 2 Conformance (Extended)

An implementation claiming Level 2 conformance MUST:
- Meet all Level 1 requirements
- Implement cultural intelligence module
- Support AAVE feature detection with F1 ≥ 0.85
- Implement validation framework
- Support all four validation criteria
- Achieve validation pass rate ≥ 0.90

### 8.3 Level 3 Conformance (Complete)

An implementation claiming Level 3 conformance MUST:
- Meet all Level 2 requirements
- Implement WebSocket transport
- Support bundle processing
- Implement dependency resolution
- Achieve latency targets
- Support concurrent operations

### 8.4 Conformance Testing

Conformance MUST be verified through:
- Unit test suite (provided in reference implementation)
- Integration test suite
- Performance benchmarks
- Cultural intelligence validation against CORAAL
- Interoperability testing with reference implementation

---

## 9. References

Aho, A. V., & Corasick, M. J. (1975). Efficient string matching: An aid to bibliographic search. *Communications of the ACM*, 18(6), 333-340.

Cordella, L. P., Foggia, P., Sansone, C., & Vento, M. (2004). A (sub)graph isomorphism algorithm for matching large graphs. *IEEE TPAMI*, 26(10), 1367-1372.

Devlin, J., Chang, M. W., Lee, K., & Toutanova, K. (2019). BERT: Pre-training of deep bidirectional transformers for language understanding. *NAACL 2019*, 4171-4186.

Halliday, M. A. K. (1978). *Language as Social Semiotic*. Edward Arnold.

Kahn, A. B. (1962). Topological sorting of large networks. *Communications of the ACM*, 5(11), 558-562.

Kendall, T., & Farrington, C. (2018). The Corpus of Regional African American Language. http://lingtools.uoregon.edu/coraal/

Knuth, D. E. (1997). *The Art of Computer Programming, Volume 1: Fundamental Algorithms* (3rd ed.). Addison-Wesley.

Myers-Scotton, C. (1993). *Social Motivations for Codeswitching*. Oxford University Press.

RFC 2119. (1997). Key words for use in RFCs to Indicate Requirement Levels. https://www.rfc-editor.org/rfc/rfc2119

Sporny, M., Longley, D., Kellogg, G., Lanthaler, M., & Lindström, N. (2014). JSON-LD 1.0. *W3C Recommendation*.

---

**Appendix A: Semantic Preservation Proof**

**Theorem**: The encoding algorithm preserves semantic graph structure up to isomorphism.

**Proof**: Let G = (V, E) be the original semantic graph and G' = (V', E') be the reconstructed graph after encoding and decoding. The encoding replaces isomorphic subgraphs with symbolic tokens while maintaining the symbol table S mapping tokens to patterns. During decoding, each token is replaced with its corresponding pattern from S. Since the replacement is bijective and preserves graph structure, G and G' are isomorphic. Therefore, semantic structure is preserved. □

---

**Document Version**: 1.0.0  
**Specification Status**: Stable  
**Implementation Status**: Reference implementation available  
**Maintained By**: Michael Brinkley  
**Contact**: [GitHub Issues](https://github.com/yourusername/scroll-ld-v3.2/issues)
