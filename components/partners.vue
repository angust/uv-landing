<template>
    <div class="partners-display">

        <div class="background-stack">


                <div
                  class="stack-row"
                  :class="`s${index + 1}`"
                  v-for="(row, index) in rowStack"
                  :key="index + 1"
                >
                  <div class="stack">
                    <div class="stack-block" v-for="item in row">
                     <img :src="item.src" />
                    </div>
                  </div>
                  <div class="stack">
                    <div class="stack-block" v-for="item in row">
                     <img :src="item.src" />
                    </div>
                  </div>
                  <div class="stack">
                    <div class="stack-block" v-for="item in row">
                     <img :src="item.src" />
                    </div>
                  </div>
                  
                </div>
        </div>

        <div class="logo-display">

            <img src="images/graphics/uno-symbol.svg">
        </div>

        <div class="shadow-footer"></div>
    </div>
</template>

<script>
export default {
components: {

},
name: "Partners",
data() {
    return{
        rows: 3,
        partners: [
        { name: "Wine Club", src: "images/partners/bleasdale.jpg" },
        { name: "Our Wines", src: "images/partners/brockenchack.jpg" },
        { name: "Wine Club", src: "images/partners/dowie-doole.jpg" },
        { name: "Our Wines", src: "images/partners/show-block.jpg" },
        { name: "Wine Club", src: "images/partners/tarawarra.jpg" },
        { name: "Our Wines", src: "images/partners/vickery.jpg" },
        { name: "Wine Club", src: "images/partners/passing-clouds.jpg" },
        { name: "Our Wines", src: "images/partners/brockenchack.jpg" },
        { name: "Wine Club", src: "images/partners/dowie-doole.jpg" },
        { name: "Our Wines", src: "images/partners/show-block.jpg" },
        { name: "Wine Club", src: "images/partners/tarawarra.jpg" },
        { name: "Our Wines", src: "images/partners/vickery.jpg" },
      ]
    }
},
computed: {
    rowStack() {
      let rows = [];
      let mid = Math.round(this.partners.length / this.rows);
      for (let row = 0; row < this.rows; row++) {
        rows.push(this.partners.slice(row * mid, row * mid + mid));
      }
      return rows;
    }
}
}
</script>

<style  lang="scss" scoped>
.stack-block {
    height: 9em;
    width: 16em;
    border-radius: 6px;
    position: relative;
    overflow: hidden;
    img {
        object-fit: cover;
        opacity: .5;
    }
}

.stack-row {
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    gap:1em;
}

.stack-row {
    .stack{
    }
    &.s1 {
        .stack {
            --marquee-start: 0%;
        }
    }

    &.s2 {
        .stack {
            --marquee-start: 20%;
            animation: 32s linear 0s infinite normal backwards running scrolly;
        }
    }
    &.s3 {
        .stack {
            --marquee-start: 80%;
        }
    }
    &.s4 {
        .stack {
            --marquee-start: 20%;
        }
    }
}

.stack {
    display: flex;
    flex-direction: row;
    gap: 1em;
    animation: 28s linear 0s infinite normal backwards running scrolly;
}

.background-stack {
    display: flex;
    gap: 1em;
    flex-direction: column;
}

.stack-block {
    background: #17164f;
    
}

.background-stack {
    user-select: none;
    max-width: 100%;
    margin: auto;
}

.partners-display {
    position: relative;
    overflow: hidden;
    max-width: 800px;
    margin: 0 auto;
    &:before {
        content: "";
        position: absolute;
        left: 0;
        top: 0px;
        background: linear-gradient(270deg, #010032 0%, rgba(6, 6, 6, 0) 100%);
        transform: rotate(-180deg);
        will-change: transform;
        width: 5em;
        height: 100%;
        z-index: 1;
    }

    &:after {
        content: "";
        position: absolute;
        right: 0;
        top: 0px;
        background: linear-gradient(270deg, #010032 0%, rgba(6, 6, 6, 0) 100%);
        width: 5em;
        height: 100%;
        z-index: 1;
    }
}

.logo-display {
    --size: 160px;
    position: absolute;
    inset: 0px;
    margin: auto;
    width: var(--size);
    height: var(--size);
    display: flex;

    &:before {
        content: "";
        inset: -100px;
        position: absolute;
        border-radius: 50%;
        background: radial-gradient(#010032 0px, #010032 40px, transparent 50%);
    }

    img {
        z-index: 3;
        position: relative;
        filter: drop-shadow(0px 3px 6px #010032);
    }
}


.shadow-footer {
    position: absolute;
    bottom: 0px;
    background: linear-gradient(0deg, #010032 0%, transparent 100%);
    width: 100%;
    height: 5em;
    z-index: 2;
}

/*!sc*/
@keyframes scrolly {
    0% {
        -webkit-transform: translateX(var(--marquee-start, 0%));
        -ms-transform: translateX(var(--marquee-start, 0%));
        transform: translateX(var(--marquee-start, 0%));
    }

    100% {
        -webkit-transform: translateX(calc(-100% + var(--marquee-start, 0%)));
        -ms-transform: translateX(calc(-100% + var(--marquee-start, 0%)));
        transform: translateX(calc(-100% + var(--marquee-start, 0%)));
    }
}

/*!sc*/
</style>