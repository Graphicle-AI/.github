<p align="center">
  <a href="https://github.com/graphicle-ai/graphicle">
    <img src="./assets/banner.png" width="100%" alt="Graphicle. Maps your code. Remembers your project. Code graph and memory for your coding agents, in one Rust program.">
  </a>
</p>

<p align="center">
  <a href="https://github.com/graphicle-ai/graphicle"><b>Repository</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/graphicle-ai/graphicle/blob/main/docs/quickstart.md"><b>Quick start</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/graphicle-ai/graphicle/tree/main/docs"><b>Docs</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/graphicle-ai/graphicle/blob/main/docs/benchmarks.md"><b>Benchmarks</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/graphicle-ai/graphicle/discussions"><b>Discussions</b></a>
</p>

**Graphicle maps your code and remembers your project, for you and your coding agents.**
It builds a graph of your repository (files, functions, classes, calls and imports)
and keeps your documents, decisions and past agent sessions word for word, so
answers come with their sources. One command, `graphicle`, runs it all, and
everything it stores stays on your machine.

```sh
brew install graphicle-ai/tap/graphicle
cd your-repo && graphicle setup
```

Setup builds the code graph, connects the coding agents it finds (Claude Code,
Codex, Cursor, VS Code and Claude Desktop) and lists every file it changes.
Then ask your agent to *"use graphicle to find where failed requests are
retried"*, or run `graphicle ask` in the terminal. It runs on macOS and Linux, with a
Windows preview;
[docs/install.md](https://github.com/graphicle-ai/graphicle/blob/main/docs/install.md)
has the install script, the release archives and building from source.

<table>
  <tr>
    <td width="50%" valign="top">
      <b>One map of your code</b><br>
      Search the graph, explain a symbol, trace the path between two symbols and
      see what depends on a change. The engine is a Rust port of Graphify.
    </td>
    <td width="50%" valign="top">
      <b>Memory with sources</b><br>
      Recall returns cited excerpts without calling a model. Agents can propose
      memories that quote their sources, and a person approves each one.
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <b>Built for agents</b><br>
      MCP for Claude Code, Codex, Cursor, VS Code, Claude Desktop and any other
      MCP client, with session capture for Claude Code and Codex.
    </td>
    <td width="50%" valign="top">
      <b>Local first</b><br>
      No account and no telemetry. Nothing goes to a model unless you set one up
      (<a href="https://github.com/graphicle-ai/graphicle/blob/main/docs/faq.md#does-graphicle-send-my-code-anywhere">every case</a>).
    </td>
  </tr>
</table>

**Also built in:** one MCP server, `graphicle mcp`, with the code-graph tools
under Graphify's tool names (such as `query_graph` and `shortest_path`) next to
the memory tools; reviewed memories tied to the functions they are about (a memory goes stale when its function changes; edits elsewhere in the file usually leave it current); and recall across the repositories
of a workspace (`graphicle context --workspace`).

### Measured in the open

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/graphicle-011-13-repos-dark.svg">
  <img src="./assets/graphicle-011-13-repos-light.svg" width="100%" alt="Two bar charts comparing Graphicle with Graphify 0.9.91 (Python) on 13 codebases. Left, speed: Graphify 0.9.91's time divided by Graphicle's for a code-only extract, highest first: kubernetes 22.7×, rails 7.0×, flask 6.9×, prometheus 6.6×, react 6.2×, scikit-learn 6.1×, pandas 5.8×, vscode 5.4×, ripgrep 5.3×, tokio 5.1×, redis 4.3×, next.js 4.0×, spring-boot 3.3×. A line on each bar spans its 3 operations (code-only extract, priming update and update with no change). Graphicle took less time in all 39 measurements and in every run, 3.0× to 22.7× less. Speed label: Graphicle's 0.1.1 memory engine (a pre-release build) against Graphify 0.9.91 on the same machine, 3 CPUs and 8 workers each, one session per program, 15 Oct 2026; median of 3 runs (1 for Kubernetes and VS Code). The graphs differ slightly: node counts within 4.7%, edge counts within 2.0%. Right, peak memory: Graphicle's peak divided by Graphify 0.9.91's peak for a code-only extract, lowest first: ripgrep 0.31×, flask 0.37×, pandas 0.38×, redis 0.39×, tokio 0.40×, scikit-learn 0.41×, prometheus 0.43×, react 0.50×, next.js 0.51×, vscode 0.52×, kubernetes 0.76×, rails 0.77×, spring-boot 0.94×. Lower in all 39 measurements, at 0.29× to 0.97× of Graphify's peak, on a pre-release memory build whose graphs differ from Graphify's; Graphicle's peak RSS or PSS, whichever is larger, against Graphify's peak PSS. A build of the merged 0.1.1 source stayed below in the 5 measurements rechecked. Speed and memory tables and method: docs/benchmarks.md.">
</picture>

- **[Speed](https://github.com/graphicle-ai/graphicle/blob/main/docs/benchmarks.md#speed-on-13-codebases-against-graphify-0991):**
  on 13 codebases, a pre-release build of Graphicle 0.1.1's engine took 3.0 to
  22.7 times less time than Graphify 0.9.91 in all 39 measurements (same
  machine, 3 CPUs each). The graphs differ slightly: node counts within 4.7%,
  edge counts within 2.0%.
- **[Memory](https://github.com/graphicle-ai/graphicle/blob/main/docs/benchmarks.md#peak-memory-against-graphify-0991):**
  a later pre-release build used less peak memory than Graphify 0.9.91 in all
  39 measurements, from 0.29 to 0.97 times its peak; its graphs differ from
  Graphify's too.
- **[Coding agents](https://github.com/graphicle-ai/graphicle/blob/main/docs/benchmarks.md#coding-agents-with-graphicle-graphify-or-neither):**
  with Claude Code and Opus 5.5, Graphicle ties plain Claude Code (grep) on
  accuracy in every test. On Graphify's own showcase corpus, the 0.1.1 agent
  defaults (a pre-release build) found 99.2% of the facts, against 94.7% for plain Claude Code (a
  tie) and 87.8% for Graphify 0.9.91, with fewer tokens than Graphify.
- **[Parity](https://github.com/graphicle-ai/graphicle/blob/main/docs/benchmarks.md#parity-with-graphify):**
  the code-graph engine is checked by running Graphify's own tests against it
  and comparing the results with the pinned Graphify release it follows.
  The upstream test files that are not run yet are
  [listed with the reason each is not run](https://github.com/graphicle-ai/graphicle/blob/main/docs/evidence/upstream-tests-not-run.md).
- **[Agent memory](https://github.com/graphicle-ai/graphicle/blob/main/docs/benchmarks.md#agent-memory-comparison-with-seven-memory-systems):**
  seven memory systems and a build of Graphicle answered the same questions on
  three development sets, with one open model as every system's reader and
  judge (a proxy evaluator).

Every result, with its labels and caveats, is in
[docs/benchmarks.md](https://github.com/graphicle-ai/graphicle/blob/main/docs/benchmarks.md), including the ties and the results that did not
favour Graphicle.

### Open source

Graphicle Core is free and open source under the
[Apache License 2.0](https://github.com/graphicle-ai/graphicle/blob/main/LICENSE).
Contributions are welcome with a DCO sign-off
([CONTRIBUTING.md](https://github.com/graphicle-ai/graphicle/blob/main/CONTRIBUTING.md)).
The code-graph engine is adapted from [Graphify](https://github.com/Graphify-Labs/graphify),
credited in [NOTICE](https://github.com/graphicle-ai/graphicle/blob/main/NOTICE).
A commercial edition for teams is in private preview:
[start a discussion](https://github.com/graphicle-ai/graphicle/discussions).

### Talk to us

- **Questions and ideas:** [Discussions](https://github.com/graphicle-ai/graphicle/discussions)
- **Chat:** [Discord](https://discord.com/invite/rWuU7cWU4E)
- **Bugs:** [open an issue](https://github.com/graphicle-ai/graphicle/issues/new/choose)
- **Security problems:** [report them privately](https://github.com/graphicle-ai/graphicle/security/advisories/new), never in a public issue
- **Everything else:** [vikramlex@karlexai.com](mailto:vikramlex@karlexai.com) · [@vikram_lex on X](https://x.com/vikram_lex) · [karlex.ai](https://www.karlex.ai)

<sub>Graphicle is made by <a href="https://www.karlex.ai"><img src="./assets/karlex-ai-logo.png" width="16" height="16" align="absmiddle" alt="KarLex AI logo"></a> <a href="https://www.karlex.ai">KarLex AI, Inc.</a> Other product names are trademarks of their owners; no affiliation or endorsement is implied.</sub>
