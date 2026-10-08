# comms-watch

A single-file dashboard for amateur radio situational awareness: who is on
the air near you, what nets are running, what the bands are doing, and what
the local infrastructure looks like.

It is one HTML file. Open it from disk, serve it from anywhere, or host it
behind a URL — there is no build step, no framework and no server component
in the page itself. Everything it needs that a browser cannot fetch comes
from a small relay you run yourself.

```
comms-watch.html     the whole dashboard
```

## Getting it running

1. **Open `comms-watch.html`.** Most of it works immediately — the feeds
   that are CORS-clean and need no credentials.
2. **Stand up the relay** if you want APRS positions, active nets, or
   repeater lookups. See
   [watch-relay](https://github.com/ashenroot/watch-relay). For a
   ham-only relay, set `GRIDWATCH_ENABLED=false` and
   `ISOALERTS_ENABLED=false` in its `relay.env`.
3. **Setup tab.** Enter the relay's base URL, your grid square, and any API
   keys you hold. Nothing is shipped pre-configured and nothing is required
   to be.

## Configuration, and why it is split in two

The Setup tab writes to two separate browser storage keys:

```
comms-watch/v1        grid square, relay URL, display preferences
comms-watch/keys/v1   API keys
```

They are split so that **"share my setup" and "hand over my credentials" can
never be the same action**. The shareable config export carries the first
bucket only. If you hand a club member your settings, you are not handing
them your keys.

Both live in that browser, on that machine. Nothing is sent anywhere except
to the services the page names.

## Keys

None ship with this project and none are required to get started. Where a
feed needs one, you hold your own:

- **aprs.fi** — optional, for extended station history. **Read their API
  terms yourself before using a key with any dashboard you redistribute.**
  This project makes no claim about what those terms permit; nobody here has
  verified them.
- Anything else the Setup tab asks for is documented on the tab itself.

If you fork this and publish it, check that you have not committed a key.
The `.gitignore` excludes exported config files for that reason.

## Being a good neighbour

Several upstreams are small, free, and run by people who owe you nothing.
The relay enforces the pacing — NetLogger's published one-call-per-minute
limit is a floor in code, and the repeater sweep runs serial with 12 seconds
between calls — but the dashboard's refresh interval is yours to set. Please
do not set it to something that makes you a problem for them.

## Licence

MIT. See [LICENSE](LICENSE).
