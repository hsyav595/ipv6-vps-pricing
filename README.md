# Cheap IPv6 VPS: What $3 a Month Really Buys, IPv6-Only vs Dual-Stack, and Whether You Can Add IPv4 Later

Cheap IPv6 VPS pricing clusters in three places right now: about $2.50 to $3 a month for a 512 MB to 1 GB machine on monthly billing, around €5 a month for 4 GB of RAM in a European datacenter, and $10 to $30 a year if you accept an annual promo SKU from a budget host. Evoxt sits in the first group at $2.99 a month, and its VMs are listed with IPv6 support rather than sold as stripped-down IPv6-only boxes.

That last distinction matters more than the price. Dropping the public IPv4 address is what lets a host sell a 1 GB VM for €3, and it's also what makes some workloads fail outright. Whether you can add IPv4 back after ordering depends entirely on the provider, and almost nobody checks before paying. Below: Evoxt's complete plan list with current prices, where the IPv6 discount actually comes from, which hosts let you fix the IPv4 mistake later, and the three workloads that should never run on an IPv6-only machine.

> **Quick pick:** Evoxt VM-0.5 at **$2.99/month** (1 core, 512 MB RAM, 5 GB storage, 250 GB transfer, weekly offsite backup included) is the cheapest way to get an IPv6-capable VM without giving up normal networking. Running anything past a tunnel endpoint or a cron box? Go to VM-1 at **$5.99/month** for 2 GB RAM and 20 GB storage.
> 👉 [Check Evoxt's current plan pricing](https://bit.ly/EvoXt)

## Evoxt's full plan list, all eleven sizes

Evoxt runs a single VM line with eleven configurations. Every plan includes a weekly offsite backup at no extra charge, and you can add individual resources to an existing VM instead of jumping to the next plan.

| Plan | CPU / RAM | Storage / monthly transfer | Price | Order |
| --- | --- | --- | --- | --- |
| VM-0.5 | 1 core / 512 MB | 5 GB / 250 GB | $2.99/mo | [Deploy VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 core / 1 GB | 10 GB / 250 GB | $4.99/mo | [Deploy VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 core / 2 GB | 20 GB / 500 GB | $5.99/mo | [Deploy VM-1](https://bit.ly/EvoXt) |
| VM-1.5 | 2 cores / 2 GB | 20 GB / 500 GB | $6.95/mo | [Deploy VM-1.5](https://bit.ly/EvoXt) |
| VM-2 | 2 cores / 4 GB | 30 GB / 1,000 GB | $11.99/mo | [Deploy VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 cores / 4 GB | 30 GB / 1,000 GB | $14.99/mo | [Deploy VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 cores / 8 GB | 60 GB / 2,000 GB | $23.99/mo | [Deploy VM-4](https://bit.ly/EvoXt) |
| VM-6 | 8 cores / 8 GB | 60 GB / 2,000 GB | $29.99/mo | [Deploy VM-6](https://bit.ly/EvoXt) |
| VM-8 | 8 cores / 16 GB | 80 GB / 3,000 GB | $47.99/mo | [Deploy VM-8](https://bit.ly/EvoXt) |
| VM-12 | 16 cores / 16 GB | 80 GB / 3,000 GB | $60.95/mo | [Deploy VM-12](https://bit.ly/EvoXt) |
| VM-16 | 16 cores / 32 GB | 100 GB / 5,000 GB | $95.99/mo | [Deploy VM-16](https://bit.ly/EvoXt) |

A few things the table doesn't show. Evoxt builds its pitch around single-core clock speed (the company advertises 3.5 GHz and above) instead of core count, which is why the 1-core VM-1.5 costs almost the same as the 2-core VM-1. Third-party spec listings put Evoxt at 18 datacenters across four continents, with a custom control panel, a REST API, an external firewall, VNC access and cloning. Billing runs from monthly up to three years, and you can top up account credit and let the system apply it to future invoices. Payment options are credit card, debit card, PayPal, Bitcoin and USDt Tron. There is no hourly billing, and third-party spec sheets list no DDoS protection, so anything that attracts attacks belongs behind a proxy or CDN.

The bandwidth model is allowance-then-throttle. You get the monthly transfer in the table, and going over slows the port rather than generating an overage bill.

## Where the "IPv6 discount" actually comes from

IPv4 addresses cost money and IPv6 space doesn't, so a host that skips the IPv4 can cut the price and keep the same hardware. Hostynet puts a number on it: up to **28% cheaper for identical specs**, with the only difference being no public IPv4. servinga applies the same logic and lands at **€3/month** for 1 vCPU, 1 GB RAM, 25 GB SSD and 2 TB of traffic, with a /64 subnet available as an option.

The discount is real, but it isn't the whole price story. Cloudzy sells a **dual-stack** 512 MB VM with a dedicated IPv4 plus a routable /64 for **$2.48/month** on its current 50% promotion, list price $4.95. So a box with both protocols can undercut an IPv6-only box from another provider. Cheap comes from the provider's cost structure and how aggressively it prices, not only from which IP families it hands out.

What $3 a month buys in practice: 512 MB to 1 GB of RAM, 5 to 25 GB of disk, and between 250 GB and 2 TB of monthly transfer. Enough for a VPN endpoint, a monitoring agent, a small API, or a CI runner. Not enough for a database that matters.

## Can you add IPv4 after you order? Sometimes no

This is the question to settle before payment, because the two answers in the market are opposite.

servinga states plainly that it is **not possible to add an IPv4 address to an IPv6-only server after deployment**, for technical reasons, and that you should book an IPv4-capable server from the start if you need one. Pick wrong and you're buying a second server.

Hostynet takes the other position and advertises **dual-stack anytime, add IPv4 when needed**. Same category of product, opposite upgrade path.

Neither is lying; they built their platforms differently. The lesson is that "I'll add IPv4 later if it's a problem" is a plan you have to verify per provider, in writing, before you pay.

Evoxt avoids the trap by not selling an IPv6-only SKU at all. You're buying a normal VM with IPv6 support listed, so there's no IPv4 to add later and no discount to lose. If you plan to hand addresses to containers or tenants, ask support what IPv6 allocation comes with the plan before you order; a single address and a routed /64 support very different architectures.

Also worth knowing: on Cloudzy, disabling IPv4 inside the operating system doesn't stop it being allocated and billed. You can't convert a dual-stack plan into an IPv6-only discount after the fact.

## Three workloads that break on IPv6-only

Hostynet publishes an unusually honest "not recommended for" list, and it matches what you'd hit in production:

1. **Public web servers where most visitors are IPv4-only.** Mobile carriers, hotels and corporate networks still expose IPv4 addresses to a lot of users. If your traffic is consumer-facing and broad, some percentage simply won't connect.
2. **Inbound mail servers (MX).** Third-party SMTP relays still favour IPv4, and reverse DNS for IPv6 isn't guaranteed on every upstream.
3. **Mainstream game servers.** Minecraft and most of its player base live on IPv4.

The standard workaround, which HardBrain spells out, is to pair the IPv6-only box with a small IPv4 machine acting as the public edge. A reverse proxy, load balancer or WireGuard hop terminates IPv4 traffic and forwards over IPv6 to the cheap backend. That works well and it's how a lot of people run it, but it means two servers to patch and pay for, which eats the 28% you saved.

Outbound traffic is the failure mode people forget. An IPv6-only server can't reach an IPv4-only API, package mirror or payment webhook unless the provider runs NAT64/DNS64 or you tunnel out. Check that before you move a build pipeline onto one.

## How the cheap IPv6 options compare

| Provider | Entry plan | Price | IPv6 model | Where | Catch worth knowing |
| --- | --- | --- | --- | --- | --- |
| Cloudzy | 1 vCPU / 512 MB / 20 GB NVMe / 1 TB | $2.48/mo (50% off, list $4.95) | Dual-stack, routable /64 plus dedicated IPv4 | 13 regions | Discount is a running promo; IPv4 stays billable even if disabled in the OS |
| servinga | 1 vCPU / 1 GB / 25 GB / 2 TB | €3/mo | IPv6-only, /64 optional, Linux only on entry plan | 9 locations, Europe plus Dallas | Cannot add IPv4 after deployment |
| Hostynet | 2 vCPU / 4 GB / 30 GB SSD / 100 Mbit | €4.99/mo incl. tax | IPv6-only, IPv4 addable later | France | Unlimited traffic, 99% SLA, not for public IPv4-facing sites |
| HardBrain | 1 core / 6 GB / 40 GB NVMe / 5 TB | Prices load from a live catalog; no figure published on the page | IPv6-only, 1x /64 per plan | Frankfurt, Equinix FRA-7 | No IPv4; budget for a separate IPv4 front |

Currency and tax treatment differ between these listings: Hostynet quotes tax-inclusive euros, servinga quotes euros without stating tax, Cloudzy quotes US dollars. Don't rank them against each other without converting first.

## FAQ

**Will an IPv6-only VPS open IPv4 websites?**
Not without help. The server can only reach what it can route, so an IPv4-only destination needs NAT64/DNS64 from the provider or a tunnel you run yourself. Hostynet's own answer for inbound connections is the same: the client needs IPv6, or a tunnel or proxy in front.

**What is a /64 for?**
It's a block of IPv6 addresses routed to your machine, not a single address. Cloudzy routes the whole /64 to eth0, which lets you give containers, services or individual customers their own globally reachable address instead of building NAT and port-allocation rules. HardBrain includes one /64 on every plan, servinga offers it as an option.

**What happens when I exceed the traffic allowance?**
Policies vary and they decide whether your service goes down. servinga doesn't deactivate the server; it drops the port to 10 Mbit/s until the cycle resets, which keeps normal applications running. Hostynet advertises unlimited traffic. Evoxt throttles rather than charging overage. None of these suspend you, but a throttled port on a 100 Mbit plan is a different experience from a 1 Gbit one.

**Is the promo price the price I'll pay next year?**
Check the list price behind the discount. Cloudzy's $2.48 is 50% off a $4.95 plan and the promotion has no published end date, so treat the discounted figure as a first-term number rather than a permanent rate.

## How to choose

Match the machine to the workload and the IPv4 question answers itself:

- **Tunnel endpoint, CI runner, queue worker, backend behind a proxy, lab box.** You never needed IPv4. Take the cheapest plan that fits, or Evoxt VM-0.5 at $2.99 if you'd rather have a normal dual-stack VM and stop worrying about edge cases.
- **Anything serving IPv4-only visitors, inbound mail, or game clients.** Dual-stack, no compromise. Either buy a dual-stack plan or budget for a second IPv4 front-end machine.
- **Traffic that spikes unpredictably.** Read the overage policy before the price. Throttling keeps you online at reduced speed; suspension doesn't.
- **Long prepay discounts.** A $9.88/year promo SKU is roughly 82 cents a month, and it's also a locked-in annual commitment from a budget host. Worth it for a hobby node, wrong for anything you can't rebuild from a backup.

Three things to confirm before you pay: whether IPv4 can be added later (and at what price), what IPv6 allocation you actually receive, and what the refund window is if you prepay beyond a month. Then pick the smallest plan that runs your workload.

👉 [Start with Evoxt's VM-0.5 at $2.99/month and scale up when you need to](https://bit.ly/EvoXt)
