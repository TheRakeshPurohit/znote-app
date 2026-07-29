# MCP · Stripe — the MRR report in a note

**Use case**: indie hacker / SaaS — monthly sales, MRR, recent customers,
unpaid invoices. Your revenue reporting lives in a note you re-run.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "stripe": {
      "command": "npx",
      "args": ["-y", "@stripe/mcp", "--tools=all"],
      "env": { "STRIPE_SECRET_KEY": "rk_live_your_restricted_key" }
    }
  }
}
```

> **Official** Stripe server. Create a **restricted key** (Developers → API
> keys → Restricted) read-only on Charges / Customers / Subscriptions /
> Invoices — never the full secret key.

**Exposed tools**: `list_customers`, `list_charges`, `list_subscriptions`,
`list_invoices`, `list_products`, `retrieve_balance`, `search_documentation`…

## Examples

### Monthly sales report

```ai tools=stripe
This month's report: total collected, number of sales, average basket.
Compare with last month and give the trend in one sentence.
```

### Subscription health

```ai tools=stripe
List the subscriptions cancelled in the last 30 days with their
lifetime. Is there a pattern (lifespan, plan)?
```

### Dunning

```ai tools=stripe.list_invoices
Unpaid invoices older than 15 days: customer, amount, date. Draft a
polite reminder email template I can reuse.
```

## Tips

- Re-run the same block at the start of each month: the note becomes your
  report history, versioned with the vault.
- The read-only restricted key makes the whole thing safe: the model can't
  refund or charge anything.
