# Evoxt WordPress: Which One-Click Install Do You Pick, and Which Plan Actually Runs the Site? (Both Setup Paths, All 11 Plans, Prices and Bandwidth Compared)

Evoxt offers two WordPress one-click apps, and both end at the same place: open `YOUR_VM_IP/install` in a browser and run the standard WordPress installer. For a personal blog, start at VM-0.75 ($4.99/mo, 1 GB RAM) or VM-1 ($5.99/mo, 2 GB); the $2.99 VM-0.5 ships with 512 MB, which leaves MySQL and PHP almost no headroom. This guide covers the two install paths step by step, the full plan list, which plan fits which kind of WordPress site, and the regional bandwidth difference that most reviews leave out.

> **Quick pick:** VM-1 at $5.99/mo (1 core, 2 GB RAM, 20 GB storage, 1,000 GB transfer) covers a blog or small business site with room to spare. Running WooCommerce or a plugin-heavy build? Go to VM-2 at $11.99/mo for 4 GB RAM. Testing something or running a thin static-ish site? VM-0.75 at $4.99/mo.
> 👉 [Deploy a WordPress one-click app on Evoxt](https://bit.ly/EvoXt)

## Two WordPress one-click installs, and why the choice matters

The two apps give you different web servers underneath. One deploys WordPress on OpenLiteSpeed; the other is a plain build that comes with phpMyAdmin preinstalled. Everything after the install (themes, plugins, the admin dashboard) is normal WordPress, so the decision comes down to which server you want to maintain and how you want to reach your database.

### Path A: WordPress with OpenLiteSpeed

1. Deploy the **WordPress with OpenLiteSpeed** app from the one-click list. Your VM details arrive by email, so check the spam folder if nothing shows up.
2. Visit `YOUR_VM_IP/install`. Pick a language, enter the site title, admin username, password and email address, then click Install WordPress.
3. Install the **LiteSpeed Cache** plugin: Plugins → Add New → search "LiteSpeed Cache" → Install → Activate. OpenLiteSpeed's page caching does little for WordPress until that plugin is active, so this step is what turns the server choice into actual speed.
4. The OpenLiteSpeed admin panel lives at `YOUR_VM_IP:7080`. Get the login from SSH with `cat /usr/local/lsws/adminpasswd`, or reset it with `/usr/local/lsws/admin/misc/admpass.sh`.
5. Your WordPress database credentials are in `cat /usr/local/lsws/password`.

One quirk: the OpenLiteSpeed tutorial page still carries a leftover sentence about the system setting up "a drupal site." You are installing WordPress. Ignore the line and follow the steps.

### Path B: Plain WordPress with phpMyAdmin

1. Deploy the standard **WordPress** one-click app.
2. Open `YOUR_VM_IP/install` and complete the same installer: language, site title, username, password, email.
3. phpMyAdmin is already installed at `YOUR_VM_IP/phpMyAdmin`. The capital **M** and capital **A** matter; a lowercase path returns a 404.
4. Log in as `root`. The password comes from SSH: `cat /var/log/mysqld.log`.

This path suits you if you expect to poke at the database directly (migrations, broken plugin cleanup, staging clones) and would rather not install phpMyAdmin yourself.

### The step both paths need: point the domain

Add an A record for your domain pointing at the VPS IP. Until DNS propagates, the domain will not resolve to your new site, and WordPress will keep answering on the raw IP. Do this before you start sending traffic or configuring SSL.

👉 [Start a VM and pick WordPress from the one-click catalog](https://bit.ly/EvoXt)

## All Evoxt plans, side by side

Every standard-region plan runs on a 1 Gbps port and includes weekly offsite backups. Prices below are the publicly listed monthly rates at the time of writing.

| Plan | CPU / RAM | Storage | Monthly transfer | Price |
| --- | --- | --- | --- | --- |
| VM-0.5 | 1 core / 512 MB | 5 GB | 500 GB | $2.99/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-0.75 | 1 core / 1 GB | 10 GB | 750 GB | $4.99/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-1 | 1 core / 2 GB | 20 GB | 1,000 GB | $5.99/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-1.5 | 2 cores / 2 GB | 20 GB | 1,500 GB | $6.95/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-2 | 2 cores / 4 GB | 30 GB | 2,000 GB | $11.99/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-3 | 4 cores / 4 GB | 30 GB | 3,000 GB | $14.99/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-4 | 4 cores / 8 GB | 60 GB | 4,000 GB | $23.99/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-6 | 8 cores / 8 GB | 60 GB | 5,000 GB | $29.99/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-8 | 8 cores / 16 GB | 80 GB | 6,000 GB | $47.99/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-12 | 16 cores / 16 GB | 80 GB | 8,000 GB | $60.95/mo ·  [Order](https://bit.ly/EvoXt) |
| VM-16 | 16 cores / 32 GB | 100 GB | 10 TB | $95.99/mo ·  [Order](https://bit.ly/EvoXt) |

All plans use KVM virtualisation and NVMe storage, with base clocks listed at 3.5 GHz and turbo up to 6.0 GHz. Faster single-core clocks help WordPress more than extra cores do, because PHP execution and database queries are largely single-threaded.

### Hong Kong, Osaka and Malaysia Premium: same price, less transfer

The premium locations carry identical CPU, RAM and storage at identical prices. What changes is the monthly transfer allowance, roughly halved, because bandwidth in those markets costs more.

| Plan | Standard regions | Hong Kong / Osaka | Malaysia Premium |
| --- | --- | --- | --- |
| VM-0.5 | 500 GB | 250 GB | 150 GB ($3.49/mo) |
| VM-0.75 | 750 GB | 250 GB | 250 GB |
| VM-1 | 1,000 GB | 500 GB | 300 GB |
| VM-1.5 | 1,500 GB | 500 GB | 300 GB |
| VM-2 | 2,000 GB | 1,000 GB | 600 GB |
| VM-3 | 3,000 GB | 1,000 GB | 700 GB |
| VM-4 | 4,000 GB | 2,000 GB | 1,000 GB |
| VM-6 | 5,000 GB | 2,000 GB | 1,250 GB |
| VM-8 | 6,000 GB | 3,000 GB | 2,000 GB |
| VM-12 | 8,000 GB | 3,000 GB | 2,500 GB |
| VM-16 | 10 TB | 5,000 GB | 4,000 GB |

Hong Kong uses CN2 routing, which is the reason to pay the bandwidth penalty if your readers are in mainland China. For a WordPress site with images and a bit of video, 500 GB on VM-1 in Hong Kong is roughly 16 GB a day; a text-heavy blog with caching will not come close, a media-heavy site might.

## Which plan should a WordPress site actually run on?

Work backwards from what WordPress does on a request: PHP workers, a database query or two, and whatever your plugins add. Memory is the binding constraint far more often than CPU.

**Testing, staging, or a single-page site: VM-0.5 ($2.99).** 512 MB runs the stack, but MySQL, PHP and the OS are all competing for the same small pool. Expect to tune MySQL's buffer settings and skip heavy plugins. It works as a sandbox; it is a poor home for a site you care about.

**Personal blog or small business site: VM-0.75 ($4.99) or VM-1 ($5.99).** The 1 GB plan handles a blog with a caching plugin and modest traffic. VM-1 doubles the RAM to 2 GB and the storage to 20 GB for one dollar more than VM-0.75, which makes it the easier recommendation: plugin updates, backups and traffic spikes all need memory, and $1 buys you a lot of margin.

**WooCommerce or a plugin-heavy build: VM-2 ($11.99).** 4 GB is the comfortable starting point once you add a cart, payment gateways and a page builder. VM-1.5 ($6.95) is the cheaper compromise if you want a second core for concurrent PHP requests but can live inside 2 GB; it suits a brochure site with a contact form and a booking plugin more than a real store.

**Multiple sites, client work or a membership site: VM-4 ($23.99).** 4 cores and 8 GB let you run several WordPress installs, or one with serious traffic. From here the increments get large: VM-6 doubles cores at the same 8 GB, VM-8 doubles RAM again.

Before jumping a tier, price the add-ons. Extra RAM costs $2/GB per month and an extra vCore costs $3/month, so going from VM-1 to VM-2 as add-ons ($2 RAM + $3 core = $5 plus a storage bump) lands near the $6 difference of the full plan, which also gives you 10 GB more disk. On that step, the plan jump is the better buy. On others the math flips, so check both columns before you commit.

👉 [Order VM-1 at $5.99/mo for a WordPress blog](https://bit.ly/EvoXt)

## Bandwidth, backups and what the bill looks like after month one

Weekly offsite backups are included on every plan, which removes one common WordPress add-on cost. A backup plugin with remote storage typically runs a few dollars a month elsewhere; here it is part of the price, and restores are self-service from the control panel.

The listed renewal price matches the signup price on all the VPS plans, based on plan-tracker data read from Evoxt's own pages in November 2026. That matters more than the entry price: a $5.99 plan that renews at $5.99 is a different product from a $2.99 promo that doubles in year two.

Plan trackers also list a **7-day money-back window on the 11 VPS plans**, available to new customers from the first deployment. The dedicated server plans do not carry that guarantee. Confirm the current terms on the order page before paying, since policies change.

Payment options are credit or debit card, PayPal, and crypto (Bitcoin, Litecoin, Ethereum, USDT on Tron).

If you go over your transfer allowance, extra bandwidth is priced per TB and varies by region: cheapest on standard regions, several times higher on premium locations, highest on Malaysia Premium. For a WordPress site, the practical fix is a caching plugin and image compression long before you buy more transfer.

👉 [Check current pricing and terms before you order](https://bit.ly/EvoXt)

## Promo codes: what you can and cannot rely on

There is a Promotional Code box at checkout, and codes do circulate. The problem is that the widely shared ones contradict each other: the same code gets described as a recurring 40% discount in one place and a 5% discount in another, and none of those claims are confirmed on Evoxt's own pages. Treat any specific percentage you read in a coupon roundup as unverified.

The sane approach: configure your plan on a billing cycle you are happy with at full price, then paste a code into the box and click validate. The discounted total shows before you pay. If the code fails, you have lost nothing but a minute. Do not choose a larger plan than you need on the assumption that a code will bring it into budget.

## When Evoxt is the wrong choice for WordPress

**You want managed WordPress.** Evoxt sells unmanaged VPS. You handle core and plugin updates, PHP versions, server hardening and the database. The one-click app gets you to a working site in minutes; it does not take over maintenance.

**You need fast ticket replies.** Third-party reviews consistently report ticket response times in the 4–8 hour range, with Discord and Telegram moving faster. For a blog, that is fine. For a store losing sales during an outage, build in your own fallback.

**You need a formal SLA.** Nothing in the public plan information describes an uptime guarantee. If procurement requires one, this is not the vendor for that project.

**You need dedicated hardware outside Malaysia.** Evoxt lists dedicated servers from $219/mo, a different budget and a different conversation from a $5.99 VPS.

## A few questions that come up before ordering

**Does Evoxt sell WordPress hosting as a separate product?** No. WordPress runs on a normal VPS, deployed through the one-click app list. You get root access and full control, which is the trade for doing your own maintenance.

**Can I host more than one WordPress site on one VPS?** Yes. Add extra domains in the OpenLiteSpeed panel or run separate installs, but plan memory accordingly: two sites with plugins on 2 GB gets tight, and VM-2 is the more realistic starting point.

**Do I need SSH to install WordPress?** Not to install it. You do need SSH to read the database password on the plain build, or the OpenLiteSpeed admin credentials on the other. If a terminal is foreign to you, budget an hour with a guide before you start.

## Final decision rules

- A single blog with caching: **VM-1, $5.99/mo**.
- Tight budget, one small site, willing to tune: **VM-0.75, $4.99/mo**.
- WooCommerce or a page-builder-heavy site: **VM-2, $11.99/mo**.
- Several sites or client installs: **VM-4, $23.99/mo**.
- Readers in mainland China: Hong Kong on **VM-1**, and watch the 500 GB allowance.

Two things to confirm before you pay: pick the region closest to your actual audience, since moving later means rebuilding, and check that the transfer allowance covers your monthly image and video traffic, not just your page views.

👉 [Compare the plans and deploy your WordPress VM](https://bit.ly/EvoXt)
