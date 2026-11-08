# Dedicated hosting: what a whole server really costs, when a VPS beats it, and what the monthly fee leaves out (Spin Servers plans compared)

Dedicated hosting rents you an entire physical server: every core, every gigabyte of RAM, every disk, and the network port. Nothing else runs on that hardware unless you install it. The bill reflects the exclusivity, and against a VPS with similar nominal specs the gap is usually several times over, before management, control panel licences or a commercial OS get added.

Spin Servers sells these machines in two US locations, Dallas and San Jose. Every listing comes with 10Gbps networking, 30TB of monthly transfer, month-to-month billing and no setup fee, and the San Jose page advertises the lineup from **$79.00 per month**. Below you'll find the current configurations, the point where a single-tenant box stops being worth the money, how 95th-percentile bandwidth billing and per-account control panel fees change the real monthly number, and what to confirm before you order.

> **Quick pick.** Start with the 16-core/32-thread, 64GB machines (SJC‑202 with SSD, SJC‑206 with NVMe). They cover a busy database-backed site or a small private cloud without paying for capacity you can't use yet. Take the 4-core Xeon E3‑1280 v5 (SJC‑205, or the Dallas equivalent) when single-thread speed and NVMe throughput matter more than core count. The 32-core/512GB SJC‑204 only makes sense if you already know you're RAM-bound. 👉 [See the current Spin Servers configurations and live prices](https://bit.ly/Spinservers)

## The current Spin Servers lineup, Dallas and San Jose

Both locations run bare metal, so there's no virtualization layer between your OS and the hardware. Dallas listings provision automatically once the order is approved; San Jose listings are marked instant. IPMI/KVM console access is part of the package, which matters the day a kernel update leaves a machine unbootable.

**Dallas, Texas**

| Plan | CPU | RAM | Storage | Network | Price |
| --- | --- | --- | --- | --- | --- |
| Intel Xeon E3‑1280 v5 | 4 cores / 8 threads, 3.7GHz turbo | 32GB DDR4 ECC | 1TB M.2 NVMe | 10Gbps port, 30TB/month, 1 IPv4 | [Live price](https://bit.ly/Spinservers) |
| Dual Intel Xeon E5‑2630L v3 | 16 cores / 32 threads, 2.90GHz turbo | 128GB DDR4 ECC | 1TB NVMe | 10Gbps port, 30TB/month | [Live price](https://bit.ly/Spinservers) |

**San Jose, California**

| Plan | CPU | RAM | Storage | Network | Price |
| --- | --- | --- | --- | --- | --- |
| Dual Xeon E5‑2630L v3, 1.6TB SSD (SJC‑202) | 16C / 32T, 1.8–2.9GHz | 64GB DDR4 ECC | 1 × 1.6TB SSD | 2 × 10Gbps, 30TB/month | [Live price](https://bit.ly/Spinservers) |
| Dual Xeon E5‑2630L v3, 1.6TB NVMe (SJC‑206) | 16C / 32T, 1.8–2.9GHz | 64GB DDR4 ECC | 1 × 1.6TB NVMe | 2 × 10Gbps, 30TB/month, 1 IPv4 | [Live price](https://bit.ly/Spinservers) |
| Dual Xeon E5‑2650L v3 (SJC‑203) | 24C / 48T, 1.8–2.5GHz | 64GB DDR4 ECC | 1 × 1.6TB SSD | 2 × 10Gbps, 30TB/month | [Live price](https://bit.ly/Spinservers) |
| Dual Xeon E5‑2630L v3, 256GB (SJC‑201) | 16C / 32T, 1.8–2.9GHz | 256GB DDR4 ECC | 2 × 1.6TB SSD, hardware RAID with cache | 2 × 10Gbps, 30TB/month | [Live price](https://bit.ly/Spinservers) |
| Dual Xeon E5‑2683 v4 (SJC‑204) | 32C / 64T, 2.1–3.0GHz | 512GB DDR4 ECC | 2 × 3.84TB SSD, RAID with battery-backed cache | 2 × 10Gbps, 30TB/month, 1 IPv4 | [Live price](https://bit.ly/Spinservers) |
| Intel Xeon E3‑1280 v5, 1TB NVMe (SJC‑205) | 4C / 8T, 3.7–4.0GHz | 32GB DDR4 ECC | 1 × 1TB M.2 NVMe | 2 × 10Gbps, 30TB/month, 1 IPv4 | [Live price](https://bit.ly/Spinservers) |
| 12C / 24T entry configuration (San Jose) | 12C / 24T, 2.6–3.1GHz | 64GB DDR3 ECC | 1 × 240GB SSD | 2 × 10Gbps, 30TB/month, 1 IPv4 | [Live price](https://bit.ly/Spinservers) |

Two things about that table. Per-configuration prices are published on the order page, not in the listing text, and the **$79.00/month** figure is the "starting from" price shown on the San Jose page. The smallest machine listed there is the 12-core/24-thread box with 64GB of older DDR3 and a single 240GB SSD, so treat that as the entry point and confirm the exact match on the order page rather than assuming the $79 applies to a 16-core machine. Memory generation and disk size are where the cheap tiers differ most.

## Dedicated hosting vs VPS vs a dedicated instance in the cloud

All three put you on one physical machine's worth of silicon. What changes is how much of that machine is yours and who controls the layer underneath.

|  | Dedicated server | VPS |
| --- | --- | --- |
| **Resource allocation** | Every core, bit of RAM and disk on the machine | A partitioned slice with fixed limits |
| **Scalability** | Manual: add disks or a second server, with cost and downtime | Reallocate resources to a degree, bounded by the host machine |
| **Performance** | Full system resources, no noisy neighbours | Comparable for smaller workloads |
| **Customizability** | Anything you want on the box | Restricted by other tenants on the parent machine |
| **Cost** | Highest, hardware included | Pay for what you need |
| **Security and isolation** | Advanced controls, hardware-level separation | Effective, not always enough for complex compliance |

AWS publishes that comparison on its own site, and it also calls dedicated servers expensive and often unnecessary for most organizations. Read that with the source in mind: the company sells VPS and cloud instances, so the framing favours the cheaper product. The underlying point still holds for a single small site. If one WordPress install with modest traffic is the whole workload, a $79 bare metal box is overspending by a wide margin, and a VPS or a virtual dedicated server does the job.

The cloud vocabulary adds more confusion than it clears. A **bare metal server** is a dedicated server hosted and managed by a cloud provider, and the term gets used interchangeably with dedicated server. **Amazon EC2 Dedicated Hosts** give you a whole physical server with EC2 capacity on top, which preserves per-socket and per-core licences for Windows Server, SQL Server or SUSE Linux Enterprise. **EC2 Dedicated Instances** are VMs on hardware reserved for one customer, and two restrictions get buried: they may share hardware with other instances in the same AWS account that aren't Dedicated Instances, and the architecture doesn't support per-machine software licensing. If licence compliance is the reason you're shopping, Dedicated Instances can quietly fail the requirement.

## What the monthly fee leaves out

The advertised price buys hardware, power, network and a working OS install. Everything past that is a line item. Published add-on prices from Namecheap give a realistic scale for the market, and they are not Spin Servers quotes:

- **Management**: free if you take full responsibility, **$20.00/month** for Basic, **$50.00/month** for Complete, which adds weekly backups to separate storage up to 200GB.
- **Server failure restore**: **$10.00 flat** per restore.
- **Core software change** (OS reinstall, version change): **$20.00 flat** for the first hour, **$10.00/hour** after that; $15.00 for the first hour on the Basic tier.
- **cPanel**: billed per account since the licensing change, from **$19.88/month** for the Solo tier.
- **Commercial operating systems**: Windows Server arrives through Microsoft's SPLA programme, Red Hat Enterprise through a monthly subscription that includes updates. Most Linux distributions and the BSDs cost nothing.

Run the arithmetic on a $79 server with Complete management and a cPanel account and the monthly outlay lands near **$149** before you've bought a single licence or backup slot. That number, not the sticker price, is what you compare against a managed VPS. 👉 [Check what Spin Servers includes in the base price and what's quoted separately](https://bit.ly/Spinservers)

## 30TB on a 10Gbps port: how the bandwidth is actually metered

Two numbers that get read as one. **30TB monthly transfer** is a volume allowance. **10Gbps** is port speed. A 10Gbps port running flat out moves roughly 3.2 petabytes in a month, so the quota bites long before the port does. You're buying burst capability for traffic spikes, not 30TB of sustained throughput.

Many providers meter line speed at the **95th percentile**, also called burstable billing: the port is sampled every five minutes across the month, the highest 5% of readings are discarded, and the next-highest reading becomes the billable rate, expressed in Kbps, Mbps or Gbps. Bursty workloads survive this well; a machine sitting at high throughput around the clock does not. Others bill per gigabyte of total traffic, a shift the industry has been making for years. Ask which model applies before you sign, because a 30TB allowance and a 95th-percentile commitment are different products at the same headline speed.

Network SLAs sit in the 99% to 100% range among quality providers, achieved with multiple upstream carriers and redundant hardware. Spin Servers runs its own network (AS396073) across several upstreams with DDoS filtering, and advertises Tier III data centres.

## Four management levels, and who should pick each

| Level | What the provider does | Who it fits |
| --- | --- | --- |
| **Fully managed** | Monitoring, software updates, reboots, patches, OS upgrades; you stay hands-off | Teams without a sysadmin who still need the whole machine |
| **Managed** | Medium-level monitoring, updates and limited support; you handle some tasks | In-house IT with partial coverage |
| **Self-managed** | Regular monitoring and some maintenance; most work stays with you | Experienced admins who want a safety net |
| **Unmanaged** | Almost no involvement; you own patching, upgrades, security | Anyone with a working ops routine |

The market price difference between the bottom and the top of that ladder runs about **$50 per month**. A dedicated server is usually unmanaged by default, and that default is fine for a team already running configuration management. For a company whose entire server experience is a cPanel login, the managed add-on is cheaper than the first outage.

## Compliance is not the same as security

A dedicated server gives you isolation, your own firewall rules and your own patch schedule. It does not hand you a certificate. Healthcare, financial and legal workloads operate under frameworks such as SOC 2, HIPAA or PCI DSS, and satisfying them requires evidence about the provider's environment: attested reports, data centre controls, access logs, a signed business associate agreement where relevant. Ask for the specific documents tied to your obligation instead of accepting "compliant infrastructure" as a phrase. Third-party coverage of Spin Servers describes SOC 2, HIPAA and PCI aligned Tier III facilities; verify that directly with the provider against your own framework before you move regulated data. 👉 [Compare the Dallas and San Jose configurations before you shortlist](https://bit.ly/Spinservers)

## Size the machine by bottleneck, not by visitor count

There is no visitor threshold that flips a site from VPS to dedicated. Resource contention decides it, and a small site running heavy database queries can lose a shared plan on its own. Match the symptom to the spec:

- **Pages hang at peak hours, CPU pinned under load** → cores. The 24-core SJC‑203 exists for this, though the 16-core machines handle most sites.
- **Slow queries, failing cache, timed-out connections** → RAM. This is the resource people underestimate most. SJC‑201 (256GB) and SJC‑204 (512GB) are the answers, and 64GB covers a surprising amount of caching.
- **Disk filling faster than expected, unwieldy backups, large media libraries or many client accounts** → storage, plus RAID for redundancy. SJC‑201 and SJC‑204 include hardware RAID with cache.

Start at the tier that matches the bottleneck you can measure. Move up when a product launch or a seasonal peak is inside three months, not because the next tier looks more comfortable.

## Before you order, confirm four things

Get these in writing, since they decide whether the cheap tier stays cheap:

1. **Root access and out-of-band console.** Full root comes standard on bare metal, and IPMI/KVM access saves you a support ticket when a boot loader breaks. Confirm both.
2. **What the SLA covers and when support answers.** Network uptime guarantees say nothing about hardware replacement times or whether support is business hours or 24/7.
3. **Billing cycle and cancellation terms.** Month-to-month with no setup fee keeps your exposure to one cycle. Check the notice period and whether any refund window exists before you prepay.
4. **Bandwidth overage and extra IPv4 pricing.** The 30TB allowance and the included addresses are the two places overage charges appear.

## Which machine, for which situation

Need hardware-level isolation for regulated data, or software licensed per socket or per core? Go dedicated, and partition the box into VMs if that lets you amortise the licence across several environments (Windows Server, SQL Server and SUSE all license this way).

Running a busy storefront, a game server, a VPN endpoint or a media-heavy publisher with sustained concurrency? The 16-core/64GB machines (SJC‑202, SJC‑206) are the sane starting point, and SJC‑205 with its 4.0GHz turbo and NVMe is the pick when single-thread response time is what users feel.

Building a small private cloud across several boxes? Dual 10Gbps ports and a free private L2 network between servers change what you can architect, and month-to-month billing means you can add a second machine for a project and drop it afterwards.

One modest website, a tight budget, nobody on staff who patches a kernel? A VPS or a managed virtual dedicated server is the right purchase, and buying bare metal will just move the cost from the invoice to your evenings.

👉 [View the live Spin Servers plan list and order page before you commit](https://bit.ly/Spinservers)
