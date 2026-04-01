---
type: region
location_category: geography
dominant_race:
state: non_state
terrain:
  - highlands
  - forest
  - hills
climate: temperate
danger: low
resources:
importance: major
---
###### City
```dataview  
TABLE WITHOUT ID file.link AS city, state, mayor, population
FROM "City"
WHERE contains(region, this.file.link)
SORT city ASC, level ASC
```

###### NPC 
```dataview  
TABLE WITHOUT ID  
file.link AS "NPC", 
city AS "City",  
join(occupation, ", ") AS "Occupation",  
role AS "Role", 
choice(status = "alive", "🟢 Alive", "🔴 Dead") AS "Status",  
importance AS "Importance"  
FROM "NPC"  
WHERE contains(region, this.file.link)  
SORT join(occupation, ", ") ASC
```
###### Lokace
```dataview  
TABLE location_type AS "Typ lokace"
FROM "Location"
WHERE contains(parent_region, this.file.link)
SORT location_type ASC, level ASC
```
###### Quests
```dataview  
TABLE level, quest_type, giver, reward
FROM "Quest"
WHERE contains(region, this.file.link)
SORT city ASC, level ASC
```
###### Eventy
```dataview  
TABLE era AS "Éra"
FROM "Event"
WHERE contains(region, this.file.link)
SORT era ASC
```

#### description
An area located approximately 650 meters above sea level. Settlement began around year 32 of the [[8 Věk dýmu a železa]]. Colonization was difficult, as it was not supported by any state. People were drawn here primarily by the freedom that was lacking in [[Delhein]].

Obtaining materials other than wood and stone was challenging, as was acquiring proper tools. The first settlers brought everything with them at their own expense.

One of the earliest settlers was Darian Harvenský, who was chosen as the first mayor. The only village in the highlands, [[Harven]], was named after him.

The region remains largely unexplored. Stone is mined near the entrance to [[Finařina stezka]], and only a small portion of one forest, the one across the river has been explored.

The second forest is almost entirely unknown. There are also several other locations within the highlands that are known by name, but none have been properly explored. Any knowledge about them comes from accounts over a fifty years old, preserved only as fragments of stories and rumors.