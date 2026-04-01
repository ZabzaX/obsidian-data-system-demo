---
type: npc
race:
  - "[[Human]]"
age: "47"
state:
  - non_state
city:
  - "[[Harven]]"
region:
  - "[[Trévilské Výšiny]]"
organization:
  - none
role: commoner
occupation:
  - healer
  - merchant
  - shopkeeper
related_NPC:
social_class: middle_class
status: alive
importance: background
alignment: neutral
era: "[[8 Věk dýmu a železa]]"
related_event:
---

```dataview  
TABLE  
race,  
age, 
occupation,  
role, 
region, 
state, 
city,  
status,  
importance  
WHERE file = this.file
```

###### Organizace 
```dataview  
LIST
FROM "Organization"
WHERE contains(members, this.file.link) OR contains(leader, this.file.link)
SORT file.name
```
###### Related NPC
```dataview  
LIST
FROM "NPC"
WHERE contains(related_NPC, this.file.link) 
OR contains(this.related_npc, file.link)
SORT file.name
```
###### Related Quests
```dataview  
LIST
FROM "Quest"
WHERE contains(related_NPC, this.file.link)
SORT file.name
```
###### Eventy

```dataview  
LIST
FROM "Event"
WHERE contains(participants, this.file.link)
SORT file.name
```
#### description
A woman in her fifties, with greying hair always tied back under a scarf, her hands stained with ink and herbs.

She is not a mage, but an alchemist - herbs are her domain. She can stop bleeding, prepare remedies for pain or fever, but is incapable of healing through magic.

She settled in Harven years ago after her husband died from an illness she could not cure. Since then, she has dedicated herself to ensuring that no one around her suffers needlessly.

Somewhat gruff in demeanor, but ultimately kind-hearted.