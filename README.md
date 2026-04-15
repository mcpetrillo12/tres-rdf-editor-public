# TRèS - Triple Store RDF Editor Suite

![TRèS](static/icon.png)

**Platform-Independent RDF Data Management for the Modern Semantic Web**

TRèS is a comprehensive, enterprise-grade RDF (Resource Description Framework) editor built with Rust and eGUI. Designed to be completely independent of any specific graph database platform, TRèS empowers data engineers, knowledge architects, and semantic web practitioners with a unified interface for their day-to-day graph data operations.

**Version 2.9.6** - Licensed under Apache License 2.0

## Why TRèS?

### True Platform Independence
TRèS isn't tied to any vendor or platform. Whether you're working with Stardog, RDFox, Fuseki, GraphDB, or AllegroGraph, TRèS provides a consistent, familiar interface that respects each platform's strengths while abstracting away the complexity of switching between them.

### Built for Daily Workflows
Rather than trying to replace vendor-specific admin consoles, TRèS excels at the tasks you do every day:
- **Quick Query Iterations**: Write once, run anywhere with smart SPARQL query management
- **Visual Data Exploration**: Understand complex relationships instantly with interactive graphs
- **Rapid Prototyping**: Test ideas across different triple stores without context switching
- **Documentation Generation**: Transform SKOS vocabularies into beautiful, shareable documentation
- **Cross-Platform Data Migration**: Move data seamlessly between different RDF stores

### Performance That Respects Your Time
Built in Rust with immediate-mode GUI rendering, TRèS is blazingly fast. No web browser overhead, no network latency for the UI, just pure native performance. Query results appear instantly, graphs render smoothly even with thousands of nodes, and the interface remains responsive under heavy workloads.

### Professional Tools, Thoughtful Design
Every feature in TRèS is designed with the practicing professional in mind:
- Multi-tab query editors that remember your work
- Smart namespace management that actually persists
- Graph visualizations that make sense at first glance
- Export formats that work with your existing toolchain
- Audit trails that satisfy compliance requirements

## New in v2.9.6

### Spreadsheet Import — Native Rust RML-Subset Engine
- **RML-Subset Mapping**: New backend engine translates spreadsheet rows (CSV/XLSX) into RDF triples using a native Rust implementation of an RML-compatible mapping subset — no external RML processor required
- **Phase 2 Backend**: Full pipeline from source file to validated graph, including typed literal coercion, URI template expansion, language tag handling, and join references across multiple logical sources
- **Load-Rule Enforcement**: Imports now enforce VDB loading rules, rejecting triples that would violate domain/range constraints or create orphan nodes before anything is written to the triple store

### CLI Tools for Automation & CI
- **`tres-import`**: Standalone binary for running spreadsheet imports from the command line — ideal for scripted data loads, batch conversions, and integration into CI pipelines. See [CLI Tools Reference](Documentation/public/CLI_TOOLS.md)
- **`tres-validate`**: Standalone RDF validation binary that runs the same validator used inside TReS — point it at a Turtle/N-Triples/N-Quads file to get exit-code-friendly pass/fail output suitable for pre-commit hooks and CI checks

## Documentation

- **[Getting Started](Documentation/public/GETTING_STARTED.md)**: Quick start guide for new users
- **[Operations Guide](Documentation/public/OPERATIONS.md)**: Complete user guide with tutorials and best practices
- **[Vocabulary Guide](Documentation/public/VOCABULARY_GUIDE.md)**: Managing SKOS vocabularies and taxonomies
- **[Ollama AI Guide](Documentation/public/OLLAMA_TRAINING_GUIDE.md)**: AI-powered ontology analysis setup
- **[Federated Queries](Documentation/public/FEDERATED_QUERIES_GUIDE.md)**: Cross-database query federation guide

## Quick Links

