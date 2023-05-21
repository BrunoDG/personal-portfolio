<template>
  <div class="flex flex-col gap-[2.5rem]">
    <!-- introduction section -->
    <div class="divCenter">
      <p
        id="landing_intro"
        ref="landingIntro"
        class="lg:text-xl text-md acrlyic w-auto text-center selector"
      ></p>
    </div>
    <!-- <section class="">
      <h1 class="text-4xl font-bold">Bruno Dias</h1>
      <h3 class="text-lg">Full-Stack Web and Game Developer</h3>
    </section> -->
    <section class="pt-2">
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        Professional Background
      </h2>
      <br />
      <p class="lg:text-lg text-sm text-justify leading-6">
        &nbsp;&nbsp;&nbsp;&nbsp; Senior Full-Stack developer capable of making
        websites and systems for the web, focusing on creating
        <strong>performance optimized, reusable and refactorable codes</strong>.
        Works as a web and game developer since 2012 and has worked for several
        companies with different sizes and cultures, from start-ups to
        multinationals.
      </p>
      <br />
      <p class="lg:text-lg text-sm text-justify leading-6">
        &nbsp;&nbsp;&nbsp;&nbsp; Always hungry for knowledge, passionate
        learner, collaborative individual and loves to discover and study newer
        technologies and how they can make the team's workflow faster, easier,
        more efficient and maintainable.
      </p>
    </section>
    <!-- info section -->
    <section class="">
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        Bio
      </h2>
      <br />
      <p class="lg:text-lg text-sm text-justify leading-6">
        &nbsp;&nbsp;&nbsp;&nbsp; Bruno has a strong passion on technology as a
        whole. Outside of programmimg, He has a hobby of collecting videogames
        and engaging with technology. He likes to tinker with electronics,
        Arduino, create his own MIDI controllers and also is a musician and a
        writer that not only writes technical articles, but science fiction
        books and tales as well.
      </p>
    </section>
    <!-- journey section -->
    <section class="">
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        Development Journey
      </h2>
      <br />
      <div class="flex flex-col gap-2">
        <!-- year 2010 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2010:</strong>
          &nbsp; Got his first development experience as an intern, working with
          Objective-C and iOS development
        </p>
        <!-- year 2012 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2012:</strong>
          &nbsp; Worked at EY (fka Ernst & Young Terco) as a trainee as a
          systems analyst, working with frontend and backend technologies such
          as Vanilla JS, jQuery, prototype.js, Twitter Bootstrap, Classic ASP
          and MS SQL Server 2012 R2
        </p>
        <!-- year 2014 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2014:</strong>
          &nbsp; Has his first Game Development experience as an internship,
          working for SENAI CTS Benfica at a simulation platform using Unity3D
          Game Engine, C#, PHP and MySQL
        </p>
        <!-- year 2016 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2016:</strong>
          &nbsp; Worked on a couple of indie mobile games using Unity3D and
          started working at Globosat with Python, Web, Mobile (using Java for
          Android) and Game Development (using Unity3D with VuForia for AR
          projects)
        </p>
        <!-- year 2017 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2017:</strong>
          &nbsp; Got his Bachelor in Computer Sciences at UERJ - Rio de Janeiro
          State University
        </p>
        <!-- year 2018 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2018:</strong>
          &nbsp; Started working at Tecgraf Institute / PUC-Rio using OpenGL and
          C++ for a legacy system, while creating unit and interface tests using
          Selenium and C#
        </p>
        <!-- year 2019 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2019:</strong>
          &nbsp; Started working at Bemobi to work on reverse engineering
          Unity3D android games and developed part of a legacy tool using Python
          + Django
        </p>
        <!-- year 2020 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2020:</strong>
          &nbsp; Moved to Florianópolis - Santa Catarina to work at CERTI
          Foundation to work as a Backend Developer, focused on OpenBIM projects
          using Angular.JS and Typescript. Also, helped development on 3D
          functionalities for the same platform using Three.JS and started
          development of the mobile app using the Flutter framework
        </p>
        <!-- year 2021 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2021:</strong>
          &nbsp; Started working as a Senior FullStack Developer for OASIS
          Ventures, based in Wyoming, USA. While leading a two-members team, he
          was tasked to develop with React, Typescript, Django, AWS, Kubernetes
          and GitLab
        </p>
        <!-- year 2022 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2022:</strong>
          &nbsp; Contracted as a game developer at EPRA Games and resumed his
          work with Unity3D and C#, as well as developing shaders using HLSL and
          ShaderLab
        </p>
        <!-- year 2023 -->
        <p class="lg:text-lg text-sm text-left">
          <strong>2023:</strong>
          &nbsp; Returned to Rio de Janeiro and started working as a Backend
          Typescript Developer for FS Studio, based in California, USA. Worked
          with a web3 game engine called Needle Engine, which uses Three.JS,
          Typescript and Unity3D as its main scene visualizer
        </p>
      </div>
    </section>
  </div>
</template>

<script>
import TypeIt from 'typeit';
import 'animate.css';
import { ref } from 'vue';

export default {
	data() {
		return {
			display: false
		};
	},
	setup() {
		const landingIntro = ref('');

		if (landingIntro.value !== '') {
			landingIntro.value === '';
		}
	},
	mounted() {
		new TypeIt('#landing_intro', {
			speed: 50,
			waitUntilVisible: true,
			startDelay: 2000,
			startDelete: true,
			// remove cursor when finished
			afterComplete: function (instance) {
				instance.destroy();
			}
		})
			.type(
				'Hi there! I am a Full-Stack Web and Game Developer based in Brazil'
			)
			.go();
	}
};
</script>

<style>
  .selector {
    background-color: var(--bg-sel);
  }

  .copyright {
    animation: fadeInLeft; /* referring directly to the animation's @keyframe declaration */
    animation-duration: 1s; /* don't forget to set a duration! */
    animation-delay: 3s;
  }

  /* @keyframes copyright {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
    visibility: visible;
  }
} */
</style>
