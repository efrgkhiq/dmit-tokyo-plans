# Japan VPS Hosting: DMIT Tokyo Plans Compared by Route, Traffic Policy and Price, From $36.9/Year

Most people searching for Japan VPS hosting are not really shopping for CPU cores. They want a Tokyo IP that answers quickly for users in Japan and East Asia, usually without the filing overhead that comes with a mainland Chinese host. Then they open a provider's pricing page, see eight plan names that differ only in numbers, and pick whatever looks mid-range.

That approach works fine on a provider with one network profile. It falls apart on DMIT, where the Tokyo location sells the same chassis under three different route profiles, and the cheapest plan on the "premium" line costs several times what the entry plan on the international line costs. Same datacenter city. Very different packets.

So here is the actual decision tree, plus the current Tokyo plan list and what each route is good for.

## What a Japan VPS is really for

Five recurring reasons people put a server in Tokyo:

- **Japanese IP for Japanese services.** Streaming, manga, banking portals, and game account regions all care about where the exit IP is registered.
- **Latency to East Asia.** Tokyo to Shanghai is roughly 30 ms on a good route and Tokyo to US West is around 100–120 ms. If your users are in Asia, US West hosting adds 100 ms-plus round trips on every request. That is the difference between a snappy site and a slow one.
- **No ICP filing.** A Japan-hosted site reachable from China does not need a mainland registration, which is why cross-border stores, landing pages and API endpoints cluster in Tokyo and Hong Kong.
- **Data residency.** Japan's APPI framework pushes a lot of local businesses to keep data physically in-country, and many Japanese enterprises treat that as a hard requirement rather than a preference.
- **A neutral endpoint.** Backup nodes, remote development boxes, relay points for teams spread across Asia.

None of those use cases are decided by core count. They are decided by the return path your traffic takes, and that is what you are actually paying for.

## Why the route matters more than the spec sheet

From a Tokyo machine, a packet bound for a mainland Chinese user can travel on several very different kinds of path:

- **CN2 GIA** is China Telecom's premium backbone. Lower packet loss, more consistent during the evening peak when ordinary transit links congest.
- **AS9929 / AS10099** are China Unicom's premium ranges, and **CMI / CMIN2** is China Mobile's international arm. Together with CN2 GIA these make up what Chinese hosting communities call "three-network optimization" (三网优化).
- **Plain international transit** means carriers like NTT, Telia, Lumen, HE, Cogent. Great for Japan-domestic and general Asian traffic, unpredictable for mainland China, and sometimes routed the long way around.

Two "1 GB RAM, $20/month" Tokyo VPSes can differ by 200 ms of peak-hour latency and double-digit packet loss, purely on this.

## DMIT and its Tokyo product lines

DMIT is a US-registered VPS provider running three locations: Los Angeles, Hong Kong and Tokyo. It built its reputation on premium China-optimized routes rather than on being cheap, and its Hong Kong and Tokyo CN2 GIA plans sit at the expensive end of the market for that reason.

Tokyo runs on the AS3 platform: AMD EPYC 7003 (Milan) CPUs, NVMe SSD, KVM virtualization, one IPv4 address plus a /64 IPv6 block, in Equinix TY8. Three network profiles are sold there:

- **Premium (TYO.AS3.Pro)** — three-network CN2 GIA optimization. The flagship line.
- **Tier 1 (TYO.AS3.T1)** — international routing only. No mainland China optimization.
- **Lite (PVM.TYO.Lite)** — a newer, cheaper international line launched in open beta. Big traffic allowances on a 1 Gbps port, no China optimization.

A fourth, **Eyeball (TYO.AS3.EB)**, historically sat between Pro and T1 with a CMI-optimized return path from $25.9/month. Recent Tokyo restock listings no longer include it, and at least one write-up describes the line as withdrawn. If CMI routing is specifically what you need, confirm it still exists before building a plan around it.

## TYO.AS3.Pro: the CN2 GIA line

This is the one to buy if mainland Chinese users are in your audience. The return path runs CN2 GIA, with AS9929/AS10099 and CMI alongside it, so all three major Chinese carriers get a decent lane. Bandwidth is 1 Gbps across the board, and traffic overage **suspends the service** rather than throttling it, which is worth reading twice before you order.

Test IP: `154.12.190.32`. Looking glass: `lg.dmit.sh`.

| Plan | CPU | RAM | SSD | Traffic / port | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| Pro.TINY | 1 core | 1 GB | 20 GB | 500 GB @ 1 Gbps | $21.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Pro.STARTER | 1 core | 2 GB | 40 GB | 1 TB @ 1 Gbps | $45.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Pro.MINI | 2 cores | 4 GB | 60 GB | 2 TB @ 1 Gbps | $89.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Pro.MICRO | 4 cores | 4 GB | 80 GB | 4 TB @ 1 Gbps | $189.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Pro.MEDIUM | 4 cores | 8 GB | 160 GB | 6 TB @ 1 Gbps | $320.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Pro.LARGE | 8 cores | 16 GB | 320 GB | 8 TB @ 1 Gbps | $429.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Pro.GIANT | 8 cores | 24 GB | 640 GB | 15 TB @ 1 Gbps | $829.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |

