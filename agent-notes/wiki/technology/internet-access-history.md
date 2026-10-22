---
source: agent
compiled_from:
  - agent-notes/raw/technology/2019-10-29-murphy-dial-up-to-5g.md
compiled_at: 2026-10-21
model: claude-fable-5-1
confidence: medium
---

# Internet access history: from ARPANET to 5G

Mike Murphy's October 2019 Quartz explainer traces how people have connected to the internet, from ARPANET's leased telephone lines to the first 5G rollouts. It is a timeline reference rather than an argument, and McCormick draws on it for the history half of [[apps-infrastructure-cycle]]. This article compresses it into a table, adds what the sequence shows, corrects one date, and updates the 2019 forecasts.

## Timeline

| Era | Access technology | Key facts from Murphy | What it enabled |
| --- | --- | --- | --- |
| ARPANET (1969 to 1980s) | Leased phone lines between Interface Message Processors (the first routers) | ARPA's Cold War project; UCLA's $700,000 SDS Sigma 7 ($4.8M in 2019 dollars) sent "lo" to Stanford, crashing on the third letter of "login"; satellite link to NORSAR in Norway and on to London by the mid-1970s; NSF grants connected smaller universities in the 1980s; ~25 countries by the late 1980s; MILNET split off in 1983 | Tomlinson's email (1971); the term "internet" (Cerf) |
| Pre-web internet (late 1980s to early 1990s) | Same, with standardized protocols | "An almost entirely text-based world... only welcoming to techies" (Vaughan-Nichols) | IRC, Usenet, FTP |
| Web and dial-up (1991 to ~2004) | Phone modem: PC modems from 1977, 56k from 1996 | Berners-Lee's 1989 proposal at CERN; Mosaic (1993); Netscape Navigator at ~80% share by the mid-1990s; Internet Explorer shipping with Windows 95 and out-iterating Netscape (CSS first); AOL, Prodigy, Earthlink, CompuServe; the phone line tied up while online | Static web pages; a 1 GB file took about 3.5 days at 56k versus 32 seconds in 2019 |
| Broadband and wifi (2004 onward) | Cable and DSL, always on; wifi from the mid-1990s, mainstream after the 1999 iBook | Pew: broadband passed dial-up in the US in 2004; FCC benchmark 25/3 Mbps at the time of writing | Richer pages, real-time commerce, YouTube (2005) |
| Mobile (1999 onward) | WAP (1999, Nokia 7110), 3G (2003), the iPhone (2007; 3G model 2008), LTE | Smartphone subscriptions from 1.9B (end 2013) to 5.3B (end 2018); over a billion iPhones and two billion Android devices; $120B in App Store developer revenue since 2008; four hours a day on phones; 8 GB a month of data per US user, forecast by Ericsson to reach 200 GB by 2025 | "An iPod, a phone, and an internet communicator"; the app economy |
| 5G (2019 onward) | Millimeter-wave and sub-6 GHz cellular, promising >1 Gbps against LTE's ~25 Mbps in the US | Remote surgery, monitored autonomous truck fleets, AR glasses, cloud-hosted computers: "for now, these are still pipe dreams" | To be determined |

Coverage gaps as of 2019: about 19 million Americans and roughly 43% of the world's population without access, with cable companies reusing old broadcast spectrum and autonomous balloons as the proposed fixes.

## What the sequence shows

- **Access technologies are invented long before they matter.** The modem dates to 1958 and the PC modem to 1977, but the web needed the 56k modem of 1996; wifi existed in the mid-1990s and mattered after 1999; WAP arrived in 1999 and mobile internet took off in 2007. The lag closes when a device or interface makes the access worth paying for, which is the interface term McCormick adds to the cycle in [[apps-infrastructure-cycle]].
- **Access and use are different curves.** Connecting people is one story; moving money and behavior online is another, which is Evans's argument in [[internet-maturation]].
- **Each bandwidth jump unlocks an application category.** 56k gave web pages, broadband gave video, 3G and LTE gave Uber and Snapchat. The open question Murphy ends on is what 5G unlocks; see the temporal notes.
- **The critical input collapsed in price.** From a $700,000 room-sized computer to a sub-$50 smartphone is five orders of magnitude, the "critical factor of production suddenly becoming very cheap" that opens a surge in [[technological-revolutions]].

## Corrections to the source

- Murphy dates the first webpage to 1993. Berners-Lee's first site went live in 1991; 1993 is when CERN placed the web software in the public domain (April 30).
- CERN is a particle-physics laboratory; "nuclear" survives only in the acronym.

## Temporal notes

- **5G's consumer effect was mostly faster phones and fixed wireless home internet.** T-Mobile's and Verizon's 5G home services accounted for essentially all US broadband net additions in 2022 and 2023 (Leichtman Research Group). Remote surgery and AR glasses did not go mainstream. Autonomous vehicles did arrive ([[waymo-autonomous-driving]]) but rely on onboard compute rather than the network.
- **Balloons lost to satellites.** Google's Loon shut down in January 2021; the answer for hard-to-reach users became low-earth-orbit constellations, with Starlink passing 12 million subscribers by mid-2026. Dourado's 2020 forecast of exactly this is scored in [[technology-in-the-2020s]].
- **The offline share fell.** The ITU estimated about 5.5 billion people online in 2024, roughly a third of humanity offline against the 43% Murphy cites.
- **The FCC raised its broadband benchmark** to 100/20 Mbps in March 2024.
- **Ericsson's 200 GB a month by 2025 did not happen.** Ericsson's own later Mobility Reports put North American usage at tens of gigabytes a month.

## Sources

- Murphy, Mike (2019-10-29). "From dial-up to 5G: a complete guide to logging on to the internet." Quartz. <https://qz.com/1705375/a-complete-guide-to-the-evolution-of-the-internet/> (captured via the Internet Archive; qz.com refuses direct fetches) — [[2019-10-29-murphy-dial-up-to-5g|local copy]]
