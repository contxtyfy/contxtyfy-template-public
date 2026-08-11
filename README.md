# Contxtyfy — your AI chief of staff, on Railway

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/contxtyfy-command-centre)

Live on the Railway marketplace as [**Contxtyfy Command Centre**](https://railway.com/template/contxtyfy-command-centre) (first published edition: v0.2.0, 2026-08-11).

Contxtyfy is a private, single-tenant **GTD command centre + knowledge graph**
run by supervised AI agents:

- **Capture** from Gmail, Calendar, Drive, Slack, Teams, WhatsApp and more —
  through your own [Composio](https://composio.dev) OAuth connections, with
  hard per-account boundaries.
- **Clarify** everything into an append-only GTD store: lanes, projects,
  contexts, priorities, due dates.
- **Graph** your people, organisations, meetings and commitments into a living
  Neo4j knowledge graph with an interactive visualization.
- **Prepare** you for meetings: agendas, talking points and open threads built
  from your own history and attached transcripts.
- **Delegate** tasks to agents — anything external (send, post, submit) pauses
  in a Decision Queue until you approve the exact preview. Nothing leaves your
  instance without you.

**Bring your own model**: OpenRouter, OpenAI, Ollama cloud, or any
OpenAI-compatible endpoint. Your keys, your usage, your data — everything
lives on your Railway volume.

## Quickstart

1. Click **Deploy on Railway** above (template `contxtyfy-command-centre`) — two services come up (Command Centre + Neo4j, each with a persistent volume, on a private network).
2. Open the Command Centre URL → you land on `/setup`. Enter the
   `CC_SETUP_TOKEN` shown in your Railway service variables.
3. Walk the wizard: password → accounts → model key → Composio OAuth →
   finish. ~10 minutes, all in the browser.

## Updating

Watch this repo / the in-app banner. To update, redeploy the Command Centre
service in Railway — the image's `stable` tag always points at the latest
release. See [CHANGELOG.md](CHANGELOG.md).

## Privacy

Your instance makes exactly the outbound calls you configure (your LLM
provider, your Composio connections, optional webhooks) plus one anonymous
daily `GET` of this repo's `versions.json` for the update banner
(disable with `CC_UPDATE_CHECK=0`). No telemetry, no phone-home.

## Support

Questions → the template's **Discuss this Template** queue on Railway, or
open an issue here.
