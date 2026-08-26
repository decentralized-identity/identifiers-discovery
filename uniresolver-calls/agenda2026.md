# Identifiers & Discovery WG - Special Topic: Universal Resolver 2026

## 9 Sept 2026 - 3PM CEST / 9am EST

## 26 Aug 2026 - 3PM CEST / 9am EST

- ThisDID <> TS Resolver relationship
    - what gets upstreamed, in what order?
    - how review?
- does a DIF service have different IP risk tolerance/requirements than a commercial service?

## interim blotter

- Github Coordination - what would be the best strategy to make it easy for a low-context contributor to land anywhere and understand their options?
    - [d-i/UR](https://github.com/decentralized-identity/universal-resolver)
    - [d-i/DR](https://github.com/decentralized-identity/did-resolver)
        - README.md - link to `./thisdid` as an edge-worker-based implementation using these same drivers, and which supports load-balancing across multiple backends 
    - [d-i/thisdid]([d-i/UR](https://github.com/decentralized-identity/thisdid)
        - README.md 
            - somewhere near the top, link to `./did-resolver` as the place to submit a TS/NPM DRIVER in isolation 
        - CONTRIBUTING.md
            - explain the multiple options:
                1. submit an NPM driver to `/.did-resolver`
                2. submit a PR to https://github.com/decentralized-identity/thisdid/blob/main/wrangler.jsonc#L18-L26 for a LIVE prod subresolver (mention DIF membership/sponsoring org in PR!)
                3. link to [dockerized development instruction](https://github.com/decentralized-identity/universal-resolver/blob/main/docs/driver-development.md) as an option for people who can't/don't want to do NPM or stand up a subresolver
    - does anything need to change anywhere else? any change needed to thisdid.com copy, GoDiddy copy, etc?

## 12 Aug 2026 - 3PM CEST / 9am EST

Proposed Agenda:
- Codewalk of newly-transfered codebase
    - relationship to original [ts uniresolver repo](https://github.com/decentralized-identity/did-resolver)?
        - BF: someone creates a new TS driver using `did-resolver` - how do they operationalize it? can they PR `did-resolver` and/or `thisdid`?
            - thisdid rebuilds periodically - just publishing to npm a conformant, test-passing driver actually gets it deployed live anyways if it's known to `did-resolver` (PR on did-resolver assumes NPM publication anyways, it's just a package.json/submodule PR anyways)
                - `did-resolver` PR still mandatory
            - alternate path: if driver already in npm or in docker-container format, but not known to `did-resolver`, as many "tier 2" (mostly blockchain) methods are, MG can PR them in once he's confident they will work; they could also live outside of DIF github space if they want to maintain it
    - work item status
        - top priority is fine-tuninng the "smart routing", making it more reactive to various corner cases
            - including when resolution fails across multiple providers (because of underlying VDR unavailability or coderot in undermaintained software) - currently just logging this case for future governance process
            - bf: maybe github action checking "most recent commit" or # of commits (maybe excluding dependabot style bots) on driver repo and/or a set of upstream/related repos before autoflagging a driver/method as "unmaintained" 
    - spec reconciliation?
    - 
- Markus: delicacy of not treating the java/docker version as the "old" or deprecated version; having multiple
    - Markus: Important people who land on any of our resolvers know where to donate
    - Markus: Would love help triaging the PRs on the docker repo as well, it's joint work
        - MG: Happy to help!
    - MG: Absolutely, the more the merrier, and resiliency comes from distinct implementations (either of which would resolve show-stopping problems with the other or its deps) - I want this to be strictly complementary, it makes different tradeoffs (and many will still need to use docker for, e.g., non-edge-friendly languages or expensive per-query logic)
    - BF: agree with markus, still maintain both; WASM/npm option can be fast/cheap lane, but still need the flexibility for dockerizable option for some methods; getting people to stand up their own BACKEND (without frontend) is an improvement here
    - BF: gotta make sure we differentiate getting PR merged with "being in the public option resolver"
        - MG: I think agentic stack means lots of people will just stand up lightweight no-frontend JSON-only resolvers live and skip us entirely... people can just proceed directly to subresolver registration 
- joint blog post? Markus + MG: sure!
- Action Items
    - [ ] - Send over Slack to MG summary of what CONTRIBUTING.md 

## ~~29 July~~ 07 AUG 2026 - 3PM CEST / 9am EST

Proposed Agenda:
- banter/ transfer logistics
- Porject intro: `decentralized-identity/did-resolver` re-architected to create thisdid.com (now donated as`decentralized-identity/thisdid`) - new form factor
    - Codewalk of newly-transfered codebase
        - unified edge worker, currently designed for Cloudflare (hono based), but doesn't take much to tweak to Digital Ocean, vercel, etc.
        - TS packages rejiggered to be "vendored" via npm packman
        - Swagger/OpenAPI3 docs --> JSON APIs (but with conneg, can return HTML)
        - analytics are open to end-users; no admin-only stats
        - very JIT: hydrated at query time as workers, which stay dormant until session is destroyed
        - static files in /dist/ dir (CDN-able Durable Objects)
    - next week - more detail on API docs and docs for driver-developers next Wednesday
- codewalk [recording](https://us02web.zoom.us/rec/share/nzi2GYJEjm6GADoB41siURm_OFw51_r9-qTiqkMM5mtq1DYcRQTB_Rkf5QaoxgJW.r2xhaG9xBHRp6RvG)



## 15 July 2026 - 2PM CEST / 8am EST

Proposed Agenda:

- update from Steering Committee?
- update from I&D WG-- Adopt [thisdid.com routes](https://thisdid.com/docs) and subresolver architecture?
    - new major version of UR or new spec?

Minutes:

- update from Steering Committee - not consensus yet but almost there to point URL to thisdid.com
- update from I&D WG-- Adopt [thisdid.com routes](https://thisdid.com/docs) and subresolver architecture?
    - plan for new repo
        - MG will transfer soon
        - issue template and PR template (more realistic for agentic codegen) - "the agent will understand the github actions" (to do unit testing, vector runs, etc all happen BEFORE first human reviews)
        - miracle of TS: can run not just frontend but also the BACKEND (for many drivers) in browser, in service worker, even as a service (NPX-style?) 
    - new major version of UR or new spec?
        - explore micropayment approach? frontend gets a percentage (i.e. DIF could get a tiny income stream!)
        - rebuild more drivers in TS? MG: I could do one every month or two, there are only 20 that actually get used much left to redo in TS


## 1 July 2026 - 2PM CEST / 8am EST

Proposed Agenda:

- Algorand is working on privacy-preserving query/resolution stuff; demo/announcement?
- Update on MG's proposal to use TS resolver for new load-balancing/sub-resolving DIF instance
    - thisDID.com is already running a lot of custom code that can be upstreamed to do this load-balancing part, so won't take too long to build if resolvers are interested in dividing up the "free tier" traffic coming from the DIF instance
    - detailed "what you need to add" pitch to current implementers (to become "subresolvers" from a future load-balancing DIF instance)
- From the TSC: what's the security model for redirecting? What if a less-secure fourth sub-resolver signs up and starts doing something sneaky (does the user meaningfully consent by clicking a link, or does the DID doc just come back while still at a DIF URL?)
    - KISS: what if every 24 hours, the resolver just pinged each subresolver with the "test DID" and the subresolvers didn't need to update anything?
    - KISimplerStill: does the metaresolver even need to validate DIDs or track which resolvers resolve which DIDs?

Minutes:

- [exciting demo](thisdid.com)
    - temporarily no rate-limiting, so load-test away!
    - just to confirm: no changes required!
        - non-rate-limited token would be good, would make reputation/metrics more accurate; currently everyone's  
- ideating
    - MG: [sub]resolvers could also do outsourced verification (i.e. here's a DID, here's a payload/JWT/etc, does the signature prove against the current/live doc) - outsourced/SaaS verification could be 
        - not a lot of precedent, just platforms like Kilt; Credo had something similar, but only worked for their own DID methods; usable Universal Verifier API -- there are lots of SaaS possibilities here!
    - bf: what about interactive usecases? mg: that's actually out of scope, x401 and mpp are more stateless, document-validity and proofing is all that matters (ERC-8004 as well; none of the three are really interactive or protocol-based, it's all OOB and submitted as a complete package; general tendency here seems to be that the more decentralized topologies are sidestepping interactive signature/protocol)
- Bifold Wallet has been forked and whitelabeled to create an agentic client platform called "", which has DID and VC built in
- Rulesets
    - priorities requested at time of registration by each subresolver
    - other than/after applying the rules, load-balancing actually done by mS response per subresolver/method pair (i.e., if a resolver's uptime or response time lags over time, it'll get deranked in the load-balancing)
- future work
    - a specific (non-rate limited) token for each subresolver would allow
        - better analytics on their side
- Approval? ongoing maintenance? replace existing one?
    - MG: I'm happy to be responsible for maintenance of the DIF version once it goes live, and can promise very low server bills
        - willing to maintain as a DIF-governed repo/work item
    - cutover pretty easy: just point the DNS, no front-end server, will be logged separately as a DIF-originating request
    - 
    - analytics on thisdid.com use the same [custom] engine that is used on the [x402 site](https://facilitator.goplausible.xyz/dashboard) - allpublic, all free already
        - 

## 17 June 2026

- DID privacy <> ZKP
    - algorand launching some stuff
    - ethr background
- Report on Ankur's first-stab at cheaper AWS and domain-name details?
- Discuss MG's proposals for:
    - a different basic internal architecture [better suited to a cheaper CF-hosted version]
    - an extension for "subresolver" discovery/routing, and 
    - possible API changes (as a new work item, or as a reboot of the TS version)
        - maybe static/buildtime/github registry + load-balancing (send every third request to one of the three, for example) + live failover if endpoints down or whole resolvers down
        - automatable testing after self-registration/enrolment to be a subresolver in the mix/load-balance
    - TS drivers made from the existing docker-compose drivers? are some easier/faster to unwrap/rewrap?
        - stackrank most high-value ones and start there?
        - christian: ongoing driver maintenance; make sure someone is willing to own maintenance before making a v1 for them
        - good docs more important than doing many of them

## 3 June 2026

- Agenda:
    - Updates
        - Ankur: quick read of AWS & CF dashboards?
            - high level: 94% memory at peak, 10% compute; reconfig to diff instance (mem-optimized profile)
            - ankur: just switching which instance type would save 300/mo, ballpark?
            - christian: the memory is brutal, each driver i run (on my instance of the java codebase) adds another 2 or 3%, 80% with 0 traffic just to run them
            - markus: most of the drivers aren't in java, fwiw, they're dockerized versions of whatever people's things do in whatever language they're already in
            - ankur: other optimizations: we're also paying on-demand pricing instead of commiting monthly
            - ankur: kim added CloudWatch and never turned it off; it has 144 metrics which we're retaining forever and not looking at!
            - MG: just switch to CF altogether? way cheaper in my experiments; ankur: well yeah, now that they support docker...
            - Ankur: These optimizations make sense? Who decides?
            - BF: DIF can approve all this, it seems all worth trying (if you're volunteering to take a stab, and rollback whatever breaks)
    - MG Proposal
        - ![image](https://hackmd.io/_uploads/BklalkCgGe.png)
        - Thinking longer term: PoH extension point? ZTAuth?
        - BF: Seems good to experiment with; maybe do it on a fork, and/or of the TS version?
    - Concrete proposals:
        - Ankur: domain options?
            1. dev.uniresolver.io can redirect to resolver.identity.foundation OR
            2. dev.uniresolver.io can delegate DNS (and caching) to DIF's CF to have uniform stats OR
            3. dev.uniresolver.io can just redirect to 
            * Decide before next meeting?
        - TS[/WASM?] version 
            * how much work to be equivalent?
            * could driver-authors choose to write for either and say they've "written a driver" for DID Methods WG purposes?
        - Router/Subrouter- how does resolver.i.f know WHICH resolvers to recommend/route for a given method, at runtime?
            * could live resolvers self-attest what drivers they are currently running? mapping on github? etc?
        - Actual Target State: 
            * resolver.identity.foundation --> ?
            * uniresolver.io --> Danube's GoDiddy
- Action Items:
    + [ ] Ankur will take a crack at some AWS optimizations discussed today to triage billing pain, reverse anything that breaks or is more complicated than expected.
    + [ ] Markus to consider domain/DNS/redirect options, followup with Ankur if needed
    + [ ] BF will move the meeting in two weeks to an earlier time to stop colliding with TSC (emoji poll in the thread on this message)

### Analysis of AWS & Cloudflare dashboards (3 June)

#### Cloudflare
- **Short-term**
    - **No traffic stats for the resolver**
      - Most records are not proxied behind Cloudflare, hence there's no data.
      - **Resolution:** Turn on proxying via Cloudflare, check if anything breaks, start collecting traffic stats.
      - **Catch:** DIF's Cloudflare only has records for resolver.identity.foundation.
          - Proxying ideally needs doing on dev.uniresolver.io's DNS records too, otherwise there's a gap in the data.
          - Alternative: 301 redirect dev.uniresolver.io → resolver.identity.foundation, perhaps with a "hosted by GoDiddy" or similar shoutout? What would be acceptable here?
    - **No rate limiting set**
      - No security and rate limiting (WAF) rules set.
      - **Resolution:** Pre-requisite is to have proxying turned on. After that, turn on basic best-practice WAF rules and rate-limiting rules (catches pest traffic without throttling legitimate high-volume callers).
- **Medium/long-term**
    - **Supporting multiple backends for a resolver**
        - Can do load balancing at Cloudflare, without having to drop traffic into a specific AWS account
        - E.g., User/API call hits Cloudflare, then load balanced to one of many different backends

**AWS**
Spend ~$1,066/month and rising (Mar/Apr/May: $889 / $1,052 / $1,066), ~$12.8k/year. Runs as an EKS cluster (`dif-universal-resolver-prod`) in us-east-2.

- **Compute is on the wrong instance type (biggest cost)**
  - 6 × c6a.xlarge on-demand ≈ $683/mo (~65% of bill). CPU runs only ~11%, but memory is the real constraint (per-node peaks 52-94%). c6a is compute-optimised; the Java/Docker driver workload is memory-bound, so we're paying for vCPU we never use.
  - **Resolution:** Switch the node group to general-purpose/memory-optimised, e.g. 3 × m6a.xlarge (same 48 GB RAM, half the vCPU, one per AZ) or 4 × r6a.large. ~$305/mo saving. Validate peak memory concurrency before consolidating.
- **No Savings Plan (everything on-demand)**
  - Nodes have run 24/7 since March at full on-demand rates.
  - **Resolution:** After right-sizing, buy a 1-year no-upfront Compute Savings Plan (~28-30% off, fully flexible). ~$80/mo.
- **CloudWatch is the hidden #2 cost (~$160/mo)**
  - ~$132/mo of custom metrics (~440 of them) plus ~$27/mo log ingestion/storage.
  - **Resolution:** Keep only metrics that feed a dashboard or alarm, bin the rest; lower prod log level and set ~14-day retention. ~$115/mo.
- **Worker nodes are publicly addressable (cost + security)**
  - 11 public IPv4 addresses billed; only 4 are the Elastic IPs visible in console (3 × ALB, 1 × NAT, both legitimate). The other 7 are auto-assigned to the 6 nodes + utility box, which sit in public subnets and are internet-routable.
  - **Resolution:** Move the node group to private subnets (ingress via ALB, egress via NAT; `MapPublicIpOnLaunch=false`). Removes ~7 IPs (~$25/mo) and takes nodes off the public internet. Use SSM Session Manager instead of a public bastion.
- **Minor (not worth chasing now)**
  - Cross-AZ data transfer ~$38/mo, NAT Gateway ~$33/mo, gp3 EBS ~$10/mo. Largely inherent to multi-AZ HA; fewer nodes trims the cross-AZ chatter.

**Bottom line:** ~half the bill (~$530/mo) is recoverable on the existing stack with no migration and no architecture rewrite. That reframes the "move off AWS?" question as "do we want to go lower?" rather than "we're bleeding and must flee".

---
#### Appendix: supporting data

**May 2026 cost breakdown**

| Item | $/mo |
|---|---|
| EC2 compute (6 × c6a.xlarge) | 683 |
| CloudWatch custom metrics | 132 |
| EKS control plane | 74 |
| Public IPv4 (11 addresses) | 41 |
| Cross-AZ data transfer | 38 |
| NAT Gateway (hours) | 33 |
| CloudWatch logs (ingest + store) | 27 |
| Load balancer (ALB) | 17 |
| EBS (gp3) | 10 |
| t3.micro | 8 |
| Route 53 + misc | ~3 |
| **Total** | **~1,066** |

**Node utilisation (May; each node = 4 vCPU / 8 GB)**

| Node | CPU avg | CPU peak | Mem avg | Mem peak |
|---|---|---|---|---|
| i-014c | 26% | 43% | 38% | 52% |
| i-0909 | 17% | 57% | 46% | 81% |
| i-0e97 | 16% | 27% | 30% | 40% |
| i-0972 | 3% | 7% | 36% | 42% |
| i-05b3 | 2% | 16% | 35% | 55% |
| i-03ba | 2% | 8% | 43% | 94% |

Aggregate ~11% CPU, ~38% memory. CPU is hugely over-provisioned; memory is the binding constraint and trending up. Note the idle-CPU nodes still hold 35-94% memory, so they cannot simply be removed.

**Public IPv4 (11 total, $0.005/hr each)**
- 4 Elastic IPs (shown in console): 3 × ALB, 1 × NAT Gateway. Keep.
- 7 auto-assigned (not shown on EIP page): 6 × worker node + 1 × t3.micro. Removable via private subnets.

**Implementation notes**
- Cloudflare proxying: CF proxy has a ~100s origin timeout (524 errors) and only proxies HTTP/S on standard ports. Flip records one at a time in case slow blockchain drivers trip it.
- AWS node-group reshape: do it the EKS way (right-size pod memory requests → new node group → drain and delete old), and confirm the 81%/94% memory peaks aren't simultaneous (5-min granularity) before consolidating to fewer nodes.

## 20 May 2026
 
- First meeting of DIF Universal Resolver Instance Rescue Club
- Agenda: 
    - Problem space (10min)
        - Uniresolver as work item - who is reviewing new drivers? How are they paid or recognized for that labor?
            - WG members "swapping" review?
            - Ongoing champion, if Bernhard (DanubeTech) steps down as work item lead?
        - Uniresolver as deployment - Move from AWS to something cheaper? 
        - Rising traffic costs - how triage over time? Distinct rate-limiting/DevOps/traffic-analysis function 
    - Possible Futures (40min)
        - Short-term - trial outtage?
        - Redirect traffic to DID Members, whether the site is up or not!
            - Uniresolver forks - VidOS, MyDID, and GoDiddy
            - are there other tools like the [OYD Linter](https://github.com/decentralized-identity/universal-resolver/issues/330#issuecomment-1357375237) that we should be pointing to as well?
            - matrix of driver coverage?
            - Total surface of redirect: 404 messages, outage messages, rate-limiting messages
                - can someone show me in the code where all these error pages live for me to PR something in? searching in github didn't make the error handling self-evident to a non-Java reader!
        - "Universal Router" option - don't resolve DIDs, just show other sites that resolve them

### Minutes

- Problem space (10min)
    - Uniresolver as work item - who is [reviewing new drivers](https://github.com/decentralized-identity/universal-resolver/pulse?period=monthly)? How are they paid or recognized for that labor?
        - One of DIF's first work items!
        - WG members "swapping" review? Structured swap?
        - Ongoing champion, if Bernhard (DanubeTech) steps down as work item lead?
        - Markus: Invoicing gets messy quickly, unfair to other WGs
    - Uniresolver as deployment - Move from AWS to something cheaper? 
    - Rising traffic costs - how triage over time? Distinct rate-limiting/DevOps/traffic-analysis function 
- Possible Futures (40min)
    - Short-term - trial outtage?
        - Christoph (OYD): I used it in research; SEO is hard-won, maturity is hard-won, sends a terrible signal about DIDs to shut it down
            - Cost reduction moving off AWS? 
    - Redirect traffic to DID Members, whether the site is up or not!
        - Uniresolver forks - [VidOS](https://vidos.id/products/vidos-universal-resolver), [ThisDID](thisdid.com), [archon](resolver.archon.technology), and [GoDiddy](https://godiddy.com/)
            - corner-case: include single-method resolvers like the [did:ebsi resolver](https://hub.ebsi.eu/tools/did-resolver)
        - are there other tools like the [OYD Linter](https://github.com/decentralized-identity/universal-resolver/issues/330#issuecomment-1357375237) that we should be pointing to as well?
        - matrix of driver coverage?
        - Total surface of redirect: 404 messages, outage messages, rate-limiting messages
            - can someone show me in the code where all these error pages live for me to PR something in? searching in github didn't make the error handling self-evident to a non-Java reader!
        - Grace: That's a better Press Release/announcement - maturity/graduation narrative
            - Christoph: Sure, within DID community, but outside, this still looks like "experimental" or pre-market technology to some
    - "Universal Router" option - don't resolve DIDs, just show other sites that resolve them
        - Tim: Letting us 3 volunteers decide which DIDs we want to resolve is great, but you will want to balance that against keeping it accessible so that people can 
        - Tim: Importantly, we don't want to rate-limit this too much, since we want to showcase our enterprise-grade/SaaS product... 
        - Tim: Analytics; should rate limit trigger/nudge towards a named API token? Is the rate limit across all callers and all subproviders? Per IP? etc?
            - MG: you don't know you're being DDos'd or bot-armied or authentically trafficked if you have no analytics...
    - Christoph: I would argue keeping uniresolver up at current domain is important, would want to explore ways to do that, even if i/OYD has to run it
    - MG: I've been running, in addition thisDID.com, a self-updated ref-impl instance
        - One barrier to both contribution and cheaper operation is Java; switching to a language that can run on edge might make it much cheaper; cloud-edge is WASM-only these days... Java is one of the only langauges you can't build to WASM as a target?
            - Markus: drivers are docker images, so drivers can be in any language (and not really feasible for edge-cloud)
            - Markus: making a version of the uniresolver in another language would be a great work item of IDWG - there's already a TS version [underway](https://github.com/decentralized-identity/did-resolver)
            - MG: Docker-based architecture is kind of inefficient and redundant; "Edge Services" [microservice] cloud offerings make this (e.g. CloudFlare sandboxes as durable objects that hibernate until called)
        - Hosting - what if we replaced at the current URL the full Uniresolver  with a "load balancer" that sends DIDs for resolution to all of our sites? 
            - Markus: Sure, that's something we could do, we discussed it previously but 
                - MG: Capabilities metadata (i.e. list of did methods supported) in handshake between querier and resolver (getting more common with agentic dev) - add that to the spec so it can happen at runtime?
                - MG: costs get shared across subresolvers; load balancer would be trivial to pay for
    - DDoS problem and cost-monitoring
        - BF: Vaguely remember quick-and-dirty, "try and see if we need to do more" rate-limiting 18months ago...
            - Tim: Free version of Shield; this isn't DDoS properly speaking, though, this is more like pest traffic
        - Captcha or PoPhood?
        - Ankur: What would be a more appropriate strategy if the problem is pests?
            - Tim: Good Load-balancing and caching is probably enough
    - Is cost the urgency?
        - Tim: AWS usually throws credits at OS projects, non?
        - Markus: Uniresolver and Uniregistrar are both on sponsored FOSS programs on DockerHub - renewed every 6 months
        - BF: Port existing Uniresolver to OVH/Hetzner and simple per-IP ratelimiting might get us a lot of the way to lower bills, might be the fastest fix if all we care about is the bill?
- Next Steps?
    - BF: Who can do this kind of stuff soonish?
        - MG: I'm down, but want a DIF direction/decision beforehand
        - MG: longer-term solution is probably to rearchitect and go microservicey/WASMy with the drivers... only 3 or 5 methods were ever written for the TS version linked above!
            - Markus: sure, but very few did methods would do this (less universal)
        - Ankur: one idea that came up in TSC was just combining regression testing and dockerization so that any time a docker starts failing more than X tests, it just spins down and makes the deployment cheaper; i've been playing with it in Codex; might not be a huge cost-saver, but...
            - Markus: There's something like that in github actions, not sure it still works, tho? I think the W3C DID test suite and DID-linked service (from Christoph); someone just has to look at these
    - 1June is less than 2 weeks 
