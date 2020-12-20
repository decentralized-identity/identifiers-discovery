# DIF Identifiers & Discovery WG – Rolling Agenda & Minutes

[![hackmd-github-sync-badge](https://hackmd.io/b-x6jEpMSOm5HiILrkC1oA/badge)](https://hackmd.io/b-x6jEpMSOm5HiILrkC1oA)




[**WG projects** ](https://github.com/search?p=2&q=topic%3Awg-id+org%3Adecentralized-identity+fork%3Atrue&type=Repositories) | [ DIF page ](https://identity.foundation/working-groups/identifiers-discovery.html) | [Mailing list and Wiki ](https://lists.identity.foundation/g/id-wg) 

_For this call, you are encouraged to turn your video on. This is a good way to build rapport given we are a large, disparate group experiencing a lot of churn._

_This document is live-edited DURING each call, or shortly after the call, and stable/authoritative copies live on our github repo under /agenda.md . 
Please note that we might not notice a pullrequest in time, but you are free to propose agenda items for future meetings via hackmd._

<details>
<summary> Meeting information </summary>

* Before your contribute - [**join DIF**](https://identity.foundation/join) and [sign the WG charter](https://bit.ly/DIF-WG-select1) (both are required!) 
* Time: Every Monday, 14:00-15:00 ET
* [Calendar entry](https://calendar.google.com/event?action=TEMPLATE&tmeid=OWtzNWZuanA4bWRnYmF0ZnVxaDR0MnQ2cGVfMjAyMDA5MjFUMTgwMDAwWiBkZWNlbnRyYWxpemVkLmlkZW50aXR5QG0&tmsrc=decentralized.identity%40gmail.com&scp=ALL)
* [Zoom room](https://us02web.zoom.us/j/81145177291?pwd=NElWUEYycm4xdjAvcXhGS0V4aHNNdz09), Meeting ID: 811 4517 7291, 
Password: 387317
</details>

 

#### Future topics: 

<details>
<summary> Topics for upcoming meetings</summary>

* topic 1 (to be discussed on this date) 
* topic 2 (to be discussed on this date)
* topic n. (tbd)

</details>

## Meeting - 21 Dec 2020 - (1400 ET)
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization
4. Process for creating new repos / work items
5. Review of 2020 and plans for 2021

### Attendees
* ...

## Meeting - 14 Dec 2020 - (1400 ET) [recording](https://us02web.zoom.us/rec/share/zzlMoqr-B1gvugiMA3-zvcj68B-e9ll_AZKb_9ChbiWIEsO3ZjnVBeZGXpH9hQmT.1kjaI3SGgSR0NxzK)
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization
4. New implementations
   * **[Tomislav Markovski/Trinsic]** Rust implementation of did:key
       * Worked on DIDComm extensions, but separated them out to independent component
       * Initial keys: Those supported by DIDComm (Ed25519, P256)
       * did:key is very flexible to work with, not anchored, self-certifying, uses multicodec
       * Rust is good for native libraries that you can call from other platforms
       * No FFI layer yet, but it would be easy to expose if anyone wants to consume it
       * Functions: Resolve, generate, generate from seed, sign, verify, create DID document (currently supports JSON-LD but should also support plain JSON)
       * https://github.com/trinsic-id/did-key.rs
   * **[Juan Blanco/Nethereum, Veikko Eeva]** Planned .Net implementation work
       * Created a .Net implementation of Ethereum
       * Have followed DIDs but they are still work-in-progress
       * Have looked at Java and JavaScript implementations, there is still a lot to do
       * Joined DIF and are looking to collaborate with other people to get the ball rolling with a .Net implementation of DIDs
       * https://github.com/veikkoeeva/DotDecentralized/tree/main/src/DotDecentralized.Core
   * **[Alen Horvat/Aceblock]** Universal services
       * High level of universality and independence of underlying technologies is important, to avoid vendor lock-in
       * Universal Services: Standardize the way to interact with and access SSI services
       * Use DID Auth, REST endpoints for read, JSON-RPC endpoints for write
       * Read operations are standardized (Universal Resolver)
       * CUD operations are more complex; e.g. the service can return an unsigned payload, plus a request for signature
       * The solution is standardized arguments 
       * The Universal Resolver currently is very heavy (lots of Docker containers); instead, it could call out to remotely hosted resolvers
       * There is need for a trust list of DID method endpoints; DIF could play a role here
   * **[Joel Thorstensson/3Box]** DID implementation in JavaScript
       * Introduced js-did library, based on EIP2844
       * Functions: did_authenticate, did_createJWS, did_decryptJWE
       * Support for ed25519, secp256k1, 3id
       * js-did library uses https://github.com/decentralized-identity/did-resolver
       * Also methods for dag-jose
       * Runs in any JavaScript environment (client, server)

### Attendees
* Markus Sabadello
* Juan Blanco
* Alen Horvat
* Charles Cunningham
* Daniel Buchner
* Dmitri Zagidulin
* Joel Thorstensson
* Juan Caballero
* Maarten Boender
* Samuel Smith
* Tom Jones
* Tomislav Markovski
* Veikko Eeva

## Meeting - 07 Dec 2020 - (1400 ET) [recording](https://us02web.zoom.us/rec/share/iSfQWY8wFde7nkHLCfwkBiInSNf3y5F0xRWnm-maiAwM9-9SzibpGA2S6t6mpgwa.Fig4sivvsP8Jj8_2)
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization
4. Admin: Set up WG team members on Github: https://github.com/orgs/decentralized-identity/teams/id-wg
    * See list of repos: https://github.com/orgs/decentralized-identity/teams/id-wg/repositories
5. Key roll-over and recovery
    * We should create a repo in the ID WG that lists recovery methods we know about.
    * Microsoft/DanielB have been working on Fuzzy Encryption: https://github.com/decentralized-identity/fuzzy-encryption
    * For the [Confidential Storage (CS) WG](https://github.com/decentralized-identity/confidential-storage), key recovery is pretty much out of scope. You can store private keys in a CS, but you still need a master key to unlock the CS, so there's a chicken and egg problem.
    * There is essentially only a limited set of options (menmonic devices, secret sharing). Usability is the main issue; we need a critical mass of people working on it, to make the user experience accessible.
    * Biometrics must not be used as a primary private key ("you can't rotate biometrics"). Biometrics can be used to unlock a private key, i.e. as an authorization capability.
    * Additional topic: How can keys be recovered when you are not capable of controlling them anymore, or after your death?
6. Topics seen in Slack channel:
    * Universal Wallet Conceptual Clarifications - https://github.com/w3c-ccg/universal-wallet-interop-spec/issues/46
    * Universal Registrar problem: https://github.com/decentralized-identity/universal-registrar/issues/18

### Attendees
* Markus Sabadello
* Daniel Buchner
* Samuel Smith
* Charles Cunningham
* Dmitri Zagidulin
* Ivan Casillas
* Juan Caballero
* Orie Steele
* Scott Mallery
* Tom Jones
* Padungkiat Tamasee

## Meeting - 30 Nov 2020 - (1400 ET) [recording](https://us02web.zoom.us/rec/share/XObP9jPhKL--j-7XlCuVeaAmpNJ9Ky-abUN9xbJ8wkqBlF77PJE9oYON28iqQbLN.pApDPAP50qLUlCKo)
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization
4. Discussion of Method Spec Registry analytics and some possible directions for DIF-based efforts to structure DID Method comparison/review (Juan)
    *  What's the current process for getting a DID method added to the [W3C DID spec registries](https://w3c.github.io/did-spec-registries/#did-methods)? What's the governance process?
    *  Orie explained that the editors check if the link works, and if the DID method spec contains the required sections.
    *  All methods are currently marked either "provisional" or "deprecated". 
    *  Maybe methods that don't fulfill the current requirements should be marked somehow (but this could be politically sensitive).
    *  Some methods were created before there even was a registry.
    *  Markus has worked on a graph that shows DID methods added over time.
    *  Sam suggested to do analytics of DID method usage.
    *  Potentially access logs of the Universal Resolver can be analyzed (but it doesn't have any built-in analytics).
    *  What's the current governance process for adding a driver to the DIF Universal Resolver?
    *  There is a [page](https://github.com/decentralized-identity/universal-resolver/blob/master/docs/driver-development.md) that describes requirements, but the process can definitely be improved, e.g. by automatically testing drivers.
    *  How can method spec authors and/or resolver driver implementers be contacted if their DID method (implementation) is outdated or doesn't work?
    *  Sophie suggested that authors/implementers should be asked to supply contact information (rather than trying to find them by their Github handle).
5. Discussion around accessibility/usability of DID technology
    * Eric noted that after taking a break from participating in the DID community, it felt hard to get back to the topic and find the inside knowledge that's required to use DIDs.
    * Many DID methods seem to be "dead", and some method specifications have "TBD" sections. Therefore people may stay away from DIDs.
    * Some DID methods are designed to be easy to use without a need for advanced infrastructure (e.g. did:web, did:key).
    * Sam explained that one objective of KERI is replace many DID methods with a single DID method.
    * Sophie agreed that it was hard to find things, there are too many documents and some broken links.
    * Eric suggested it would be good to have third-party journalistic review of DID methods.
6. Short process-related discussion about recent DID Core spec proposal related to canonical/equivalent IDs.

### Attendees
* Markus Sabadello
* Charles Cunningham
* Juan Caballero
* Orie Steele
* Samuel Smith
* Sophie [Unikname]
* Tom Jones
* Alex Varabei
* John Callahan
* Jose San Juan
* Keith Smith
* Tobias Looker
* Eric Welton

## Meeting - 23 Nov 2020 - (1400 ET) [recording](https://us02web.zoom.us/rec/share/K_AYd9_MpoBIbXUXq6TxwvkH2_-edUlzf22WDrJ0nn2_4Rv5O0Ok6Q6MBnUVoLE0.qoT43iXVZBPxkk4V)
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization
4. Questions around DID deactivation and resolution metadata
    * Can you verify a credential that was signed by a DID that has been deactivated?
    * Yes you can look up older versions of a DID document using the `version_id` and `version_time` parameters.
    * But support for those parameters, as well as support for deactivating DIDs, is method-specific and optional.
    * Support for looking up old DID document may be infeasible, considering the expected amount of DIDs, if you have to keep a copy of everything.
    * Sidetree has a "checkpoint" feature that deletes old history at some point.
5. MIME types of DID documents
    * Is it legal to have multiple `+` symbols like in `application/did+ld+json`? See discussion here: https://github.com/w3c/did-core/issues/208
6. Update on issues with WebID: https://tcwiki.azurewebsites.net/index.php?title=Authentication_UX
    * WebID came up at BlinkOn (a browser conference), slides: https://docs.google.com/presentation/d/1rOIKWSrL8acz-rl8PRHmPvS5f6fOl7-tQwByT6O595A/
    * We (DIF) should work web WebID to get DID support into browsers.
    * This is an opportunity to get smooth and "in context" support for having a direct connection to the wallet (sending requests and responses).
    * Can WebAuthn be used for this? It offers a direct connection from a browser to a trusted wallet.

### Attendees
* Markus Sabadello
* Tom Jones
* Sam Smith
* Juan Caballero
* Charles Cunningham
* Daniel Buchner

## Meeting - 16 Nov 2020 - (1400 ET) [recording](https://us02web.zoom.us/rec/share/D0m7Zk6UjriFJ9wxh5FM_yIG6GfHSEi1rgVVv-lViyFXjPa7XCC0tCP512D8Vz1v.cYtgFmIhkpYrfl7q)
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization
4. [Sam] Collect use cases for KERI
   * Time: the hour before the developer meeting
   * Send use cases to Sam or Juan
5. Status of the DID rubric PR that adds security and privacy criteria:
   * https://github.com/w3c/did-rubric/pull/11
6. [Markus] Open PRs in DID Core about the abstract data model and reprsentations:
   * https://github.com/w3c/did-core/pull/455
   * https://github.com/w3c/did-core/pull/454
7. How will the Universal Resolver support different representations?
   * It should delegate as much as possible to its drivers.
   * The Universal Resolver can also "convert" between representations, but should indicate that it did this, and a client should be able to control this behavior via input metadata properties.
   * Need to define how the "Accept" header works in the HTTP(S) binding.
   * Should the "default behavior" be to return a DID document, or a DID resolution result (which includes the DID document plus metadata).
   * Need to update the Universal Resolver [driver development documentation](https://github.com/decentralized-identity/universal-resolver/blob/master/docs/driver-development.md), as well as the [DID Resolution spec](https://w3c-ccg.github.io/did-resolution/).
8. [Orie, Sam] Any progress on KERI test vectors? Things are still changing too much.
9. Updates on current work items
	did:peer, KERI, Universal Resolver, .well-known DID configuration, DID
	parameters, secret recovery mechanisms

### Proposals
-proposals here-

### Attendees
* Markus Sabadello
* Tom Jones
* Charles Cunningham
* Juan Caballero
* Samuel Smith
* Rory Martin
* Orie Steele

## Meeting - 09 Nov 2020 - (1400 ET) [recording](https://us02web.zoom.us/rec/share/kupVdGlwe30wjuPFmHBfUG_toosS9Hv-2rl1pReIMWVrODDkJATa7MErNGk0FoQD.J2Ho-Tz_5ZYq3n8D)
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization
4. [All] Review of DID WG meetings during TPAC - https://docs.google.com/presentation/d/1RoE8E4y8S1j65EJaXZ8oihkduNbjTXXvdwtkzw961Xw/
    * Discussed privacy violating properties, following "type" topic in DID WG meeting
    * Talked about GDPR right to erasure. A better idea might be a "right to remove correlation".
    * Regarding the Abstract Data Model (ADM): Representation-foreign properties could be hidden in a "special" place.
    * There will be language that describes how to add and register new representations.
    * Work on "security" and "privacy" in DID Rubric: https://github.com/w3c/did-rubric/pull/10
5. Updates on current work items
	did:peer, KERI, Universal Resolver, .well-known DID configuration, DID
	parameters, secret recovery mechanisms

### Proposals
-proposals here-

### Attendees
* Markus Sabadello
* Samuel Smith
* Tom Jones
* Juan Caballero

## Meeting - 02 Nov 2020 - (1400 ET) [recording](https://us02web.zoom.us/rec/share/neXv2MQy0QT2MxWZlyH2cpEMjbkVrzvdnt954FX4Pl2xFHv4aBMqfgdSWq1ADB0Q.05IoQNTXYSCNBOQ1) 
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization  
    Polyfill Buchner  
    
    Goto WebID working group and express concerns about no conrol over identifiers: https://github.com/WICG/WebID https://wicg.github.io/WebID/README.html 
    
      
4. [Sam, all] Updates on various topics  
    Fuzzy vault updated looking for review feedback joint work on fuzzy vault
    Python version is done for evaluation but may not be supported in future.
    C++ coming up in 2 weeks will have long term support
    Microsoft DID configuration spec. Well-known DID support. For parse and read.
    KERI demo'd direct mode at IIW. Target to finish KERI core by end of year.
    Jolocom app and wallet demo
    ReSpec vs. SpecUp for standards writing. DIF will end supporting both. 
    SpecUp: SideTree, DIDComm, Presentation Exchange  DIF standards
    ReSpec: W3C  DID and VC specs
    ToIP: Having a discussion about which one to use.
    
5. Updates on current work items
	did:peer, KERI, Universal Resolver, .well-known DID configuration, DID
	parameters, secret recovery mechanisms

### Proposals
-proposals here-

### Attendees
* Samuel Smith
* Tom Jones
* Steve Todd
* Charles Cunningham
* Daniel Buchner
* Juan Caballero (partial)
* Kaliya Young (partial) 

## Meeting - 26 Oct 2020 - (1400 ET) [recording](https://us02web.zoom.us/rec/share/qYfm_yeJKE7bxx1ikeNllphHHPETk3mjZzo4UmMpg9ZaE0Pjejica0s6RMgafV-l.T9YvAAGgWMe_NCr2) 
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization
4. [Markus] I&D WG resources and work items: [Website](https://identity.foundation/working-groups/identifiers-discovery.html), [Github](https://github.com/decentralized-identity/identifiers-discovery/), [Notion](https://www.notion.so/dif/Identifiers-Discovery-Working-Group-aea2c07cc10d4f45b729b633691e364e)
5. [All] Impressions from Internet Identity Workshop #31
6. From IIW: did:indy https://hackmd.io/@icZC4epNSnqBbYE0hJYseA/S1eUS2BQw
    - What does the namespace look like? E.g. did:indy:897347:2498237498374982374
    - Is the "controller" the wallet?
7. Websites and browser
    - How would a website know what to ask for, e.g. in OIDC SIOP? 
    - The website wants the user's identity, how does that connect to the controller?
    - What does the website send to the browser to initiate the process?
    - The user would send an identifier plus a proof of authority..
    - What should be our next steps regarding WebID? (see notes from last week)
    - At IIW there were sessions about WebID and its relation to CHAPI and SIOP
    - CHAPI is a "dumb pipe" that can be used for sending get() and store() requests. Wallets are registered via a polyfill (uses localStorage). There are some privacy/confidentiality/usability issues with polyfill.
    - Volunteers to collaborate on a statement from DIF about WebID?
7. [Daniel] Implementation updates
    - Implementing .well-known now, wallets that will connect to it by the end of the year
    - Python implementation of Fuzzy Vault is available now: https://github.com/decentralized-identity/fuzzy-encryption/tree/master/src/python
    - Implementing WASM bundle now in ~2 months, then publish a blog post?
8. [Wayne] From IIW: Opt-in discovery rather than passive discovery by Daniel Hardman
9. [Markus and all] Current topics in DID Core spec
    - DID document representations: https://drive.google.com/file/d/1KHw7QfGBbJrr4okIdxDbDRhHJHJJLmzE/, also see various issues and PRs on DID WG Github repos.
    - 'type' property: https://github.com/w3c/did-core/pull/410
    - W3C TPAC meeting is happening now
    - [Sam] Differentiate between "privacy" and "confidentiality". Privacy is one-way; confidentiality can be preserved long-term. Trilemma: Authenticity/privacy/confidentiality.
10. [Tom] Security of keys in a wallet, is this covered by the DID Core spec?
11. Updates on current work items
	did:peer, KERI, Universal Resolver, .well-known DID configuration, DID
	parameters, secret recovery mechanisms

### Proposals
-proposals here-

### Attendees
- Samuel Smith
- Markus Sabadello
- Daniel Buchner
- Charles Cunningham
- Dmitri Zagidulin
- Juan Caballero
- Maarten Boender
- Orie Steele
- Tom Jones
- Wayne Chang

## Meeting - 19 Oct 2020 - (1400 ET) [recording](https://us02web.zoom.us/rec/share/YeOQcUDNUweNouX6TemFh6Qkt8or2ZGhYC5HifRNtjrAKbAVd2xwr4iOQ3tCi_m4.xzWnVsSXUY_u2pUX) 
 
### Agenda

1. Welcome and introductions
2. [ID WG participation tracking](https://docs.google.com/spreadsheets/u/1/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=1245330243)
3. Agenda creation/review/prioritization
4. Meeting minutes on Github
https://github.com/decentralized-identity/identifiers-discovery
e.g. see SDS https://github.com/decentralized-identity/secure-data-store/blob/master/agenda.md
5. [All] IIW this week!
    * Several sessions related to KERI (intro, detail, developer recruitment, project planning, did:un method) - see KERI work item Google doc
    * Current topics related to DID resolution and representations
    * WebID (Tom+Sam)?
6. [Tom and others] Collaborate on statement about WebID
https://drive.google.com/file/d/1HdnlLr6GemqmsCSl7101FZ5lCWJ722h_/view?usp=sharing
    * How to interop with SIOP/DIDs?
    * How does it relate to DIF's .well-known DID configuration (can WebID be "the" endpoint that browsers look at, instead of having many endpoints?)
    * How does it relate to CHAPI?
7. [All] Update on Fuzzy Encryption implementation
https://github.com/decentralized-identity/fuzzy-encryption/tree/dev-kirko-python/src/python
    * See DIF blog post here: https://medium.com/decentralized-identity/dif-id-wg-starting-work-on-cryptographic-secret-recovery-204117b6a2ab
    * See Appendix C here: https://docs.google.com/document/d/1PDTGzurA2EPDglKcAeFkWbKgnuUDWbx1ag929ui4vs0/
8. Updates on current work items
	did:peer, KERI, Universal Resolver, .well-known DID configuration, DID
	parameters, secret recovery mechanisms

### Proposals
-proposals here-

### Attendees
* Markus Sabadello
* Charles Cunningham
* Juan Caballero
* Tom Jones
* Wayne Chang
* Kaliya
* Balazs Nemethi


## Old meeting page (before October 2020) 
[Old meeting page](https://docs.google.com/document/d/1gV99R7G2bUlRerxznyd0ucwWPfc1v2F2gQVaTawIPYI/edit#)