Two practical notes on this table.

First, these figures come from DMIT's Tokyo restock listings, and DMIT has repriced the Pro line before (older community posts still quote STARTER at $39.90 and MINI at $79.90). Tokyo stock arrives in small batches, usually recycled IPs, and the vendor has said large restocks are not planned. Treat the order page as the source of truth.

Second, TINY at $21.90/month buys 500 GB of traffic and no upgrade path if you blow through it mid-month. A site with images, or anything doing backups over the wire, will find 500 GB tight.

## TYO.AS3.T1: international routing on a budget

Tier 1 skips the China optimization entirely. Traffic goes out over international transit, and the overage policy is the opposite of Pro: instead of getting cut off, you get **throttled to a fixed speed with unlimited traffic**. WEE drops to 50 Mbps, TINY through MINI to 100 Mbps, and the bigger plans keep 200 Mbps to 1 Gbps.

Test IP: `154.31.112.5`.

| Plan | CPU | RAM | SSD | Traffic / port | After overage | Price | Order |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T1.WEE | 1 core | 1 GB | 20 GB | 1 TB @ 4 Gbps | 50 Mbps, unlimited | $36.90/yr | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| T1.TINY | 1 core | 2 GB | 40 GB | 2 TB @ 4 Gbps | 100 Mbps, unlimited | $6.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| T1.STARTER | 2 cores | 2 GB | 40 GB | 4 TB @ 10 Gbps | 100 Mbps, unlimited | $12.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| T1.MINI | 2 cores | 4 GB | 80 GB | 8 TB @ 10 Gbps | 100 Mbps, unlimited | $21.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| T1.MICRO | 4 cores | 4 GB | 80 GB | 16 TB @ 10 Gbps | 200 Mbps, unlimited | $32.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| T1.MEDIUM | 4 cores | 8 GB | 160 GB | 32 TB @ 10 Gbps | 200 Mbps, unlimited | $49.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| T1.LARGE | 8 cores | 16 GB | 320 GB | 64 TB @ 10 Gbps | 500 Mbps, unlimited | $99.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| T1.GIANT | 8 cores | 24 GB | 640 GB | 128 TB @ 10 Gbps | 1 Gbps, unlimited | $199.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |

T1.WEE at $36.90/year is the cheapest way into a Tokyo IP in this lineup. For a backup node, a monitoring box, a small site aimed at Japanese or Southeast Asian visitors, that is a genuinely low entry cost. What you give up is mainland China performance, and the routing is not guaranteed to stay pretty — community traceroutes show T1 sometimes taking the long way through the US on some carriers.

If your users are in mainland China, do not buy T1 and hope. That is the single most common mistake with this lineup.

## TYO Lite: the new budget line

Lite is the newest Tokyo option and still labelled open beta, which DMIT explicitly says comes without uptime guarantees. The trade is straightforward: bigger traffic allowances at a lower price, on an international mix of NTT, Telia, HE and Equinix-adjacent transit, with no China optimization and no guarantee that the assigned IP unlocks streaming services.

