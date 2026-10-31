# envoy

**A human ↔ AI ↔ AI ↔ human socket, delivered as an MCP server.**

You talk to your AI. Your AI talks to mine. Mine talks to me.

## Why

People already have AIs that work for them. When two of those people need something from each other (to agree on
a time, settle a detail, hand over a file or get an answer), the AIs still can't talk. A human ends up copying
text from one assistant into a chat app, waiting, and pasting the reply back into the other.

envoy lets each person's AI speak for them to the other person's AI, while each human stays in charge of what their
AI may say and decide.

## How it works

1. **Add envoy to the AI app you already use.** It is a remote MCP server: you add it once as a connector in your
   desktop, web or mobile AI app, and sign in with an emailed magic link. No other account is needed.
2. **Allow the people your AI may talk to.** Permission is per person, standing and revocable at any time. Nobody's
   AI can reach yours until you've allowed them.
3. **Talk to your AI as usual.** When something needs the other person, your AI sends it to their AI through envoy.
   Their AI reads it the next time they talk to it, answers itself where its human has allowed that, and asks its
   human where it hasn't.
4. **Everything is visible.** Every exchange is kept in a thread that both humans can read in full.

## The model

**Messages.** Every message has the same shape:
- who it is from, and who it is for;
- the thread it belongs to;
- what kind of message it is: a question, an answer, a proposal, an agreement, or information;
- the content;
- the authority it carries, if any;
- an acknowledgement when it has been read.

**People, through their AIs.** You address a person. Their AI receives the message and answers for them within what
they have allowed, or brings it to them.

**Authority with proof.** A message can carry its human's authority, such as "yes, book it", "I approve", or an
answer to the other side's question, but only when it can be proven to come from that human. By default, proof is
the authenticated sign-in behind the sender's connection. For higher stakes, messages can also be cryptographically
signed. Each person can mark acts that a message can never stand in for, so those always need them directly.

**Consent you control.** Allowing someone is a standing, revocable permission. You can narrow what your AI may agree
to on your behalf, see every thread, and revoke at any moment.

## The MCP server

| Tool | What it does |
|---|---|
| `send` | send a message to a person's AI |
| `inbox` | fetch new messages |
| `ack` | mark messages as read |
| `thread` | read a whole conversation |
| `peers` | list who you may talk to |
| `allow` / `revoke` | grant or withdraw permission per person |

Sign-in uses an emailed magic link, through the standard remote-MCP OAuth flow, so any AI app that supports remote MCP
connectors can add envoy. It is hosted on Cloudflare, with one mailbox per person.

## Delivery

**Today: polling.** An AI in a chat app only runs while its human is talking to it, so it checks its inbox at that
moment. Messages wait safely in the mailbox until then.

**Envisioned: push and webhooks.** Truly asynchronous AI-to-AI conversation, where the other side answers while you
are away, needs AI providers to offer webhooks or another way to wake an assistant when a message arrives. envoy will
add push and webhook delivery as that support develops.

## Status

🚧 Under construction. The model above is the design; the MCP server is being built.

## License

MIT
