---
type:
  - location
location_category: building
building_type:
  - shop
shop_quality: rare
subtype: alchemy
specialization:
Deity:
owner:
  - "[[Maribel Veyra]]"
city:
  - "[[Harven]]"
district:
state:
region:
  - "[[Trévilské Výšiny]]"
importance:
shop_inventory_type:
  - potion
  - poison
extra_inventory:
price: cheap
extra_inventory_max_rarity:
special_items:
---


##### Shop inventory
```dataviewjs
const shop = dv.current();  
const items = dv.pages('"Items"');  
  
const root = dv.container;  
root.innerHTML = "";  
  
// UI  
const controls = root.createEl("div");  
  
const sortSelect = controls.createEl("select");  
["price","rarity"].forEach(opt => {  
let o = sortSelect.createEl("option", {text: opt, value: opt});  
if (opt === "price") o.selected = true;  
});  
  
const subtypeSelect = controls.createEl("select");  
subtypeSelect.style.marginLeft = "10px";  
  
const searchInput = controls.createEl("input");  
searchInput.placeholder = "Search...";  
searchInput.style.marginLeft = "10px";  
  
// DEBUG INFO  
const debug = root.createEl("div");  
debug.style.margin = "6px 0";  
debug.style.fontSize = "12px";  
  
// TABLE  
const tableContainer = root.createEl("div");  
  
// HELPERS  
function getPrice(i) {  
let val =  
shop.price === "cheap" ? i.price_cheap :  
shop.price === "normal" ? i.price_normal :  
i.price_expensive;  
  
let num = parseFloat(val);  
return isNaN(num) ? 0 : num;  
}  
  
function rarityCheck(i) {  
if (i.rarity == "common") return true;  
if (i.rarity == "uncommon") return shop.shop_quality != "common";  
if (i.rarity == "rare") return ["rare","very rare","legendary"].includes(shop.shop_quality);  
if (i.rarity == "very rare") return ["very rare","legendary"].includes(shop.shop_quality);  
if (i.rarity == "legendary") return shop.shop_quality == "legendary";  
return false;  
}  
  
function rarityAllowed(rarity, max) {  
const order = ["common","uncommon","rare","very rare","legendary"];  
return order.indexOf(rarity) <= order.indexOf(max);  
}  
  
function availabilityCheck(i) {  
if (!i.availability || i.availability.length === 0) return true;  
return i.availability.some(a =>  
shop.city?.includes(a) ||  
shop.state?.includes(a) ||  
shop.region?.includes(a)  
);  
}  
  
// DATA  
function getData() {  
return items  
.where(i =>  
(  
(  
(  
(  
shop.shop_inventory_type?.includes(i.item_type) ||  
(Array.isArray(i.item_subtype) && i.item_subtype.some(s => shop.shop_inventory_type?.includes(s)))  
)  
&& rarityCheck(i)  
)  
||  
(  
(  
shop.extra_inventory?.includes(i.item_type) ||  
(Array.isArray(i.item_subtype) && i.item_subtype.some(s => shop.extra_inventory?.includes(s)))  
)  
&& rarityAllowed(i.rarity, shop.extra_inventory_max_rarity || "common")  
)  
)  
&& availabilityCheck(i)  
)  
|| shop.special_items?.some(s => s.path === i.file.path)  
)  
.map(i => ({  
name: i.file.name,  
path: i.file.path,  
subtype: Array.isArray(i.item_subtype) ? i.item_subtype : [],  
rarity: i.rarity,  
price: getPrice(i),  
special: shop.special_items?.some(s => s.path === i.file.path),  
isExtra:  
(  
shop.extra_inventory?.includes(i.item_type) ||  
(Array.isArray(i.item_subtype) && i.item_subtype.some(s => shop.extra_inventory?.includes(s)))  
)  
}));  
}  
  
// RENDER  
function render() {  
tableContainer.innerHTML = "";  
  
let data = getData();  
  
// DEBUG  
debug.innerText = "SORT: " + sortSelect.value;  
  
// subtype options  
const subtypeSet = new Set();  
data.forEach(i => i.subtype.forEach(s => subtypeSet.add(s)));  
  
const currentSubtype = subtypeSelect.value;  
  
subtypeSelect.innerHTML = "";  
subtypeSelect.createEl("option", {text: "All", value: ""});  
  
[...subtypeSet].forEach(s => {  
let opt = subtypeSelect.createEl("option", {text: s, value: s});  
if (s === currentSubtype) opt.selected = true;  
});  
  
// search  
const search = searchInput.value?.toLowerCase();  
if (search) {  
data = data.filter(i => i.name.toLowerCase().includes(search));  
}  
  
// subtype filter  
const sub = subtypeSelect.value;  
if (sub) {  
data = data.filter(i => i.subtype.includes(sub));  
}  
  
// SORT  
if (sortSelect.value === "price") {  
data = [...data].sort((a, b) => a.price - b.price);  
}  
  
if (sortSelect.value === "rarity") {  
const order = ["common","uncommon","rare","very rare","legendary"];  
data = [...data].sort((a, b) => order.indexOf(a.rarity) - order.indexOf(b.rarity));  
}  
  
// ROZDĚLENÍ  
const specialItems = data.filter(i => i.special);  
const extraItems = data.filter(i => !i.special && i.isExtra);  
const normalItems = data.filter(i => !i.special && !i.isExtra);  
  
// RENDER SEKCE  
function renderSection(title, list) {  
if (list.length === 0) return;  
  
const h = tableContainer.createEl("h3", {text: title});  
h.style.marginTop = "10px";  
  
const table = tableContainer.createEl("table");  
table.style.borderCollapse = "collapse";  
table.style.width = "100%";  
  
const header = table.createEl("tr");  
header.style.opacity = "0.7";  
header.style.fontSize = "12px";  
  
["Item","Subtype","Rarity","Price"].forEach(h => {  
header.createEl("th", {text: h});  
});  
  
list.forEach((i, index) => {  
const row = table.createEl("tr");  
  
// zebra  
if (index % 2 === 0) {  
row.style.backgroundColor = "rgba(255,255,255,0.03)";  
}  
  
row.style.fontSize = "13px";  
  
// highlight special  
if (i.special) {  
row.style.backgroundColor = "rgba(255, 215, 0, 0.08)";  
row.style.borderLeft = "3px solid gold";  
}  
  
// CELLS  
const linkCell = row.createEl("td");  
linkCell.style.padding = "4px 8px";  
  
linkCell.createEl("a", {  
text: i.name,  
href: i.path,  
cls: "internal-link"  
});  
  
row.createEl("td", {  
text: i.subtype.join(", "),  
attr: {style: "padding: 4px 8px; opacity: 0.7;"}  
});  
  
row.createEl("td", {  
text: i.rarity,  
attr: {style: "padding: 4px 8px;"}  
});  
  
row.createEl("td", {  
text: i.price,  
attr: {style: "padding: 4px 8px; text-align: right; font-weight: 500;"}  
});  
});  
}  
  
// VÝSTUP  
renderSection("⭐ Special Items", specialItems);  
renderSection("🧪 Extra Inventory", extraItems);  
renderSection("📦 Normal Inventory", normalItems);  
}  
  
// EVENTS  
sortSelect.onchange = render;  
subtypeSelect.onchange = render;  
searchInput.oninput = render;  
  
render();
```

