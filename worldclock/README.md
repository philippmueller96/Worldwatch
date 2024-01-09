# Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

# Worldwatch

Das hier ist eins meiner ersten Projekte in Vue.js und dient daher dem Lernzweck.

Worldwatch dient außerdem der Vermittlung über das Prinzip der Zeitzonen. Du wirst hier also nicht nur deine lokale Zeit sehen, sondern auch neue Standorte hinzufügen, löschen oder eine Beiträge durchlesen können. Mit der Zeit wird nach und nach mehr hinzukommen.

Sei also gespannt auf alles weitere! :)

### ToDo:

#### Funktionen

- Bewertungssystem
  - als Formular
  - mehrer Bewertungen anzeigen lassen
    - als Cards

#### Optisch

- Video als Hintergrund einbinden
  - Schwarzer Fade über die Hälfte des Bildschirms
    > https://www.w3schools.com/howto/howto_css_fullscreen_video.asp
- Logo entwerfen und einbinden
  - Zwei W untereinander und Negativ von Erde ausschneiden

#### Strukturelle Anpassungen

- in eigenen Ordner packen
  - deleteClock
  - CSS u. SCSS
- Einleitung einfügen
- Video mit Tutorial einbinden
  - weitere Sektion der Seite
- Bewertungsformular einfügen

## Installation

## Verwendung

Ich verwende hier Vue.js und SCSS. Falls dir beides noch nicht bekannt sein sollte, findest du hier die Dokumentation:

### Vue.js

> https://vuejs.org/guide/introduction.html

### SCSS

> https://sass-guidelin.es/#introduction

## Funktionalität

### Lokale Zeit

´´´vue
const getTime = () => {
let today = new Date();
let hours = today.getHours();
let minutes = today.getMinutes();
let seconds = today.getSeconds();
return (
hours +
":" +
(minutes < 10 ? "0" : "") +
minutes +
":" +
(seconds < 10 ? "0" : "") +
seconds
);
};

console.log(getTime());
let localTime = ref(getTime());

const createInterval = () => {
setInterval(() => {
localTime.value = getTime();
}, 1000);
};
´´´

### Hinzufügen neuer Standorte

#### Main.vue

´´´vue
function addNewTime(newID, newTime, newLocation) {
timeZones.value.push({
id: newID,
time: newTime,
location: newLocation,
});
console.log(timeZones.value);
}
´´´

#### NewTimeZoneForm.vue

´´´vue
const newLocation = ref("");

const emitAddTimeZone = defineEmits(["addTimeZone"]);

async function addNewTimeZone() {
const newID = uuidv4();
if (containsNumbers(newLocation.value)) {
alert("Contains numbers. Please enter only letters.");
return;
}
try {
const result = await fetchWorldTime(newLocation.value);
const newTime = result.hour + ":" + result.minute + ":" + result.second;

    if (newTime) {
      emitAddTimeZone("addTimeZone", newID, newTime, newLocation.value);
      newLocation.value = "";
    }

} catch (error) {
console.error("Error fetching world time:", error);
alert("Could not find your entered location. Please check and try again.");
}
}

function containsNumbers(location) {
return /\d/.test(location);
}

async function fetchWorldTime(city) {
const apiKey = "syrfzxa2LemedbwMWv+o/g==z4C3ZT7OSnh7MgIm";
const url = `https://api.api-ninjas.com/v1/worldtime?city=${city}`;

const response = await fetch(url, {
method: "GET",
headers: {
"X-Api-Key": apiKey,
"Content-Type": "application/json",
},
});

if (!response.ok) {
throw new Error(`API call failed with status ${response.status}`);
alert("Something went wrong!");
}

return await response.json();
}
´´´

### Löschen vorhandener Standorte

#### Main.vue

´´´vue
function deleteClock(id) {
const index = timeZones.value.findIndex((timeZone) => timeZone.id === id);

if (index !== -1) {
timeZones.value.splice(index, 1);
}
}
´´´

### Aktualisierung im Sekundentakt

#### Main.vue

´´´vue
onMounted(() => {
startUpdatingTime();
});

onBeforeUnmount(() => {
clearInterval(intervalId);
});

function startUpdatingTime() {
intervalId = setInterval(() => {
timeZones.value.forEach((timeZone) => {
const [hours, minutes, seconds] = timeZone.time.split(":").map(Number);
const newSeconds = (seconds + 1) % 60;
const newMinutes = minutes + Math.floor((seconds + 1) / 60);
const newHours = (hours + Math.floor(newMinutes / 60)) % 24;

      timeZone.time = `${String(newHours).padStart(2, "0")}:${String(
        newMinutes
      ).padStart(2, "0")}:${String(newSeconds).padStart(2, "0")}`;
    });

}, 1000);
}
´´´

####

## Dateistruktur

public
|-

src
|- assets
|- components
| |- Footer.vue
| |- Header.vue
| |- LocalTime.vue
| |- Main.vue
| |- NewTimeZoneForm.vue
|- App.vue
|- main.js
|- style.css
|- style.css.map
|- style.scss

## Changelog

commits überprüfen und nachträglich eingeben
