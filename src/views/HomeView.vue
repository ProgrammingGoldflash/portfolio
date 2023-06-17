<script lang="ts" setup>
import TechStackIcon from '../classes/TechStackIcon.vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { library } from '@fortawesome/fontawesome-svg-core';
import { faCodeBranch, faWrench, faNewspaper, faAnglesDown, faComputerMouse } from "@fortawesome/free-solid-svg-icons";

library.add(faCodeBranch, faWrench, faNewspaper, faAnglesDown, faComputerMouse)
</script>

<template>
  <div class="absolute inset-0 z-0 bg-[url(../assets/grid.svg)] bg-center"></div>

  <main class="flex flex-col md:flex-row flex-grow h-screen relative">
    <div class="md:w-1/2 p-4 grid bg-black bg-opacity-5 justify-end content-center">
      <div class="grid justify-end content-center text-center space-y-3">
        <h2 class="text-xl font-bold uppercase z-1">Philip</h2>
        <p class="">
          Short person description here. This can span <br> multiple lines and provide more detail about the
          person.
        </p>
        <!-- <a href="#example">Skills</a> -->
        <a href="#example" class="bg-orange-600 text-white font-semibold p-1 rounded-md">
          <font-awesome-icon icon="fa-solid fa-code-branch" />
          techstack
        </a>
        <a href="#example" class="bg-orange-500 text-white font-semibold p-1 rounded-md">
          <font-awesome-icon icon="fa-solid fa-wrench" />
          projects
        </a>
        <a href="#example" class="bg-orange-400 text-white font-semibold p-1 rounded-md">
          <font-awesome-icon icon="fa-solid fa-newspaper" />
          articles
        </a>
      </div>
    </div>

    <div class="md:w-1/2 p-4 grid">
      <div id='ellipse1'
        class="bg-gray-300 h-[284px] w-[284px] top-[379px] left-[1005px] rounded-full justify-self-start self-center">
      </div>
    </div>

    <div id="scroll-down" class="absolute inset-x-0 bottom-10 flex flex-col justify-center items-center text-gray-700">
      <font-awesome-icon icon="fa-solid fa-computer-mouse" />
      <font-awesome-icon icon="fa-solid fa-angles-down" />
    </div>
  </main>

  <div class="flex flex-col md:flex-row flex-grow h-screen relative h-screen">
    <div class="md:w-1/2 p-4 flex flex-col">
      <div class="text-center w-full font-bold uppercase my-8 text-xl">
        Tools and technologies I use on a daily basis
      </div>
      <div class="container" ref="techStack" style="height: 100%;">
        <div v-for="(tech, i) in myTechStack" :key="i"
          :style="{ left: `${tech.positionX}px`, top: `${tech.positionY}px`, animation: `float${i} ${tech.duration}s ease-in-out infinite` }"
          class="icon">
          <img :src="`./src/assets/images/techStack/${tech.icon}`" />
        </div>
      </div>
    </div>
    <div class="md:w-1/2 p-4 flex flex-col bg-black bg-opacity-10 justify-end content-center">
      <div class="text-center w-full font-bold uppercase my-8 text-xl">
        Technologies that I used in projects
      </div>
      <div class="container" ref="experience" style="height: 100%;">
        <div v-for="(exp, i) in experience" :key="i"
          :style="{ left: `${exp.positionX}px`, top: `${exp.positionY}px`, animation: `float${i + myTechStack.length} ${exp.duration}s ease-in-out infinite` }"
          class="icon">
          <img :src="`./src/assets/images/experience/${exp.icon}`" />
        </div>
      </div>
    </div>
  </div>

  <div class="flex flex-col md:flex-row flex-grow h-screen relative h-screen">
    <div class="md:w-1/2 p-4 grid bg-black bg-opacity-10 justify-end content-center">

    </div>

    <div class="md:w-1/2 p-4 grid">

    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: "TechStackComponent",
  data(): { myTechStack: TechStackIcon[]; experience: TechStackIcon[] } {
    return {
      myTechStack: [],
      experience: [],
    };
  },
  mounted() {
    this.myTechStack = this.initIcons(
      ["azure.png", "csharp.png", "dotnet.png", "javascript.png", "ms_sql_server.png", "visual_studio.png", "visual_studio_code.png", "blazor.png", "postman.png", "git.png", "html.png", "css.png", "webassembly.png", "docker.png"],
      this.$refs.techStack as HTMLElement
    );
    this.experience = this.initIcons(
      ["angular.png", "cplusplus.png", "firebase.png", "grafana.png", "graphql.png", "java.png", "mysql.png", "next_js.png", "node_js.png", "open_api.png", "php.png", "react.png", "redux.png", "typescript.png", "nginx.png", "mongo_db.png"],
      this.$refs.experience as HTMLElement
    );
    this.appendStyles();
  },
  methods: {
    halton(n: number, base: number) {
      var result = 0;
      var f = 1 / base;
      var i = n;
      while (i > 0) {
        result = result + f * (i % base);
        i = Math.floor(i / base);
        f = f / base;
      }
      return result;
    },
    initIcons(iconArray: Array<string>, parent: HTMLElement) {
      return iconArray.map((icon, i) => {
        let padding = Math.floor(Math.random() * 50 + 2);
        let x = padding + this.halton(i, 2) * (parent.offsetWidth - 5 * padding);
        let y = padding + this.halton(i, 3) * (parent.offsetHeight - 5 * padding);
        let duration = Math.random() * 4 + 1;
        let distanceX = Math.random() * 2 + 1;
        let distanceY = Math.random() * 2 + 1;
        return new TechStackIcon(icon, x, y, duration, distanceX, distanceY);
      });
    },
    appendStyles() {
      let styleElement = document.createElement('style');
      [...this.myTechStack, ...this.experience].forEach((item, i) => {
        let keyframes = `
          @keyframes float${i} {
            0%, 100% {
              transform: translate(0, 0);
            }
            50% {
              transform: translate(${item.distanceX}px, ${item.distanceY}px);
            }
          }
        `;
        styleElement.textContent += keyframes;
      });
      document.head.appendChild(styleElement);
    },
  },
};
</script>

<style>
.icon {
  width: 80px;
  height: 90px;
  margin: 10px;
  position: absolute;
}

.container {
  position: relative;
  height: 50%;
  padding: 30px;
}

.right-column {
  background: linear-gradient(90deg, rgba(109, 109, 111, 1) 0%, rgba(0, 0, 0, 1) 100%);
  clip-path: polygon(40% 0, 100% 0, 100% 100%, 30% 100%);
  position: absolute;
  z-index: -1;
}

header {
  min-height: 5vh;
}

main {
  min-height: 95vh;
}

html {
  scroll-behavior: smooth;
}

@-webkit-keyframes bounce {
  0% {
    transform: translateY(-5px)
  }

  50% {
    transform: translateY(10px)
  }

  100% {
    transform: translateY(-5px)
  }
}

@keyframes bounce {
  0% {
    transform: translateY(-5px)
  }

  50% {
    transform: translateY(10px)
  }

  100% {
    transform: translateY(-5px)
  }
}

#scroll-down {
  -webkit-animation: bounce 3s infinite ease-in-out;
  -o-animation: bounce 3s infinite ease-in-out;
  -ms-animation: bounce 3s infinite ease-in-out;
  -moz-animation: bounce 3s infinite ease-in-out;
  animation: bounce 3s infinite ease-in-out;
}
</style>