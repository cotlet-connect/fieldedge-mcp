# How to connect FieldEdge to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your FieldEdge account.** There is no official FieldEdge app in the ChatGPT or Claude directories. Cotlet.dev connects your own signed-in FieldEdge account to any AI agent, so you can ask in plain words and the AI books jobs, dispatches techs and sends invoices for you.

## What you can ask

> Book a furnace tune-up for Mark Rivera at 42 Oak Street on Thursday at 9 am and assign it to Luis.

> What does tomorrow's dispatch board look like per technician? Flag anyone with more than 6 jobs.

> Move all of Dave's Friday jobs to Carlos and text the customers the new arrival window.

> Create invoices for every job completed yesterday and email them to the customers.

> Which invoices over $500 are still unpaid after 30 days? List them with the customer phone number.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its FieldEdge tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"fieldedge":{"command":"uvx","args":["fieldedge-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t fieldedge-mcp .
docker run -i --rm -e COTLET_API_KEY fieldedge-mcp
```

Tools: `fieldedge_guide`, `fieldedge_status`, `fieldedge_open`, `fieldedge_read`, `fieldedge_click`, `fieldedge_type`, `fieldedge_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install fieldedge-mcp        # or run it once: uvx fieldedge-mcp connect
fieldedge-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 fieldedge_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 fieldedge_agent.py status    # is FieldEdge ready in your Cotlet.dev account
python3 fieldedge_agent.py guide     # FieldEdge screens and sign-in link
python3 fieldedge_agent.py read      # open FieldEdge, read the page, close the browser
python3 fieldedge_agent.py tools     # list Cotlet.dev tools
python3 fieldedge_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from FieldEdge users

**Does FieldEdge have an API for developers?**

FieldEdge has an API, but only on request: you ask for access through FieldEdge's onboarding form and wait for credentials. Cotlet.dev works in your own signed-in FieldEdge account instead, so your AI agent can book work orders, dispatch technicians and send invoices without that request.

**How do I connect FieldEdge to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to FieldEdge once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no FieldEdge API key.

**Is there a way to use Claude with FieldEdge?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own FieldEdge account.

**Is there a FieldEdge MCP server?**

FieldEdge has no official MCP server and no official app in ChatGPT or Claude (checked November 2026). Cotlet.dev is a hosted FieldEdge MCP server that works in your own account, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [FieldEdge on Cotlet.dev](https://cotlet.dev/integrations/fieldedge-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=fieldedge&utm_content=find)
- [PyPI package fieldedge-mcp](https://pypi.org/project/fieldedge-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-fieldedge-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [AroFlo MCP](https://github.com/cotlet-connect/aroflo-mcp)
- [Simpro MCP](https://github.com/cotlet-connect/simpro-mcp)
- [Workiz MCP](https://github.com/cotlet-connect/workiz-mcp)
- [Kickserv MCP](https://github.com/cotlet-connect/kickserv-mcp)
- [Service Autopilot MCP](https://github.com/cotlet-connect/service-autopilot-mcp)
- [Boulevard MCP](https://github.com/cotlet-connect/boulevard-mcp)
- [Mindbody MCP](https://github.com/cotlet-connect/mindbody-mcp)
- [Meevo MCP](https://github.com/cotlet-connect/meevo-mcp)
- [DaySmart MCP](https://github.com/cotlet-connect/daysmart-mcp)
- [Acuity Scheduling MCP](https://github.com/cotlet-connect/acuity-scheduling-mcp)
- [Jane App MCP](https://github.com/cotlet-connect/jane-app-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/fieldedge-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=fieldedge

Start free: https://cotlet.dev/signup?app=fieldedge&utm_source=github&utm_medium=readme&utm_campaign=fieldedge
