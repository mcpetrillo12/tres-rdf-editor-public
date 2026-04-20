**Platform-Independent RDF Data Management for the Modern Semantic Web**

TRèS is a comprehensive, enterprise-grade RDF (Resource Description Framework) editor built with Rust and eGUI. Designed to be completely independent of any specific graph database platform, TRèS empowers data engineers, knowledge architects, and semantic web practitioners with a unified interface for their day-to-day graph data operations.

**Version 2.9.8** - Licensed under Apache License 2.0

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

See [CHANGELOG.md](CHANGELOG.md) for release history.

## Key Features

### Enterprise Database Management
- **Multi-Platform Support**: Native support for Stardog, RDFox, Apache Jena Fuseki, GraphDB, and AllegroGraph
- **Environment Management**: Support for Dev/QA/Staging/Production endpoints per profile
- **Connection Profiles**: Save and quickly switch between database configurations
- **Connection Pooling**: Efficient resource management with automatic retry logic
- **Audit & Compliance**: Complete change tracking with user attribution and rollback capabilities
- **Snapshot Management**: Automatic snapshots before destructive operations with configurable retention
- **External Change Detection**: Auto-detect when database is modified externally with smart VDB refresh

### Advanced SPARQL Interface
- **Three Modes**: Query, Browse, and Update modes with syntax highlighting and validation
- **Multi-Tab Query Editor**: Work with multiple queries simultaneously
- **Query Library**: Save, organize, and share query collections
- **Template System**: Pre-built queries for common RDF operations
- **Results Export**: Multiple format support (CSV, JSON, TSV, Turtle, N-Triples)
- **Query History**: Complete audit trail of all executed queries
- **Browse Mode**: Visual exploration of classes, properties, instances, and attributes
- **External Editor Integration**: Round-trip editing with BBEdit, VS Code, and other editors
- **Send to Viz**: Push query or browse results directly to graph visualization

### Interactive Graph Visualization
- **VDB-Powered Intelligence**: Vector database classifies nodes as hubs, bridges, satellites, or terminators for intelligent layout
- **Dual Layout Modes**: Toggle between VDB-informed and degree-based layouts
- **11 Layout Rules**: Production-quality node placement with no overlaps, crossing minimization, and space optimization
- **Animated Expansion**: Stem-and-flower bloom animation with sequential timing
- **Search Integration**: Type-ahead search with chicklet-based selection and instant canvas placement
- **Path Finding**: Discover shortest paths between any two nodes with SPARQL query display
- **Deterministic Colors**: 12-color hand-picked palette with TopClass color persistence across sessions
- **SubClass Color Hierarchy**: Lighter shades based on VDB hierarchy depth
- **Interactive Controls**: Pan, zoom, fullscreen, drag, multi-select, expand, expand all, stop expansion
- **Details Panel**: Collapsible sections showing URI, metadata, relationships, attributes, instances, and literals
- **Filters**: Toggle Classes, Instances, rdf:type relationships, and subClassOf relationships

### Vocabulary & Taxonomy Management
- **SKOS Browser**: Navigate and edit SKOS concept schemes and hierarchies
- **Taxonomy Groups**: Local file-based organization of concept schemes with ordered collections
- **Labels & Descriptions**: Preferred/alternative labels, definitions, and scope notes with language support
- **Documentation Export**: HTML, Markdown, Word, CSV, JSON-LD formats
- **SKOS Export**: Native SKOS/Turtle export with proper semantic markup
- **Validation**: Orphan concepts, duplicate labels, and structural issue detection
- **Taxonomist-First Design**: Clean, polished interface designed for non-technical vocabulary managers

### Security & Compliance
- **Encrypted Credentials**: AES-256-GCM encryption for all database passwords
- **Zero-Configuration Security**: Automatic encryption using system-specific keys
- **Transparent Migration**: Plain text passwords automatically encrypted on first use
- **Query Validation**: SPARQL injection prevention with comprehensive input sanitization
- **Audit Logging**: Track all database operations with timestamps and user attribution
- **Rollback Generation**: Automatically generate queries to undo changes
- **Import Safety**: All-or-nothing imports with validation before graph clearing

### Multilingual Support
- **Language Preferences**: 11 presets plus custom input (ISO 639-1 codes)
- **Unicode Rendering**: Embedded fonts for Arabic, Japanese, Chinese, Latin, Greek, and Cyrillic
- **Smart Fallback**: Preferred language, then English, then untagged, then first available
- **SPARQL Language Filtering**: Built-in utilities to inject language preferences into queries

### Plugin System & Intelligence Layer
- **Integrated Vector Database**: In-memory VDB with automatic persistence per connection profile
- **Graph-Aware Indexing**: Canonical URI handling with separate ID namespaces per graph
- **Semantic Search**: Entity and relationship embeddings for intelligent traversal
- **Plugin Manager**: Browse and install plugins through intuitive UI
- **Available Plugins**:
  - **Embedded Fuseki**: Local RDF database for development and testing
  - **Tool Classification**: OWL rule-based reasoning with vector acceleration
  - **Spatial Reasoning**: Geospatial data analysis and visualization
  - **Ontology Training**: Train language models on your ontologies via Ollama bridge
- **AI-Powered Analysis**: Ollama integration for ontology summarization, validation, and NL-to-SPARQL training

## Installation

### Pre-built Binaries
Pre-built binaries are available for macOS, Windows, and Linux platforms.

### Build from Source
```bash
# Clone or extract source
cd tres

# Build release version
./build.sh release

# Run the application
./target/release/tres

# Run tests (1,375 tests)
./build.sh test

# Build macOS DMG installer (macOS only)
./build.sh dmg
```

### System Requirements
- **Rust**: 1.94+ (stable toolchain)
- **macOS**: 12.0+ (Apple Silicon and Intel)
- **Linux**: GTK3 development libraries required
- **Windows**: MSVC toolchain
