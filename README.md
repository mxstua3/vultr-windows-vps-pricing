# Best Windows VPS: What Does Vultr Cost, Which Plan Runs MSSQL, and How Do You Claim the $300 Credit? (Full Plan Table + Real Billing Math)

Vultr's cheapest Cloud Compute instance you can put Windows on is **$5/mo** (1 vCPU, 1 GB RAM, 25 GB SSD) before the Windows licence fee that Vultr adds at deploy, and that fee increases as the plan gets bigger. The $300 credit is a new-account promotion (code `FLY300VULTR`) that applies to select products only and cannot be combined with other offers, so treat it as a discount on your first weeks of testing rather than a free Windows licence.

What follows is the plan ladder with the base rates, the difference between a listed monthly price and what actually leaves your bank account, which size fits an ASP.NET site versus MSSQL with remote users, and the Windows-specific traps that surface after you have paid.

> **Short answer:** one ASP.NET site or a small MSSQL instance → 2 vCPU / 2 GB at **$15/mo base** (65 GB SSD, 3 TB bandwidth), plus the licence fee. The $5/mo 1 GB plan is a test box, not a production Windows server, because the OS alone will consume most of that RAM.

👉 [Claim the $300 new-account credit and pick your Windows image](https://bit.ly/VuLtr)

## Every Vultr plan you can realistically run Windows on

| Plan | vCPU / RAM | SSD | Bandwidth | Price (hourly / monthly cap) | Deploy |
| --- | --- | --- | --- | --- | --- |
| vc2-1c-1gb | 1 / 1 GB | 25 GB | 1 TB | $0.007/hr · $5/mo | [Deploy 1 vCPU / 1 GB](https://bit.ly/VuLtr) |
| vc2-1c-2gb | 1 / 2 GB | 55 GB | 2 TB | $0.014/hr · $10/mo | [Deploy 1 vCPU / 2 GB](https://bit.ly/VuLtr) |
| vc2-2c-2gb | 2 / 2 GB | 65 GB | 3 TB | $0.021/hr · $15/mo | [Deploy 2 vCPU / 2 GB](https://bit.ly/VuLtr) |

These are base compute rates. Vultr lists every Windows image with a "+ License Fee" tag and states that Windows licence costs vary by compute plan, so the number you pay is the base rate above **plus** the licence line. Vultr's ladder continues past 2 vCPU / 2 GB with larger instances at higher base rates and correspondingly higher licence fees; the deploy screen shows the combined total for whichever size you pick. The 512 MB tiers at $2.50–$3.50/mo exist in Vultr's catalogue but are not a sensible Windows target.

One regional detail worth knowing before you pick a location: São Paulo carries a surcharge. The 1 vCPU / 1 GB plan is **$7.50/mo** there instead of $5, and the 1 vCPU / 2 GB is **$15** instead of $10. Every other listed region uses the standard rate.

**What comes with the instance**

| Item | Detail |
| --- | --- |
| Windows images | 2016, 2019, 2022 and 2025, in Standard and Datacenter editions, plus "Core" variants that ship without the desktop GUI |
| Licensing | Added automatically at provisioning; existing Windows Server licences cannot be transferred in |
| Regions | 34 cloud data centre regions |
| Security and recovery | Vultr firewall plus automatic backups, both of which you need to switch on rather than assume |
| Billing shape | An hourly rate alongside a monthly cap, with no multi-year prepayment attached |

## The monthly price is not the monthly bill

This is where Windows VPS shopping goes wrong most often, and Vultr is not the offender.

Liquid Web advertises its entry Windows VPS at **$119/mo**. The same card says "With a 2-year plan. You pay $2,856 today." The 8 GB tier reads $142.80/mo and takes **$3,427.20** upfront; the 16 GB tier reads $181.05/mo and takes **$4,345.20**. The monthly figure is a division of a two-year contract, not a payment you can stop next month. Contabo runs the same trick in the other direction: its Cloud VPS prices are marked "for the first 24 months," so the advertised euro rate has a built-in expiry.

Vultr's structure is different in a way that matters for anyone testing Windows workloads. Each plan publishes an hourly rate next to a monthly cap, so a full month costs the cap and a three-day experiment costs three days at the hourly rate. Nothing in Vultr's plan listing asks you to commit two years to get the advertised number.

Run the first-year arithmetic before you decide. On the 2 vCPU / 2 GB tier, twelve months at the base rate is about $180 before the licence fee. On Liquid Web's entry tier, year one is $2,856 paid on day one. Those are not competing products, since one includes Plesk Obsidian, 100 GB of Acronis backups, DDoS protection and an optional managed tier, but you should be comparing them knowing that.

👉 [Check the current credit terms on Vultr's coupons page](https://www.vultr.com/coupons?ref=9738262-9J)

## Which size for which job

**One ASP.NET site, low to moderate traffic.** The 1 vCPU / 2 GB at $10/mo base is the honest starting point if you are not running SQL Server on the same box. Move to 2 vCPU / 2 GB when you want the site and your build process to coexist without competing for a single core.

**MSSQL plus a handful of remote users.** Start at 2 vCPU / 2 GB and expect to climb. SQL Server caches aggressively and will take whatever RAM you give it, so 2 GB is a floor for a small database, not a comfortable ceiling. The good news is that resizing on Vultr's ladder costs you the price difference rather than a new contract.

**A remote desktop for a team.** Read the licensing section below before you promise anyone a desktop. Hosting several simultaneous interactive sessions is an RDS licensing question, not a RAM question.

**You do not want to touch patches.** Vultr gives you a server, not an administrator. Liquid Web sells three management levels (fully managed, core managed, unmanaged) on top of Windows-certified technicians, at the two-year prepay prices above. That is the trade: roughly $2,856 upfront for hands-off patching versus a $15/mo base rate and a Windows Update schedule you own.

**You want maximum specs per euro and accept self-management.** Contabo's Cloud VPS 4 gives 4 vCPU, 8 GB RAM, 100 GB SSD and a 200 Mbit/s port on a promotional rate for the first 24 months. The page describes its own product as unmanaged Windows VPS hosting.

**You want a fixed low monthly with unlimited traffic.** OVHcloud's VPS-2 starts at $8.50/mo with 4 vCores, 8 GB RAM and 75 GB NVMe on a 99.9% SLA.

## Windows-specific traps that are not on the pricing page

**The licence fee is a separate line.** Vultr's images are tagged "+ License Fee," and the site states plainly that licence costs vary by plan. Budget for it as a real cost, not a rounding error, and check the figure on the deploy screen before you commit to a size.

**You cannot bring your own licence.** Vultr provisions Windows with the licence included and does not accept transferred existing Windows Server licences. If your plan was to reuse volume licensing, that plan does not work here.

**Operating system choices can be one-way.** IONOS states outright that a Windows virtual server cannot be switched to Linux later and that switching means placing a new order. Whether a given Vultr instance can be rebuilt on a different OS after deployment is something to confirm on the deploy screen rather than assume in either direction.

**Windows availability is not universal across a provider's regions.** OVHcloud excludes Windows from its Local Zones, alongside preinstalled apps, additional storage and load balancing. Vultr publishes 34 regions, and the São Paulo surcharge above is a reminder that "same plan, different region" can mean a different price and sometimes a different feature set.

**Unlimited traffic usually has a map attached.** OVHcloud's unlimited traffic explicitly excludes its Asia-Pacific data centres. If your users are in Singapore and your server is in Europe, that clause is your problem.

**Remote desktop concurrency is licensed, not just configured.** Windows Server's built-in remote access is intended for administration. Serving several people with simultaneous desktop sessions properly requires RDS client access licences, and no VPS plan bundles those. Confirm the session behaviour with the provider before you build a workflow around five people logging in at once.

**Bandwidth numbers are not comparable across providers.** Contabo quotes port speed (200 Mbit/s on the entry tier up to 1 Gbit/s). OVHcloud quotes public bandwidth of 1 to 3 Gbps. Vultr quotes a monthly transfer allowance in terabytes. A 200 Mbit/s port and a 3 TB allowance describe different things, and neither is directly better than the other without knowing your traffic pattern.

## How the Windows VPS field compares

| Provider | Example plan | Specs | Price and payment | Watch out for |
| --- | --- | --- | --- | --- |
| Vultr | vc2-2c-2gb | 2 vCPU / 2 GB / 65 GB SSD / 3 TB | $15/mo base + licence fee, hourly rate published | Licence fee is extra; no BYOL |
| OVHcloud | VPS-2 | 4 vCores / 8 GB / 75 GB NVMe / 1 Gbps | From $8.50/mo, monthly | No Windows in Local Zones; unlimited traffic excludes Asia-Pacific |
| Contabo | Cloud VPS 4 | 4 vCPU / 8 GB / 100 GB SSD / 200 Mbit/s port | Euro pricing, promotional rate for the first 24 months | Unmanaged; promotional period expires |
| IONOS | Windows VPS+ | Windows M+ tier, 2 vCores | Not quoted here | Windows cannot be switched to Linux; new order required |
| Liquid Web | 4 GB tier | 2 vCPU / 4 GB / 80 GB / 3 TB | $119/mo on a 2-year plan, $2,856 today | Two-year prepay; Plesk, Acronis backups and DDoS included |

## FAQ

**How do I actually claim the $300 credit?**
Vultr's coupons page lists `FLY300VULTR` for $300 of free credit. The terms attached to it: new customers only, applies to select products only, cannot be combined with other offers, restrictions and terms apply. Vultr also lists `VULTRMATCH`, which matches your first deposit dollar for dollar up to $100, under the same new-customer and select-product conditions.

**Does the credit cover the Windows licence line?**
The offer text says select products, which is not the same as everything on your invoice. After signup, open the billing dashboard and confirm the licence fee is drawing from the promotional balance. If it is not, your effective cost is the base rate plus the licence fee in cash.

**Is the Windows licence included in the price?**
It is provisioned automatically with the instance and charged as a fee on top of the compute rate. It is not transferable in either direction: you cannot bring an existing licence, and the licence stays with the Vultr instance.

**Can I run SQL Server?**
The images Vultr lists are operating systems, not database templates. You install SQL Server on the instance and handle Microsoft's licensing for it yourself; the VPS price does not include a SQL Server licence.

**Is there a trial or a refund?**
The $300 credit is the trial mechanism Vultr advertises. Beyond that, hourly billing is the practical safety net: a small instance you run for three days costs three days at the hourly rate, which is a cheap way to benchmark a Windows image before committing to a monthly cap.

## The decision, in one pass

Single ASP.NET site, you handle the patching → **1 vCPU / 2 GB at $10/mo base**, and step to 2 vCPU / 2 GB at $15 if the site shares the box with builds or a database. MSSQL with real users → start at 2 vCPU / 2 GB and expect the first resize within a month, because SQL Server will make 2 GB feel tight. You want someone else on patch duty and can fund a two-year contract → Liquid Web's managed tiers at $119/mo equivalent. You want the largest specs for the smallest monthly number and are comfortable with a terminal → Contabo, with the promotional period in mind.

Two things to confirm before you pay: the **combined total of base rate plus Windows licence fee** on the deploy screen for the exact size and region you chose, and whether the **promotional credit applies to that licence line**. Those two figures turn a $15/mo headline into your actual first-year cost, which is the only number that should drive the decision.

👉 [Start with the $5/mo 1 GB instance and the $300 credit, then resize once you see your real usage](https://bit.ly/VuLtr)