- **Current Version**: v2.9.6
- **All Releases**: [github.com/mcpetrillo12/tres-rdf-editor-public/releases](https://github.com/mcpetrillo12/tres-rdf-editor-public/releases)
- **v2.9.6 Downloads** (version-pinned):
  - Windows: [tres-v2.9.6-windows-x64.exe](https://github.com/mcpetrillo12/tres-rdf-editor-public/releases/download/v2.9.6/tres-v2.9.6-windows-x64.exe)
  - macOS (signed & notarized, recommended): [TRES-v2.9.6-macos.dmg](https://github.com/mcpetrillo12/tres-rdf-editor-public/releases/download/v2.9.6/TRES-v2.9.6-macos.dmg)
  - macOS (binary only): [tres-v2.9.6-macos](https://github.com/mcpetrillo12/tres-rdf-editor-public/releases/download/v2.9.6/tres-v2.9.6-macos)
  - Linux: [tres-v2.9.6-linux-x64](https://github.com/mcpetrillo12/tres-rdf-editor-public/releases/download/v2.9.6/tres-v2.9.6-linux-x64)
  - SHA256 Checksums: [checksums.txt](https://github.com/mcpetrillo12/tres-rdf-editor-public/releases/download/v2.9.6/checksums.txt)
- **Support**: info@taurusystems.com
- **Contributing**: See Developer Guide documentation

## Supported Platforms

### Enterprise RDF Databases

| Platform | Query Endpoint | Update Endpoint | Authentication | Special Features |
|----------|---------------|-----------------|----------------|------------------|
| **Stardog** | `/query` | `/update` | Basic Auth | Reasoning, Virtual Graphs |
| **RDFox** | `/sparql` | `/sparql` | API Key | Incremental Reasoning |
| **Fuseki** | `/query` | `/update` | Optional | Embedded Server Support |
| **GraphDB** | `/repositories/{repo}` | `/statements` | Token/Basic | Full-text Search |
| **AllegroGraph** | `/repositories/{repo}` | `/statements` | Basic Auth | Geospatial, Multi-model |

### Platform Intelligence

TRèS automatically adapts to each platform's specific requirements:
- **Default Graph Handling**: Platform-specific default graph URIs
- **Query Formatting**: Optimized query syntax for each platform
- **Full-Text Search**: Platform-specific FTS index discovery and query generation
- **Connection Management**: Platform-appropriate connection pooling
- **Error Handling**: Intelligent error interpretation and recovery

## Architecture

### Technology Stack
- **Framework**: eGUI (immediate mode GUI) for maximum performance
- **Language**: Rust for safety, speed, and reliability
- **Async Runtime**: Tokio for concurrent operations
- **HTTP Client**: reqwest with connection pooling
- **Intelligence Layer**: In-memory vector database with semantic indexing and persistence
- **Graph Engine**: StateManager-based architecture with topology pathfinding
- **RDF Parsing**: rio for standard-compliant RDF I/O

### Design Principles
- **Native Performance**: Direct GPU rendering, no web overhead
- **Platform Agnostic**: Works with any SPARQL 1.1 compliant endpoint
- **Privacy First**: All data stays local, no telemetry
- **VDB as Authority**: Single source of truth for node/edge IDs and type classification
- **Extensible**: Modular architecture for easy platform additions
- **Reliable**: Comprehensive error handling and recovery (1,375 tests)

## Contributing

We welcome contributions! Areas of interest:
- Additional RDF platform support
- Enhanced visualization features
- Query optimization tools
- Documentation improvements
- Internationalization
- Extension development (see [Extension Guide](extensions/README.md))

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

Apache License 2.0 - see [LICENSE](LICENSE) for details.

## Acknowledgments

- **Rust Community**: For excellent libraries and tooling
- **W3C RDF Working Group**: For SPARQL and RDF standards
- **Database Vendors**: For advancing the semantic web ecosystem
- **Contributors**: Everyone who has helped improve TRèS

## The TRèS Philosophy

TRèS believes that your tools should adapt to your workflow, not the other way around. Built on the principle that RDF professionals deserve a tool that:

- **Respects your expertise** by providing powerful features without unnecessary complexity
- **Values your time** with instant responses and efficient workflows
- **Travels with you** across different projects, platforms, and organizations
- **Grows with you** as the semantic web ecosystem evolves

Whether you're exploring a new dataset, debugging a complex query, presenting findings to stakeholders, or building the next generation of knowledge graphs, TRèS is the reliable companion that makes your RDF work more productive and enjoyable.

---

**TRèS** - The platform-independent RDF editor that puts practitioners first.

*Built for data engineers, knowledge architects, and semantic web practitioners who need tools that work as hard as they do.*

*Created by Matthew C. Petrillo*
