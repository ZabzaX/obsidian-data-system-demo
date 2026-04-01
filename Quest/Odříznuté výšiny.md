---
type:
  - quest
quest_type: main
status:
giver:
related_NPC:
  - "[[Tobias Harvenský]]"
  - "[[Drénik Vargan]]"
  - "[[Norbis Vennel]]"
reward:
  - food
  - shelter
dungeons: "[[Finařina stezka dungeon]]"
state:
  - non_state
city:
  - "[[Harven]]"
region:
  - "[[Trévilské Výšiny]]"
level: 3
---
###### Dungeons
```dataview  
TABLE WITHOUT ID file.link AS Dungeon
FROM "Location"
WHERE contains(related_quest, this.file.link)
SORT city ASC, level ASC
```

## Summary
A caravan is struck by a collapse in [[Finařina stezka]], cutting off the [[Trévilské Výšiny]] from all supplies. The players survive and arrive at [[Harven]], where the mayor [[Tobias Harvenský]] asks for their help.

## Situation
- The region is isolated (no incoming supplies)
- 5 people have disappeared in the village over the past two months
- Political pressure from [[Delhein]] (offer to take control of the region)
## Objectives
- Identify the cause of the collapse
- Investigate the disappearances
- Restore connection to the outside world
## Hooks / Leads
- [[Kobold cave]] (abductions, unknown agent) - possible source of the disappearances
- [[Normanova věž]] - potential magical solution or long-distance communication
- [[Caerwyn (Ruined Village Dungeon)]] - ancient ruins in the north; possible traces of an old route out of the region
- [[Starý jeskynní komplex]] - unexplored cave systems that may lead outside the region
- [[Molkeshův chrám ve výšinách]] - oldest structure in the area; possible underground passages
- [[Druid na sever od města]] - druids may possess knowledge of natural portals

## Key Moments
- Arrival of the damaged caravan to the [[Harven]]
- Meeting with [[Tobias Harvenský]]
- Arrival of [[Norbis Vennel]] by air, presenting an ultimatum disguised as aid:  
	join [[Delhein]] and sign the agreement, or face isolation and starvation as supplies run out
- Player decision on which lead to follow

## Notes (Design Intent)
- Open-ended quest (multiple solutions)
- Strong focus on exploration
- Environmental storytelling (abandoned places, fog, isolation)