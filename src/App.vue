<script setup>
import Poem from './components/Poem.vue';

// стих, разделенный на четверостишья

const poem = [
  `Out of the night that covers me,     
  Black as the pit from pole to pole,
  I thank whatever godsmay be 
  For my unconquerable soul.`,
  `In the fell clutch of circumstance 
  I have not winced nor cried aloud. 
  Under the bludgeonings of chance 
  My head is bloody, but unbowed.`,
  `Beyond this place of wrath and tears 
  Looms but the Horror of the shade, 
  And yet the menace of the years 
  Finds and shall find me unafraid.`,
  `It matters not how strait the gate, 
  How charged with punishments the scroll, 
  I am the master of my fate, 
  I am the captain of my soul.`,
];

// добавление отступов

const formattedQuatrains = poem.map((quatrain) => {
  const lines = quatrain.split('\n');
  const modifiedLines = [];
  lines.forEach((line, index) => {
    if (index % 2 === 1) {
      modifiedLines.push('\t      ' + line);
    } else if (index % 3 === 2) {
      modifiedLines.push('\t' + line);
    } else {
      modifiedLines.push(line);
    }
  });
  return modifiedLines.join('\n');
});
</script>

<template>
  <Poem :quatrains="formattedQuatrains" />
</template>

<style scoped></style>