| Plan | CPU | RAM | SSD | Traffic / port | List price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| Lite.TINY | 1 core | 0.75 GB | 10 GB | 2 TB @ 1 Gbps | $6.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Lite.STARTER | 1 core | 1.5 GB | 20 GB | 4 TB @ 1 Gbps | $10.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Lite.MINI | 2 cores | 2 GB | 40 GB | 6 TB @ 1 Gbps | $16.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Lite.MICRO | 2 cores | 4 GB | 60 GB | 8 TB @ 1 Gbps | $21.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Lite.MEDIUM | 4 cores | 4 GB | 80 GB | 12 TB @ 1 Gbps | $32.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |
| Lite.LARGE | 4 cores | 8 GB | 100 GB | 22 TB @ 1 Gbps | $49.90/mo | [Check this Tokyo plan](https://www.dmit.io/aff.php?aff=12046) |

Note the RAM on Lite.TINY: 0.75 GB. That is enough for a tunnel, a tiny static site or a monitoring agent, and not much else. Running Docker on it is a bad afternoon.

## The overage policy is the hidden spec

Two DMIT plans can have identical core counts and identical prices and still behave completely differently when you hit the monthly cap.

| Line | When traffic runs out |
| --- | --- |
| Pro (TYO.AS3.Pro) | Service suspended |
| Tier 1 (TYO.AS3.T1) | Throttled to 50 Mbps–1 Gbps, traffic stays unlimited |
| Lite | Per open-beta terms, check the current policy on the order page |

For a production site, "suspended" is a terrifying default. If your site gets a traffic spike on the 27th of the month, a Pro plan goes dark until you buy more traffic or the cycle resets. On T1, the same site just gets slow. Some buyers would rather have the guaranteed route quality and eat the risk; others would rather never go offline. Neither answer is wrong, but you have to pick it deliberately, and DMIT does let you change throttling behaviour from the control panel on the lines that support it.

## Getting the price down

DMIT runs promo codes that are tied to a specific line **and** a specific billing cycle, which is why the ones floating around community forums sometimes fail at checkout. The patterns that have been used recently:

- **Tier 1, quarterly or longer:** 30% off recurring, published as `2025-TYO-T1-HI-GSL-NON-MONTHLY-30OFF`, and separately as `202510_HKG_TYO_T1_30OFF_RECURRING` for Tokyo and Hong Kong T1 (excluding WEE). Monthly T1 orders had a separate 10% code.
- **Pro, quarterly or longer:** 20% off recurring for Tokyo and Hong Kong Pro, and an annual-only 20% recurring code for Tokyo Pro.
- **Lite, annual:** a one-time 50% off code and a recurring 20% off code from the open-beta launch, plus a 30% code for the TINY plan on quarterly or longer terms.

Two honest caveats. Several of these codes carried published expiry dates that have already passed, and DMIT excludes them from stacking with other offers. Enter the code in the order form and use the validation button before you pay. If it validates, you get the discount; if it does not, you pay list price. Do not build a budget around a code you have not validated.

Annual billing is also worth a look on the Lite and T1 lines even without a code, since the effective monthly rate drops noticeably. The Pro line is priced for people who have already decided the route quality is worth it.

## Which DMIT Tokyo plan to actually pick

**A production site with mainland Chinese visitors.** Pro.STARTER minimum. It gives you 2 GB RAM and 1 TB of traffic on the CN2 GIA return path, which is what you are paying the premium for. Pro.TINY works for a low-traffic site but the 500 GB cap and 1 GB of RAM leave no room to grow.

**A site for Japanese, Korean and Southeast Asian users only.** T1.STARTER or T1.MINI. You lose nothing that matters, you keep the unlimited-traffic throttle as a safety net, and the price is a quarter of Pro.

**A relay, tunnel or personal endpoint.** T1.WEE at $36.90/year is the cheapest sensible option. If you want more traffic at a similar cost, Lite.STARTER works, but its no-guarantee open-beta status means you should have a second node configured as a fallback.

**Storage-heavy work with big bandwidth needs.** Lite.MEDIUM or Lite.LARGE. 12 TB and 22 TB a month on a 1 Gbps port at $32.90 and $49.90 is the best traffic-per-dollar in the Tokyo lineup, as long as you do not need China-optimized routing.

**Handling real user data from Japanese customers.** Pro.MICRO and up, with the understanding that you are paying for both route quality and a Japan-resident dataset. Confirm DMIT's terms for your specific compliance obligations rather than assuming.

## Before you order

A short list of things that actually change the outcome:

1. **Test the route from your own network.** DMIT publishes looking-glass endpoints and test IPs. Pinging from your own ISP in your own timezone at peak hour tells you more than any review table, including this one.
2. **Check stock before planning.** Tokyo Pro sells out and comes back in small batches. If TINY is gone, the next plan up is double the price.
3. **Confirm the billing cycle you want is actually discounted.** Monthly Pro orders rarely qualify for the recurring codes.
4. **Re-read the refund and IP-replacement terms.** DMIT points Lite buyers at its ToS specifically, and IP replacement is not free.

👉 [Check DMIT's current Tokyo stock and pricing](https://www.dmit.io/aff.php?aff=12046)

## FAQ

**Is a Japan VPS good for streaming and unlocking service regions?**
Sometimes. A Japan IP gets you a Japanese region, but providers vary in how reliably their Tokyo ranges unlock specific services, and DMIT states that Lite open-beta IPs are not guaranteed to unlock anything. Test the actual IP you are assigned rather than trusting the plan name.

**How is DMIT's Tokyo different from a cheap $3/month Tokyo VPS?**
Route. The cheap end of the market uses whatever transit is cheapest that month, which shows up as swinging latency and packet loss during Chinese peak hours. DMIT's Pro line buys dedicated premium capacity, which is why a 1 GB plan costs more than $20/month.

**Do I need CN2 GIA if my users are in Japan?**
No. CN2 GIA is optimized for traffic heading into mainland China. For Japanese and general Asian visitors, Tier 1 or Lite routing is fine and costs far less.

**Can I pay from China?**
Community posts report PayPal and Alipay as accepted payment methods. Verify at checkout, as payment options can change.

**How bad is the Pro suspension policy in practice?**
It depends entirely on your traffic profile. A steady site that uses 60% of its allowance will never notice. A site with unpredictable viral traffic spikes will, and for that profile T1's throttling behaviour is the safer design.

The short version: in Tokyo, decide your audience first, then your route, then your plan size. Get that order backwards and you end up paying CN2 GIA prices for visitors who were never going to touch a Chinese backbone.
