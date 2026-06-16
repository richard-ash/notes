---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/operations/2026-06-16-grafana-alerting.md
compiled_at: 2026-06-16
model: claude-opus-4-8[1m]
confidence: high
---

# Grafana Alerting with Slack notifications

A practical runbook for wiring Grafana alerts to a Slack channel. The flow has three independent pieces that compose: a **notification template** (how the message looks), a **contact point** (where it goes), and an **alert rule** (when it fires). Build them in that order — the rule references the contact point, and the contact point references the template.

## 1. Notification template

A template is a reusable Go-template snippet that formats the alert body. Define it once under **Alerting → Contact points → Add notification template group**, give it a name, paste the body, and save. The example below defines `metrics_template`:

```
{{ define "metrics_template" }}
{{ if and .CommonLabels.alertname (ne .CommonLabels.alertname "") -}}
*Alert:* {{ .CommonLabels.alertname }}
{{ end }}
*Status:* {{ if eq .Status "firing" }}🚨 *Firing* 🚨{{ else if eq .Status "resolved" }}✅ *Resolved* ✅{{ else }}ℹ️ *{{ .Status | title }}* ℹ️{{ end }}
{{ if and .CommonLabels.instance (ne .CommonLabels.instance "") -}}
*Instance:* {{ .CommonLabels.instance }}
{{ end }}
{{- if .CommonAnnotations.panel_url -}}
*Panel Link:* <{{ .CommonAnnotations.panel_url }}|Click here>
{{ end }}
{{ if and .CommonAnnotations.summary (ne .CommonAnnotations.summary "") -}}
*Summary:* {{ .CommonAnnotations.summary }}
{{ end }}
{{ if and .CommonAnnotations.description (ne .CommonAnnotations.description "") -}}
*Description:* {{ .CommonAnnotations.description }}
{{ end }}
{{ end }}
```

Mechanics worth noting:
- **`.CommonLabels` vs `.CommonAnnotations`** — labels (alertname, instance) identify and group the alert; annotations (summary, description, panel_url) carry human-readable context. The template guards each field with `if (ne … "")` so empty fields are simply skipped rather than rendering blank lines.
- **Slack markup, not Markdown** — `*bold*` and `<url|text>` are Slack's mrkdwn syntax. The `<{{ .CommonAnnotations.panel_url }}|Click here>` form produces a clickable link only because `panel_url` is supplied as a custom annotation on the rule (step 3).
- **`{{- … -}}`** — the hyphens trim surrounding whitespace so the rendered message stays compact.

## 2. Slack contact point

The transport is a Slack **incoming webhook**, not the Grafana Slack app:

1. At [api.slack.com/messaging/webhooks](https://api.slack.com/messaging/webhooks), create an app **From scratch**, then **Add New Webhook**, pick the target channel, **Allow**, and copy the webhook URL.
2. In Grafana, **Alerting → Contact points → Create new contact**. Paste the webhook URL into the **Webhook URL** field.
3. Under **Optional Slack settings**, set a custom **title** — the message header / Slack notification line:
   ```
   [{{ .Status | toUpper }}:{{ len .Alerts }}] {{ .CommonLabels.alertname }}
   ```
   `len .Alerts` is the count of alerts batched into this notification (see grouping below), so a title like `[FIRING:3] HighCPU` tells you the firing/resolved state and how many instances are involved at a glance.
4. Set the **text body** to the `metrics_template` from the drop-down, save, then **Test** to confirm a templated message lands in the channel.

## 3. Alert rule

On the panel you want to watch, enter **Edit mode → Alerts tab → new alert**:

1. **Name** the rule clearly.
2. **Query & condition** — pick the metric and any label filters (e.g. by instance).
3. **Folder & labels** — folders organize rules; labels are what the contact point and template read.
4. **Evaluation behavior** — create an evaluation group and set the period. The guide uses `30s` but flags it explicitly as a *learning* value: production cadence should match how fast the monitored signal actually moves, since over-frequent evaluation adds query load and noise.
5. **Notifications** — select the contact point. Under **Muting, grouping, and timings → Override timings**:
   - **Group interval** — how long Grafana waits after the first notification before sending a *new* notification for the same group (batches related alerts).
   - **Repeat interval** — how long before re-sending a notification for an alert that is *still* firing (controls reminder frequency).

   Both are set to `30s` in the example — again a test-friendly value that would be far too chatty in production.
6. **Notification message** — to make the template's panel link work, add a custom annotation with key `panel_url` and value = the panel's share link (**Share → Copy link**). `summary` and `description` annotations are optional and may be left empty.

## Why the three-part split matters

The separation is deliberate: one template can serve many contact points, one contact point many rules, and one rule routes by labels. This is the same fan-in/fan-out shape Prometheus Alertmanager uses (Grafana's alerting is built on a vendored Alertmanager), so the template syntax, label/annotation distinction, and grouping/repeat semantics all transfer to a standalone Prometheus + Alertmanager stack.

## Sources
- "Grafana Alerting." (n.d.) <https://www.notion.so/Grafana-Alerting-259e8c61e93480fa935ec2ab5d1da2de> — [[2026-06-16-grafana-alerting|local copy]]
