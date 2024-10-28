<template>
  <div class="wrapper">
    <div class="cube" ref="cube">
      <div class="front">
            <span class="" v-if="input.length >= 1 && input[0]">
                {{ input[0] }}
            </span>
        <span v-else>
          Rechts
        </span>
      </div>
      <div class="back">

             <span class="" v-if="input.length >= 1 && input[1]">
                {{ input[1] }}
            </span>
        <span v-else>
                Links
            </span>
      </div>
      <div class="left">
             <span class="" v-if="input.length >= 1 && input[2]">
                {{ input[2] }}
            </span>
        <span v-else>
                U-Turn
            </span>
      </div>
      <div class="right">
             <span class="" v-if="input.length >= 1 && input[3]">
                {{ input[3] }}
            </span>
        <span v-else>
                Geradeaus
            </span>
      </div>
      <div class="top">
            <span class="" v-if="input.length >= 1 && input[4]">
                {{ input[4] }}
            </span>
        <span v-else>
                Würfel noch einmal
            </span>
      </div>
      <div class="bottom">
            <span class="" v-if="input.length >= 1 && input[5]">
                {{ input[5] }}
            </span>
        <span v-else>
                Autobahn
            </span>
      </div>
    </div>
  </div>
</template>

<script setup>

defineProps({
  input: {
    required: true,
    type: Array,
    default: []
  }
})

const cube = ref();

console.log(cube);

// var cube = document.getElementsByClassName('cube')[0];
// console.log(cube)

var min = 1;
var max = 24;

var curXAngle = 0;
var curYAngle = 0;

onMounted(() => {
  cube.value.addEventListener('click', () => {
    // Die korrekten Winkel für die Würfelseiten (front, left, right, back, bottom, top)
    var xAngle = [0, 0, 0, 0, 90, 270];
    var yAngle = [0, 90, 270, 180, 0, 0];

    // Sicherstellen, dass die gewürfelten Seiten gleichverteilt sind
    var targetSide = Math.floor(Math.random() * 6);

    // Den Zielwinkel holen
    var xRand = xAngle[targetSide];
    var yRand = yAngle[targetSide];

    // Zufällige Rotationen hinzufügen, damit der Würfel sich etwas mehr bewegt.
    // Sicherstellen, dass wir immer um ganzzahlige Vielfache von 360 Grad rotieren, damit die Orientierung
    // des Würfels immer gleich bleibt
    xRand += 360 * Math.floor(Math.random() * 2 + 1);
    yRand += 360 * Math.floor(Math.random() * 2 + 1);

    // Sicherstellen, dass wir uns immer um mindestens 360 Grad drehen, damit immer genug Bewegung passiert
    while (Math.abs(xRand - curXAngle) < 360) {
      xRand += 360;
    }
    while (Math.abs(yRand - curYAngle) < 360) {
      yRand += 360;
    }

    // Die Dauer des Übergangs dynamisch setzen, damit die Geschwindigkeit der Drehung konstant ist
    var distAngle = Math.abs(xRand - curXAngle) + Math.abs(yRand - curYAngle);
    var duration = distAngle / 270;

    cube.value.style.transitionDuration = duration+'s';
    cube.value.style.webkitTransform = 'rotateY('+yRand+'deg) rotateX('+xRand+'deg)';
    cube.value.style.transform = 'rotateY('+yRand+'deg) rotateX('+xRand+'deg)';

    curXAngle = xRand;
    curYAngle = yRand;
  })
});

function getRandom(max, min) {
  let angle = (Math.floor(Math.random() * (max-min)) + min) * 90;
  console.log("angle="+angle+" mod 360 = "+angle%360);

  return (Math.floor(Math.random() * (max-min)) + min) * 90;
}
</script>

<style lang="scss" scoped>
.wrapper {
  margin: 0 auto 200px;
  width: 200px;
  height: 200px;
  perspective: 400px;
  perspective-origin: 50% 100%;
}

.cube {
  position: relative;
  transform-style: preserve-3d;
  transition: transform 6s;
  width: 100%;
  height: 100%;
  top: 100px;
}

.cube div {
  background-color: rgba(110,126,133,0.8);
  border: 1px solid #545F64;
  width: 200px;
  height: 200px;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  color: whitesmoke;
  font-family: Arial, Helvetica, sans-serif;
  border-radius: 7px;
}

.front {
  transform:
      translateZ(100px);
}

.back {
  transform:
      rotateY(-180deg)
      translateZ(100px);
}

.right {
  transform:
      rotateY(90deg)
      translateZ(100px);
}

.left {
  transform:
      rotateY(-90deg)
      translateZ(100px);
}

.top {
  transform:
      rotateX(90deg)
      translateZ(100px);
}

.bottom {
  transform:
      rotateX(-90deg)
      translateZ(100px);
}
</style>