---
type: npc
race:
  - "[[Human]]"
age: "38"
state:
  - non_state
city:
  - "[[Harven]]"
region:
  - "[[Trévilské Výšiny]]"
organization:
  - none
role: commoner
occupation: mayor
related_NPC:
social_class: middle_class
status: alive
importance: major
alignment: good
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
A man in his forties. Strong and capable, but despite being the mayor, he does not make decisions alone - he always gathers the townspeople to discuss important matters.

He deeply values the freedom that the [[Trévilské Výšiny]] provide. Under no circumstances would he agree to join any state. In his view, no single ruler should have the power to decide the fate of others.

He possesses magical abilities as a sorcerer, though he never chose to further develop his talent.
