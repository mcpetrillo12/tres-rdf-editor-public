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

### Correctness Fixes
- **Scope Restriction Per Graph**: Scope-restriction queries now run per-graph instead of across the default union, eliminating cross-graph false positives during validation and browse operations
- **Graph Conflation in Load Ontology**: Fixed a bug where Load Ontology could merge entities from distinct named graphs when URIs overlapped; each graph now maintains strict entity isolation
- **Automated Layout Rule Tests**: New test suite exercises all 11 production layout rules on canonical ontology shapes to prevent layout regressions

## New in v2.9.5

### RDF Validation: Comment Handling Fix
- **Inline Comments**: Validator now correctly ignores inline comments (e.g., `marv:foo resources:bar ;  # note`) across Turtle, N-Triples, and N-Quads formats instead of flagging them as syntax errors
- **Comment-Only Lines**: Fixed `validate_string_literals` treating apostrophes in comment lines (e.g., `# It's Jeff!`) as unclosed string literals
- **URI Fragment Safety**: `#` inside URI fragments (e.g., `<http://example.org/ns#term>`) is correctly preserved and never mistaken for a comment
- **Prefix Check Fix**: `extract_non_string_content` now strips comments and tracks URI context, preventing false "undefined prefix" errors from text in comments

## New in v2.9.4

### Details Pane Redesign
- **Collapsible Sections**: All sections now use consistent CollapsingHeader controls -- Graph Info, Entity Details, Entity Relationships, and Node Color
- **Entity Image Display**: Entities with image properties (e.g., `cw:hasImage`) display the image inline below the entity name, loaded asynchronously with caching
- **Improved Layout**: Entity name displayed prominently (bold, 16pt), URI shown in readable prefixed form with steel-blue highlight, raw URI below in small text
- **Full-Height Scroll**: Single vertical scroll across all sections replaces the fragmented inner scroll areas
- **Right Padding**: Increased right-side margin for better visual balance
- **Removed Close Button**: Details panel no longer has a dismiss button, reducing clutter

### Search Improvements
- **Exact Match Priority**: Search results now rank exact label matches first, then prefix matches, then contains matches -- searching "Spider-Man Black Suit" returns the exact entity at the top
- **Property Name Search**: Properties without labels (identified only by URI local name) now appear in search results via a parallel URI local-name search
- **Local Index Enhancement**: The local search index now indexes properties (owl:ObjectProperty, etc.) by their URI local name when no label exists

### Visualization Fixes
- **Expansion Edge Drawing**: Fixed edge pruning that silently dropped edges connecting new nodes to already-displayed nodes during expansion -- subclass edges, literal edges, and hierarchy edges now draw correctly
- **Literal Node Labels**: Literal nodes now appear with labels and connecting edges immediately during expansion (previously required clicking to appear)
- **Overlap-Free Placement**: Rewrote expansion layout to reject overlapping positions at placement time using concentric ring search with bounding-rect collision detection, eliminating the post-hoc overlap resolver that scattered nodes unpredictably
- **Radial SubClass Layout**: SubClasses now arrange radially around their parent following all 11 layout rules, with inner rings preferred and empty sectors favored

## New in v2.9.2

### Visualization Pipeline Overhaul
- **Consolidated Rendering Pipeline**: All 7 rendering entry points (search, expand, query, Load Ontology, etc.) converge through a single unified pipeline ensuring consistent results regardless of data source
- **11 Production Layout Rules**: Comprehensive rule set enforced across all rendering paths — no overlaps, intelligent space usage, crossing-aware placement, color consistency, and property-as-edge filtering
- **Alternative Layout System**: New VDB-informed layout places hubs at center, bridges between hubs, and satellites radially — toggleable via "Alt Layout" button for A/B comparison with degree-based layout
- **Deterministic Color Assignment**: TopClass colors assigned at ontology load and persisted per-profile, ensuring stable colors across sessions and ontology updates

### Taxonomy Groups
- **Local Persistence**: Taxonomy group management moved to local file storage — no SPARQL round-trips needed for group organization
- **Import Integration**: Import tab reads taxonomy groups from local store for faster workflow

### Vocabulary Tab Polish
- **Permanent Scrollbars**: Non-floating scrollbars for predictable navigation
- **Improved Layout**: Better right-margin buffering and content spacing

### Quality Fixes
- **Duplicate Label Fix**: Corrected SPARQL language filter that caused duplicate `@en` labels in search results
- **Animation Reliability**: Expansion animation stays active until ALL nodes reach Drawn state; orphan nodes detected and scheduled correctly
- **VDB Property Validation**: SPARQL expansion consults VDB to distinguish properties from nodes (Rule 11)
- **Log Noise Reduction**: Missing-node warnings now logged once per edge instead of every frame

## New in v2.9.1

### Discover Paths Performance
- **SPARQL Rewrite**: Rewrote path discovery to use indexed triple patterns instead of unbound scans — orders of magnitude faster on large graphs
- **Safety Timeout**: 45-second timeout prevents runaway queries

### Show Query
- **Path Query Display**: View the generated SPARQL for any pathfinding result directly in the details panel

### Instance Node Coloring
- **Color Inheritance**: Instance nodes inherit color from their rdf:type via batch lookup
- **Visual Consistency**: Class nodes use their own URI as color key; instances inherit from parent class

### Details Panel UX
- **Collapsible Sections**: Panel sections use twisties for hierarchical organization
- **Literal Display**: Literal nodes show full text under "Value" heading
- **Color Palette Update**: Replaced Teal with Crimson for better visual distinction

## New in v2.9.0

### Pathfinding Data Source Routing
- **Ontology vs Instance Routing**: Instance operations route directly to SPARQL (bypassing VDB), while ontology operations use VDB — eliminates placeholder IDs
- **Fixed Search Positioning**: Search results now properly positioned on canvas

### Visualization Cleanup
- **Debug Overlay Removal**: Removed developer debug markers from visualization canvas
- **Type-Safe Coordinates**: New coordinate system module for vector operations

## New in v2.8.9

### Visualization Polish
- **Node Label Styling**: Larger, bolder node labels (28pt Inter-Bold) for better readability
- **Edge Label Enhancement**: Thicker edge labels (18pt Inter-SemiBold)
- **Leaf SubClass Management**: Hide/Show leaf subclasses per node with intelligent preservation of connected subclasses

### Query Tab Improvements
- **SELECT Result Display**: Fixed SELECT queries incorrectly displaying as CONSTRUCT triples
- **Column Ordering**: SELECT column ordering now matches query variable order

### Vocabulary Tab
- **Hero Image**: Professional hero image with left-fade mask
- **Wider Concept Panel**: Left column widened to 65% for better concept scheme display

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
