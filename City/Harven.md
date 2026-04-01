---
type:
  - city
settlement_type: village
state:
  - non_state
status: destroyed
mayor: "[[Tobias Harvenský]]"
capital: false
population: "0"
industry:
  - fishing
  - mining
direction: west
dominant_race:
  - "[[Human]]"
region:
  - "[[Trévilské Výšiny]]"
---

###### NPC 
```dataview  
TABLE WITHOUT ID  
file.link AS "NPC",  
join(occupation, ", ") AS "Occupation",  
role AS "Role",  
choice(status = "alive", "🟢 Alive", "🔴 Dead") AS "Status",  
importance AS "Importance"  
FROM "NPC"  
WHERE contains(city, this.file.link)  
SORT join(occupation, ", ") ASC
```

###### Districts
```dataview  
TABLE  
district_type AS "Type",  
wealth AS "Wealth",  
security AS "Security",  
population AS "Population"
FROM "Location"  
WHERE contains(city, this.file.link)  
AND location_type = "district"  
SORT district_type ASC
```

###### Buildings
```dataview
TABLE  
building_type AS "Type",  
subtype, 
owner,  
specialization,  
district, 
price,  
deity,  
importance  
FROM "Location"  
WHERE contains(city, this.file.link)  
AND location_category = "building"  
SORT district ASC, building_type ASC, subtype ASC, district ASC
```
###### Important houses
```dataview  
LIST
FROM "House"
WHERE contains(seat, this.file.link)
SORT file.name
```
###### Eventy
```dataview  
TABLE era AS "Éra"
FROM "Event"
WHERE contains(city, this.file.link)
SORT era ASC
```
###### Quests
```dataview  
TABLE level, quest_type, giver, reward
FROM "Quest"
WHERE contains(city, this.file.link)
SORT city ASC, level ASC
```

#### description
A small settlement. The only village in the [[Trévilské Výšiny]].

The first mayor was **Daruan Harvenský**, after whom the village is named. After his death, leadership passed to his son, **Deren Harvenský**, and the current mayor is Daruan’s grandson, [[Tobias Harvenský]].

The village is heavily dependent on trade. While its inhabitants are capable of producing most goods themselves, they frequently lack essential materials due to the infrequency of caravans passing through the region.

The local economy relies on exporting crafted goods and on travelers who stop here while journeying between the western and eastern parts of Mundos.