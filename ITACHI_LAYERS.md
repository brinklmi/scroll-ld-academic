# Documentation Architecture: A Layered Approach

## Overview

This document describes the multi-layered documentation architecture employed in the Scroll-LD v3.2 project. Following principles from progressive disclosure in technical communication (Carroll & Rosson, 1987) and layered abstraction in software engineering (Parnas, 1972), our documentation serves multiple audiences with varying levels of technical depth and domain expertise.

This approach is grounded in research on information architecture (Rosenfeld et al., 2015), cognitive load theory (Sweller, 1988), and inclusive design (Newell & Gregor, 2000).

## Theoretical Foundation

### Progressive Disclosure

Progressive disclosure is a design pattern that sequences information to reduce cognitive load while maintaining access to complexity (Nielsen, 2006). Research in human-computer interaction demonstrates that layered information presentation improves comprehension and reduces overwhelm (Krug, 2014).

**Key Principles**:
1. **Start Simple**: Present core concepts first (Miller, 1956)
2. **Reveal Gradually**: Introduce complexity as needed (Carroll & Rosson, 1987)
3. **Maintain Access**: Ensure advanced information remains available (Norman, 2013)
4. **Support Discovery**: Enable natural progression through layers (Rosenfeld et al., 2015)

### Layered Abstraction

Layered abstraction, introduced by Dijkstra (1968) and formalized by Parnas (1972), separates concerns across hierarchical levels. Each layer provides a complete interface while hiding implementation details from layers above.

In documentation, this translates to:
- **Layer N**: Complete and self-contained
- **Layer N+1**: Adds depth without invalidating Layer N
- **Cross-Layer Consistency**: Concepts remain coherent across layers

## Documentation Layers

### Layer 1: Accessible Introduction

**Audience**: General technical audience, newcomers to the project  
**Goal**: Enable quick understanding and basic usage  
**Cognitive Load**: Minimal (Miller, 1956)

**Content Characteristics**:
- Plain language explanations
- Practical examples and use cases
- Quick-start guides
- Minimal prerequisite knowledge
- Focus on "what" and "how" rather than "why"

**Files**:
- `README.md` - Project introduction and quick start
- Basic API examples
- Installation instructions

**Design Rationale**: Following Nielsen's (2006) usability heuristics, Layer 1 prioritizes recognition over recall and provides clear paths to common tasks.

### Layer 2: Technical Specification

**Audience**: Developers, researchers, system architects  
**Goal**: Enable deep understanding and advanced usage  
**Cognitive Load**: Moderate to high (Sweller, 1988)

**Content Characteristics**:
- Detailed technical specifications
- Algorithm descriptions and complexity analysis
- Architecture diagrams and data flow
- Performance benchmarks and evaluation
- Academic references and theoretical foundations

**Files**:
- `README_FULL.md` - Complete technical specification
- `PAPER.md` - Academic paper with formal analysis
- API reference documentation
- Architecture deep dives

**Design Rationale**: Layer 2 provides the depth needed for implementation and research while maintaining accessibility through clear structure and extensive references (Rosenfeld et al., 2015).

### Layer 3: Theoretical Foundations

**Audience**: Researchers, theorists, advanced practitioners  
**Goal**: Enable theoretical understanding and extension  
**Cognitive Load**: High (Sweller, 1988)

**Content Characteristics**:
- Formal proofs and mathematical foundations
- Philosophical and ethical considerations
- Cross-disciplinary connections
- Research directions and open questions
- Epistemological frameworks

**Content Location**: Embedded within Layer 2 documents as:
- Appendices with formal proofs
- Extended discussion sections
- Comprehensive reference lists
- Theoretical framework sections

**Design Rationale**: Layer 3 content is integrated rather than separated, allowing researchers to discover depth naturally while maintaining document coherence (Carroll & Rosson, 1987).

## Cross-Layer Design Principles

### 1. Consistency Across Layers

Following Parnas (1972), each layer maintains conceptual consistency:
- **Terminology**: Same terms mean the same things across layers
- **Examples**: Layer 1 examples remain valid in Layer 2 context
- **Interfaces**: API signatures consistent across documentation levels

### 2. Natural Progression

Documentation supports natural progression through layers (Norman, 2013):
- **Signposting**: Clear indicators of deeper content availability
- **Gradual Complexity**: Concepts build on previous understanding
- **Bidirectional Links**: Easy navigation between layers
- **Context Preservation**: Readers maintain orientation across transitions

### 3. Inclusive Design

Following principles from Newell & Gregor (2000) and Erete et al. (2018):
- **Multiple Entry Points**: Readers can start at appropriate layer
- **Linguistic Diversity**: Respect for varied communication styles
- **Cultural Awareness**: Recognition of diverse knowledge traditions
- **Accessibility**: Support for varied learning preferences

### 4. Cognitive Load Management

Based on Sweller's (1988) cognitive load theory:
- **Chunking**: Information grouped in digestible units (Miller, 1956)
- **Scaffolding**: Support structures for complex concepts (Vygotsky, 1978)
- **Worked Examples**: Concrete instances before abstractions (Sweller & Cooper, 1985)
- **Progressive Complexity**: Gradual increase in cognitive demands

