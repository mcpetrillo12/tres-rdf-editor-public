# Getting Started with TRèS

Welcome to TRèS (Triple Store RDF Editor Suite) - your platform-independent tool for managing RDF data across enterprise triple stores.

---

## Quick Start (5 Minutes)

### Step 1: Create Your First Database Connection

1. Click the **Database** tab in the main menu
2. Click **"+ New Profile"**
3. Fill in the connection details:
   - **Name:** A friendly name (e.g., "My Stardog Dev")
   - **Platform:** Select your database type (Stardog, GraphDB, RDFox, Fuseki, AllegroGraph)
   - **Endpoint URL:** Your database SPARQL endpoint
   - **Username/Password:** Your credentials (stored securely)
4. Click **"Test Connection"** to verify
5. Click **"Save"** to store the profile

### Step 2: Connect and Explore

1. Select your profile from the dropdown in the header
2. Click **"Connect"**
3. Once connected, the status indicator turns green
4. Your available named graphs appear in the graph selector

### Step 3: Run Your First Query

1. Click the **Query** tab
2. You'll see a SPARQL editor with syntax highlighting
3. Try a simple query:
   ```sparql
   SELECT ?s ?p ?o
   WHERE { ?s ?p ?o }
   LIMIT 10
   ```
4. Click **"Execute"** or press `Ctrl+Enter` / `Cmd+Enter`
5. Results appear in the table below

---

## Main Features

### Query Tab
Write and execute SPARQL queries with:
- Syntax highlighting
- Query history (arrow keys)
- Snippet library for common patterns
- Results export (CSV, JSON)

**Modes:**
- **Query:** Read-only SELECT/CONSTRUCT queries
- **Browse:** Navigate data by class and instance
- **Update:** INSERT/DELETE operations (careful!)

### Visualization Tab
Explore your ontology visually:
1. Click **"Load Ontology"** to import from a graph
2. Click any node to see its connections
3. Use **"Expand"** to show related entities
4. **"Find Path"** shows the shortest path between two selected nodes
5. Drag nodes to arrange the layout

**Tips:**
- Hold `Ctrl/Cmd` and click to select multiple nodes
- Right-click for context menu options
- Use the zoom controls in the lower right

### Database Manager Tab
Manage your data:
- **Import:** Load Turtle, N-Triples, or RDF/XML files
- **Export:** Save graph data to various formats
- **Graph Management:** Create, clear, or replace named graphs
- **Taxonomy Groups:** Assign imported ConceptSchemes to a group (existing or new)
- **Inline markers:** Add `###G:[Group Name]###` in TTL files to auto-create groups

### Vocabulary Tab
For SKOS vocabularies:
- Browse concept hierarchies grouped by Taxonomy Groups
- Export documentation (HTML, Markdown, Word, CSV)
- Validate vocabulary structure

---

## Essential Tips

### Keyboard Shortcuts
| Action | macOS | Windows/Linux |
|--------|-------|---------------|
| Execute Query | `Cmd+Enter` | `Ctrl+Enter` |
| New Query Tab | `Cmd+T` | `Ctrl+T` |
| Save | `Cmd+S` | `Ctrl+S` |

### Standard Prefixes
TRèS automatically recognizes these common prefixes without needing `@prefix` declarations:
- `rdf:`, `rdfs:`, `owl:`, `xsd:`
- `skos:`, `dc:`, `dcterms:`, `foaf:`

### Custom Namespaces
Add your own prefixes in **Preferences → Namespaces**. They'll be recognized across all features.

### Language Preferences
Set your preferred language in **Preferences → Language & Display**. TRèS will prioritize labels in your language when displaying multilingual data.

---

## AI Features (Optional)

If you have [Ollama](https://ollama.ai) installed, TRèS can provide:
- **Ontology Summarization:** Natural language description of your data model
- **Quality Analysis:** Scoring and recommendations for your ontology

To enable:
1. Install Ollama
2. Run `ollama pull gemma3`
3. Start `ollama serve`
4. TRèS will detect it automatically


## Getting Help

- **Hamburger Menu → Documentation** - Opens bundled documentation
- **GitHub Issues** - Report bugs or request features
- **Contact:** info@taurusystems.com

---

*TRèS - Platform-Independent RDF Data Management for the Modern Semantic Web*
