# Conversion Tracking MCP Starter Kit — Verify Ad Tracking with AI

[![MCP Compatible](https://img.shields.io/badge/MCP-compatible-blue)](https://modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Platform: Conversion Tracking](https://img.shields.io/badge/Platform-Conversion%20Tracking-EF4444)](https://syntermedia.ai)

**Never launch a campaign with broken tracking again.** Open this repo in Amp, Cursor, or VS Code and verify your conversion pixels, GTM tags, and tracking setup with AI — catch issues before they cost you money.

---

## Why Conversion Tracking Verification?

Here's a stat that should terrify every advertiser: **38% of ad accounts have at least one misconfigured conversion action.** Broken tracking means your Smart Bidding can't optimize, your ROAS numbers are wrong, and you're making budget decisions on bad data.

The worst part? You won't know until weeks later when your campaigns underperform and you can't figure out why. A mistyped Pixel ID, a GTM tag firing on the wrong trigger, a conversion action counting page views instead of purchases — these silent bugs burn thousands in wasted spend.

An AI agent runs pre-flight checks before every campaign launch. It verifies pixels fire correctly, conversion actions are configured right, and your data pipeline is working end-to-end.

**Best for:** Anyone launching new campaigns, switching tracking setups, debugging attribution issues, or ensuring existing tracking is still working after website changes.

---

## Quick Start (30 Seconds)

### Amp / Cursor / VS Code (Copilot)

1. **Get a free API key** at [syntermedia.ai/developer](https://syntermedia.ai/developer)
2. **Set the key:**
   ```bash
   export SYNTER_API_KEY=syn_your_key_here
   ```
3. **Open this repo** in your editor
4. **Start chatting** — MCP tools are pre-configured in `.mcp.json`

### Claude Desktop

Copy `claude_desktop_config.json` to your Claude config directory and replace the API key:

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

---

## What You Can Do

| Capability | Example |
|-----------|---------|
| **Pre-Flight Check** | "Verify all tracking before I launch my new Google Ads campaign" |
| **Pixel Verification** | "Is my Meta Pixel firing on all pages?" |
| **GTM Tag Audit** | "Check if my Google Ads conversion tag is configured correctly" |
| **Conversion Action Check** | "Do I have Google Ads conversion actions set up for purchases?" |
| **Cross-Platform Audit** | "Verify tracking for Google, Meta, LinkedIn, and TikTok" |
| **Website Scan** | "Scan my website for installed tracking pixels" |
| **Data Layer Check** | "Is my ecommerce data layer pushing the right events?" |
| **Attribution Debug** | "Why is Google Ads showing 50 conversions but GA4 shows only 30?" |
| **GTM Publishing** | "Check for unpublished GTM changes and publish them" |
| **Server-Side Tracking** | "Is my Meta Conversions API (CAPI) configured and sending events?" |

---

## Example Conversations

### 1. Pre-Launch Tracking Checklist

> **You:** I'm about to launch a new Google Ads campaign for our ecommerce store. Run a tracking check.
>
> **Agent:** Running pre-flight tracking verification for your website...
>
> **Pre-Flight Checklist:**
>
> | Check | Status | Details |
> |---|---|---|
> | Google Tag (gtag.js) installed | ✅ Pass | Found on all pages |
> | Google Ads conversion action | ✅ Pass | "Purchase" action exists, status: Active |
> | Conversion value tracking | ❌ **FAIL** | Conversion value is set to $1.00 for all purchases instead of actual order amount |
> | Conversion Linker | ✅ Pass | GTM Conversion Linker tag firing on all pages |
> | Enhanced conversions | ⚠️ Warning | Not configured — losing ~15% of conversions due to cookie restrictions |
> | GTM unpublished changes | ❌ **FAIL** | 3 unpublished changes in your GTM container |
> | Meta Pixel | ✅ Pass | Pixel ID 1234567890 firing PageView on all pages |
> | Meta Purchase event | ✅ Pass | Purchase event firing on /thank-you page |
> | Meta CAPI | ⚠️ Warning | Not configured — relying on browser pixel only |
>
> **Critical issues (must fix before launch):**
>
> 1. **Conversion value is wrong.** Every purchase reports $1.00 instead of the actual order amount. Google's Smart Bidding is optimizing for quantity, not revenue. Fix: Update your conversion tag to pull the `transaction_total` from the data layer.
>
> 2. **GTM has unpublished changes.** Your container has 3 pending changes that aren't live. If any of these are conversion-related, they're not firing. Fix: Review and publish.
>
> **Recommended improvements:**
> - Enable Enhanced Conversions for Google Ads (recovers 10-15% of lost conversions)
> - Set up Meta Conversions API alongside your Pixel (recovers ~30% of iOS conversions)

### 2. Diagnosing Attribution Discrepancies

> **You:** Google Ads shows 50 conversions but GA4 shows only 30 for the same period. Why?
>
> **Agent:** Attribution discrepancies between Google Ads and GA4 are common. Let me diagnose the specific causes:
>
> **Discrepancy: Google Ads (50) vs GA4 (30) = 20 missing conversions**
>
> | Cause | Estimated Impact | Explanation |
> |---|---|---|
> | Attribution window difference | ~8 conversions | Google Ads uses 30-day click attribution by default. GA4 uses last-click with a shorter window. A user who clicked an ad 25 days ago and converted today counts in Google Ads but may not in GA4. |
> | Cross-device conversions | ~6 conversions | Google Ads tracks cross-device (clicked on phone, converted on desktop). GA4 under-reports these without Google Signals enabled. |
> | View-through conversions | ~4 conversions | Google Ads counts conversions where someone SAW your ad but didn't click, then converted later. GA4 doesn't track view-through by default. |
> | Tag timing difference | ~2 conversions | If the GA4 tag fires 500ms after the Google Ads tag, and the user closes the page during that window, GA4 misses the event. |
>
> **Your action items:**
> 1. Enable Google Signals in GA4 (Admin → Data Settings → Data Collection) to improve cross-device tracking
> 2. Check your Google Ads attribution settings — consider switching to data-driven attribution
> 3. Align conversion counting: Google Ads may count "one per click" vs "every conversion" — check which you're using
> 4. Consider disabling view-through conversions in Google Ads if they inflate numbers unrealistically
>
> **The truth is between the two numbers.** Real conversions are probably ~42 (GA4 undercounts, Google Ads overcounts).

### 3. Multi-Platform Pixel Verification

> **You:** I just redesigned my website. Verify all my tracking pixels still work.
>
> **Agent:** Website redesigns are the #1 cause of broken tracking. Let me scan your site...
>
> **Scanning https://yoursite.com...**
>
> | Platform | Pixel/Tag | Status | Firing |
> |---|---|---|---|
> | Google Analytics (GA4) | G-XXXXXXXXXX | ✅ Working | All pages |
> | Google Ads | AW-XXXXXXXXX | ✅ Working | All pages |
> | Google Ads (Purchase) | AW-XXXXXXX/label | ❌ **BROKEN** | Not firing on new /checkout/success page |
> | Meta Pixel (Base) | 1234567890 | ✅ Working | All pages |
> | Meta Pixel (Purchase) | 1234567890 | ❌ **BROKEN** | Not firing — /thank-you page no longer exists |
> | LinkedIn Insight Tag | 4567890 | ✅ Working | All pages |
> | Reddit Pixel | a2_xxxxx | ⚠️ Warning | Firing but `rdt_cid` cookie not captured |
> | TikTok Pixel | XXXXXX | ❌ **BROKEN** | Script removed during redesign |
>
> **Critical issues found: 3**
>
> 1. **Google Ads Purchase conversion:** Your old confirmation page was `/thank-you`. After redesign, it's `/checkout/success`. The GTM trigger still points to the old URL.
>    - Fix: Update GTM trigger from `/thank-you` to `/checkout/success`
>
> 2. **Meta Purchase event:** Same URL change broke this. The Meta event tag was hardcoded to fire on `/thank-you`.
>    - Fix: Update trigger URL pattern
>
> 3. **TikTok Pixel completely missing:** The redesign removed the TikTok Pixel script tag. It wasn't in GTM — it was hardcoded in the old template.
>    - Fix: Add TikTok Pixel to GTM (better than hardcoding) so it survives future redesigns
>
> **Estimated revenue impact of these bugs:** If these went undetected for 1 week with $5,000/week ad spend, you'd lose $5,000 in Smart Bidding optimization (campaigns would revert to less efficient bidding without conversion data).

### 4. Server-Side Tracking Health Check

> **You:** I set up Meta CAPI last month. Is it actually working?
>
> **Agent:** Let me verify your Meta Conversions API setup...
>
> **Meta CAPI Health Check:**
>
> | Metric | Value | Status |
> |---|---|---|
> | CAPI events (last 7 days) | 1,247 | ✅ Sending events |
> | Browser Pixel events (last 7 days) | 1,891 | ✅ Also sending |
> | Deduplication rate | 78% | ✅ Good (both fire, Meta removes duplicates) |
> | Event match quality score | 6.2/10 | ⚠️ Below optimal (7+ recommended) |
> | Events with email | 92% | ✅ Good |
> | Events with phone | 31% | ⚠️ Low — add phone number capture |
> | Events with IP address | 98% | ✅ Good |
> | Events with user agent | 98% | ✅ Good |
>
> **Issues:**
> 1. **Event match quality is 6.2/10.** Meta recommends 7+. Your CAPI events include email and IP but are missing phone number and `fbp` (Facebook browser cookie) for many events.
>    - Fix: Capture `fbp` cookie from the browser and include it in CAPI requests. This alone should push you to 7.5+.
>
> 2. **Deduplication is working but imperfect.** 22% of events aren't being deduplicated, which means some conversions are double-counted. Check that your `event_id` matches between browser Pixel and CAPI.
>
> **Bottom line:** CAPI is working and recovering ~34% of conversions that the browser Pixel misses (due to iOS restrictions and ad blockers). But the match quality could be higher.

### 5. Data Layer Verification for Ecommerce

> **You:** My ecommerce tracking seems inconsistent. Some purchases fire, some don't.
>
> **Agent:** Inconsistent ecommerce tracking usually means a data layer issue. Let me check...
>
> **Data layer analysis across 5 page types:**
>
> | Page | Expected Event | Data Layer Push | Status |
> |---|---|---|---|
> | Product page | `view_item` | ✅ Fires with product_id, name, price | Working |
> | Cart page | `view_cart` | ❌ Not implemented | Missing |
> | Checkout step 1 | `begin_checkout` | ✅ Fires with item array | Working |
> | Checkout step 2 | `add_payment_info` | ❌ Not implemented | Missing |
> | Confirmation | `purchase` | ⚠️ Fires but missing `transaction_id` | Partial |
>
> **Why some purchases aren't tracked:**
>
> The `purchase` event fires on your confirmation page, BUT:
> 1. **Missing `transaction_id`:** Without this, GA4 can't deduplicate. If a user refreshes the confirmation page, the same purchase fires twice. And if the page loads slowly, the event might fire before the data layer is ready — sending an empty payload.
>
> 2. **Race condition:** Your data layer push happens in a `DOMContentLoaded` callback, but your GTM container loads asynchronously. On slower connections, GTM fires the purchase tag before the data layer is populated.
>
> **Fix:**
> ```javascript
> // Instead of DOMContentLoaded, push to dataLayer immediately
> // and let GTM's trigger handle the timing
> window.dataLayer = window.dataLayer || [];
> window.dataLayer.push({
>   event: 'purchase',
>   transaction_id: 'TXN-12345',
>   value: 89.99,
>   currency: 'USD',
>   items: [...]
> });
> ```
>
> This ensures the data is in the data layer before GTM even loads.

---

## Conversion Tracking Tips

1. **Always verify tracking BEFORE launching campaigns.** Run a pre-flight check every time. Broken tracking + Smart Bidding = wasted money.
2. **No tracking = no smart bidding.** Without conversions, Google and Meta can't optimize. Use Maximize Clicks until tracking is verified, then switch to Target CPA or Maximize Conversions.
3. **Website redesigns break tracking 90% of the time.** After any site change, run a full pixel scan. URL changes, template changes, and JavaScript refactors all break tags.
4. **Server-side tracking (CAPI) recovers 25-35% of lost conversions.** iOS privacy changes and ad blockers prevent browser pixels from firing. CAPI bypasses these limitations.
5. **Google Ads and GA4 will never match exactly.** Different attribution models, different counting methods, different cross-device capabilities. The truth is between the two.
6. **Test conversion tags with real transactions.** Don't just check if the tag fires — verify the conversion value, currency, and transaction ID are correct.
7. **GTM unpublished changes are a silent killer.** You configure everything perfectly, forget to publish, and wonder why nothing works. Always publish after changes.

---

## FAQ

### Is there an MCP for conversion tracking verification?
Yes — this repo. It pre-configures the Synter MCP server for tracking verification across Google, Meta, LinkedIn, TikTok, Reddit, and more.

### Can AI check if my Meta Pixel is working?
Yes. The agent verifies your Meta Pixel is installed, firing on the correct pages, and sending the right events (PageView, Purchase, AddToCart, etc.).

### Can the agent fix broken tracking?
The agent diagnoses issues and provides specific fix instructions. For GTM-based fixes (updating triggers, creating tags), it can apply changes directly through the GTM API.

### How often should I verify tracking?
Before every campaign launch, after every website change, and monthly as a health check. Tracking breaks silently — regular verification prevents data loss.

### Does this check server-side tracking (CAPI)?
Yes. The agent can verify Meta CAPI, Google Enhanced Conversions, LinkedIn CAPI, Reddit CAPI, and TikTok Events API configurations.

---

## Related Repos

- [google-tag-manager-agent](https://github.com/Synter-Media-AI/google-tag-manager-agent) — Fix GTM tags
- [google-analytics-agent](https://github.com/Synter-Media-AI/google-analytics-agent) — GA4 event configuration
- [google-ads-agent](https://github.com/Synter-Media-AI/google-ads-agent) — Conversion action setup
- [meta-ads-agent](https://github.com/Synter-Media-AI/meta-ads-agent) — Meta Pixel & CAPI
- [tiktok-ads-agent](https://github.com/Synter-Media-AI/tiktok-ads-agent) — TikTok Pixel setup
- [cross-platform-ads-agent](https://github.com/Synter-Media-AI/cross-platform-ads-agent) — Multi-platform verification

---

## License

MIT — see [LICENSE](LICENSE) for details.

Built by [Synter](https://syntermedia.ai) · [Get API Key](https://syntermedia.ai/developer) · [Documentation](https://syntermedia.ai/docs)
