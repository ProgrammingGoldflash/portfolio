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
    <div class="md:w-1/2 p-4 grid justify-end content-center">
      <div class="grid justify-end content-center text-center space-y-3">
        <h2 class="text-xl font-bold uppercase z-1">Philip</h2>
        <p class="">
          Short person description here. This can span <br> multiple lines and provide more detail about the
          person.
        </p>
        <!-- <a href="#example">Skills</a> -->
        <a href="#techstack" class="bg-orange-600 text-white font-semibold p-1 rounded-md">
          <font-awesome-icon icon="fa-solid fa-code-branch" />
          techstack
        </a>
        <a href="#projects-articles" class="bg-orange-500 text-white font-semibold p-1 rounded-md">
          <font-awesome-icon icon="fa-solid fa-wrench" />
          projects
        </a>
        <a href="#projects-articles" class="bg-orange-400 text-white font-semibold p-1 rounded-md">
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

  <div id="techstack" class="flex flex-col md:flex-row flex-grow relative h-screen">
    <div class="md:w-1/2 p-4 flex flex-col">
      <div class="horizontal-line-container">
        <div class="horizontal-line"></div>
        <h2 class="title">Tools and technologies I use on a daily basis</h2>
        <div class="horizontal-line"></div>
      </div>
      <div class="container" ref="techStack" style="height: 100%;">
        <div v-for="(tech, i) in myTechStack" :key="i" class="icon">
          <img :src="`./src/assets/images/techStack/${tech.icon}`" />
          <p class="icon-caption">{{ tech.icon.split('.').slice(0, -1).join('.') }}</p>
        </div>
      </div>

    </div>
    <div class="md:w-1/2 p-4 flex flex-col justify-end content-center">
      <div class="horizontal-line-container">
        <div class="horizontal-line"></div>
        <h2 class="title">Technologies that I used in projects</h2>
        <div class="horizontal-line"></div>
      </div>
      <div class="container" ref="experience" style="height: 100%;">
        <div v-for="(exp, i) in experience" :key="i" class="icon">
          <img :src="`./src/assets/images/experience/${exp.icon}`" />
          <p class="icon-caption">{{ exp.icon.split('.').slice(0, -1).join('.') }}</p>
        </div>
      </div>

    </div>
  </div>

  <div id="projects-articles" class="flex flex-col md:flex-row flex-grow relative h-screen">
    <div class="md:w-1/2 p-4 grid justify-end content-center">

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
      this.shuffleArray(["Azure.png", "CSharp.png", "dotNET.png", "Javascript.png", "SQLServer.png", "Visual Studio.png", "Visual Studio Code.png", "Blazor.png", "Postman.png", "Git.png", "Html.png", "Css.png", "WebAssembly.png", "Docker.png"]),
      this.$refs.techStack as HTMLElement
    );
    this.experience = this.initIcons(
      this.shuffleArray(["Angular.png", "C++.png", "Firebase.png", "Grafana.png", "GraphQL.png", "Java.png", "MySQL.png", "NextJS.png", "NodeJS.png", "OpenApi.png", "Php.png", "React.png", "Redux.png", "Typescript.png", "Nginx.png", "MongoDB.png"]),
      this.$refs.experience as HTMLElement
    );
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
    shuffleArray(array: Array<string>) {
      let currentIndex = array.length, temporaryValue, randomIndex;

      while (0 !== currentIndex) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }

      return array;
    }
  },
};
</script>

<style>
.horizontal-line-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100px;
  margin-left: 4rem;
  margin-right: 4rem;
  /* adjust as needed */
}

.title {
  font-style: italic;
  font-size: 1.5rem;
  margin: 0 20px;
  z-index: 1;
}

.horizontal-line {
  flex-grow: 1;
  height: 2px;
  background-color: #a5a5a5;
  /* adjust color as needed */
  z-index: 0;
}

.icon {
  width: 80px;
  height: 90px;
  margin: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.container {
  position: relative;
  height: 50%;
  padding: 5vh;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  justify-items: center;
  align-items: center;
}

.icon-caption {
  margin-top: 5px;
  font-size: 0.6rem;
  font-weight: bold;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-style: italic;
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