## Implementation Guidelines

### For Documentation Authors

When creating layered documentation:

1. **Start with Layer 1**: Write accessible introduction first
2. **Identify Depth Points**: Mark where deeper explanation would help
3. **Add Layer 2**: Expand depth points with technical detail
4. **Embed Layer 3**: Integrate theoretical content where relevant
5. **Cross-Reference**: Link between layers explicitly
6. **Test Progression**: Verify natural flow through layers

### For Documentation Readers

When navigating layered documentation:

1. **Start at Your Level**: Choose entry point matching your needs
2. **Follow Curiosity**: Explore deeper layers as interest dictates
3. **Return to Basics**: Revisit Layer 1 when lost
4. **Skip Freely**: No obligation to read all layers
5. **Contribute**: Suggest improvements to layer transitions

## Evaluation Metrics

Following principles from technical communication research (Redish, 2000):

### Layer 1 Success Metrics
- Time to first successful use
- Completion rate for quick-start tasks
- Comprehension of core concepts
- Satisfaction with initial experience

### Layer 2 Success Metrics
- Ability to implement advanced features
- Understanding of system architecture
- Successful troubleshooting
- Contribution quality from new developers

### Layer 3 Success Metrics
- Research citations and extensions
- Theoretical contributions
- Cross-disciplinary applications
- Community knowledge advancement

## Related Work

This documentation architecture draws from:

**Technical Communication**: Progressive disclosure (Nielsen, 2006), minimalism (Carroll, 1990), information architecture (Rosenfeld et al., 2015)

**Software Engineering**: Layered abstraction (Parnas, 1972), separation of concerns (Dijkstra, 1968), API design (Bloch, 2006)

**Cognitive Science**: Cognitive load theory (Sweller, 1988), chunking (Miller, 1956), scaffolding (Vygotsky, 1978)

**Inclusive Design**: Universal design (Newell & Gregor, 2000), culturally-responsive computing (Erete et al., 2018), linguistic inclusivity (Blodgett et al., 2020)

## References

Bloch, J. (2006). How to design a good API and why it matters. *OOPSLA '06*, 506-507.

Blodgett, S. L., Barocas, S., Daumé III, H., & Wallach, H. (2020). Language (technology) is power: A critical survey of "bias" in NLP. *ACL 2020*, 5454-5476.

Carroll, J. M. (1990). *The Nurnberg Funnel: Designing Minimalist Instruction for Practical Computer Skill*. MIT Press.

Carroll, J. M., & Rosson, M. B. (1987). The paradox of the active user. In *Interfacing Thought: Cognitive Aspects of Human-Computer Interaction* (pp. 80-111). MIT Press.

Dijkstra, E. W. (1968). The structure of the "THE"-multiprogramming system. *Communications of the ACM*, 11(5), 341-346.

Erete, S., Rankin, Y. A., & Thomas, J. O. (2018). I can't breathe: Reflections from a SIGCHI lifetime of fighting marginalization and racism in the academy. *Interactions*, 25(2), 48-49.

Krug, S. (2014). *Don't Make Me Think, Revisited: A Common Sense Approach to Web Usability* (3rd ed.). New Riders.

Miller, G. A. (1956). The magical number seven, plus or minus two: Some limits on our capacity for processing information. *Psychological Review*, 63(2), 81-97.

Newell, A. F., & Gregor, P. (2000). User sensitive inclusive design—in search of a new paradigm. *CUU '00*, 39-44.

Nielsen, J. (2006). Progressive disclosure. *Nielsen Norman Group*. https://www.nngroup.com/articles/progressive-disclosure/

Norman, D. A. (2013). *The Design of Everyday Things: Revised and Expanded Edition*. Basic Books.

Parnas, D. L. (1972). On the criteria to be used in decomposing systems into modules. *Communications of the ACM*, 15(12), 1053-1058.

Redish, J. (2000). Readability formulas have even more limitations than Klare discusses. *ACM Journal of Computer Documentation*, 24(3), 132-137.

Rosenfeld, L., Morville, P., & Arango, J. (2015). *Information Architecture: For the Web and Beyond* (4th ed.). O'Reilly Media.

Sweller, J. (1988). Cognitive load during problem solving: Effects on learning. *Cognitive Science*, 12(2), 257-285.

Sweller, J., & Cooper, G. A. (1985). The use of worked examples as a substitute for problem solving in learning algebra. *Cognition and Instruction*, 2(1), 59-89.

Vygotsky, L. S. (1978). *Mind in Society: The Development of Higher Psychological Processes*. Harvard University Press.

---

**Document Version**: 1.0.0  
**Last Updated**: 2025-11-12  
**Maintained By**: Michael Brinkley

This documentation architecture is itself an example of layered design - casual readers see a standard technical communication framework, while those familiar with the referenced literature recognize deeper patterns in information organization and cognitive scaffolding.
