<template>
  <div class="resume" id="resume2">
    <div class="personal_info_section">
      <div class="headline">
        <span>{{ person.name.first }} {{ person.name.middle }}</span>
        <span class="uppercase">{{ person.name.last }}</span> -
        <span class="about-txt">{{ person.about }}</span>
        <div class="headline-title">
          <span>{{ person.title }}</span>
        </div>
      </div>

      <div class="social-container">
        <a v-if="person.contact.website" :href="person.contact.website" class="external-link">
          <span class="block-marged txt-full-white">
            <i class="fa fa-globe contact-icon"></i>
            {{ person.contact.website }}
          </span>
        </a>

        <a v-if="person.contact.linkedin" :href="contactLinks.linkedin" class="external-link">
          <i class="fa fa-linkedin contact-icon"></i>
          <span class="block-marged txt-full-white">{{ person.contact.linkedin }}</span>
        </a>
      </div>
    </div>

    <div class="professional_section">
      <div class="experience-section section">
        <div class="icon">
          <i class="material-icons small-icon">work</i>
          <span class="section-headline">{{ lang.experience }}</span>
        </div>

        <div class="section-content">
          <a
            v-for="(experience, index) in person.experience"
            :key="index"
            class="section-content__item"
            :href="experience.website"
          >
            <span class="section-content__header">{{ experience.position }}</span>
            <span class="section-content__subheader">{{ experience.company }}</span>
            <div class="section-content__text--light">{{ experience.timeperiod }}</div>
            <span class="section-content__text">
              <vue-markdown>{{ experience.description }}</vue-markdown>
            </span>
          </a>
        </div>
      </div>

      <div v-if="person.projects" class="projects-section section">
        <div class="icon">
          <i class="material-icons">code</i>
          <span class="section-headline">{{ lang.projects }}</span>
        </div>

        <div class="section-content">
          <a
            v-for="(project, index) in person.projects"
            :key="index"
            class="section-content__item"
            :href="project.url"
          >
            <span class="section-content__header">{{ project.name }}</span>
            <span class="section-content__subheader">{{ project.platform }}</span>
            <span class="section-content__text">{{ project.description }}</span>
            <span class="section-content__text--light">{{ project.url }}</span>
          </a>
        </div>
      </div>

      <div class="education-section section">
        <div class="icon">
          <i class="material-icons">school</i>
          <span class="section-headline">{{ lang.education }}</span>
        </div>

        <div class="section-content">
          <a
            v-for="(education, index) in person.education"
            :key="index"
            class="section-content__item"
            :href="education.website"
          >
            <span class="section-content__header">{{ education.school }}</span>
            <span class="section-content__subheader">{{ education.degree }}</span>
            <span class="section-content__text--light">{{ education.timeperiod }}</span>
            <span class="section-content__text">{{ education.description }}</span>
          </a>
        </div>
      </div>

      <div v-if="person.contributions" class="contributions-section section">
        <div class="icon">
          <i class="fa fa-heart font-awesome-icons"></i>
          <span class="section-headline">{{lang.contributions}}</span>
        </div>

        <div class="section-content-grid">
          <a
            v-for="(contribution, index) in person.contributions"
            :key="index"
            :href="contribution.url"
            class="section-content__item-grid"
          >
            <span class="section-content__header">{{ contribution.name }}</span>
            <span class="section-content__text">{{ contribution.description }}</span>
            <span
              class="section-content__text--light"
              style="word-break: break-all;"
            >{{ contribution.url }}</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import VueMarkdown from "vue-markdown";
import { getVueOptions } from "./options";

Vue.component("vue-markdown", VueMarkdown);

const name = "creative";

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less" scoped>
@accent-color: #009d3f;

.resume {
  display: flex;
  flex-direction: column;
  position: relative;

  font-family: "Roboto" !important;
  font-size: 0.9em;
}

.personal_info_section {
  flex: 1;
  padding: 15px 30px;
  text-align: left;

  display: flex;
  flex-direction: row;
  justify-content: space-between;

  color: #ffffff;
  color: rgba(255, 255, 255, 0.59);
  background-color: @accent-color;
}

.professional_section {
  display: flex;
  flex-direction: column;
  padding: 30px;

  flex: 0;
}

a {
  color: inherit;
  cursor: pointer;
  text-decoration-line: none;

  &:visited {
    color: inherit;
  }
}

.material-icons {
  color: @accent-color;
  position: relative;
  top: 5px;
}

.font-awesome-icons {
  color: @accent-color;
  font-size: 1.3em;
  margin-right: 6px;
}

.small-icon {
  top: 2.5px;
  font-size: 1.4em;
}

.contact-icon {
  color: white;
  font-size: 1.5em;
  margin-right: 10px;

  top: 2px;
  position: relative;
}

.contact-icon-svg {
  margin-top: -2.5px;
  margin-right: 10px;

  transform: scale(1);

  top: 5px;
  position: relative;
}

.contact-icon-svg path {
  fill: white;
}

.external-link {
  display: block;
  margin-bottom: 5px;
}

.block-marged {
  margin-top: 15px;
  margin-bottom: 15px;
}

.about-txt {
  color: rgba(255, 255, 255, 0.59);
}

.headline {
  color: white;
  font-size: 1.3em;
  font-weight: bold;
}

.headline-title {
  color: white;
  font-size: 0.9em;
  font-weight: normal;
}

.txt-full-white {
  color: white;
}

.uppercase {
  text-transform: uppercase;
}

.section-headline {
  color: @accent-color;
  display: inline-block;
  font-size: 1.2em;
  margin-left: 5px;
}

.section-content {
  margin-top: 10px;
  padding-left: 32px;
}

.section-content__item {
  display: block;
  margin-bottom: 10px;
}

.section-content__item-grid {
  flex: 1 1 0;

  margin-bottom: 10px;
  padding-right: 10px;
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;

  margin-top: 10px;
  margin-bottom: 10px;
}

.grid-item {
  padding-right: 20px;
}

.section-content__header {
  display: block;

  font-size: 1.1em;
  font-weight: 500;
}

.squarred-grid-item {
  display: block;
  position: relative;

  border: 1px solid white;

  background-color: white;
  color: @accent-color;

  margin-top: 5px;
  padding: 5px;

  transition: 0.5s;

  .skill-name {
    z-index: 1;
  }

  &:hover {
    background-color: @accent-color;
    color: white;
    transition: 0.5s;
  }
}

.section-content__subheader {
  display: block;
  font-weight: 400;
}

.section-content__text {
  display: block;
  font-weight: 300;
}

.section-content__text--light {
  color: rgba(0, 0, 0, 0.42);
  font-weight: 300;
}

.section-content__subheader,
.section-content__text--light,
.section-content__header {
  line-height: 1.5em;
}

.section {
  margin-top: 10px;
  margin-bottom: 10px;
}

.lang-icon {
  color: rgba(0, 0, 0, 0.72);
  font-size: 3em;

  &:hover {
    color: @accent-color;
  }
}

.hobbies-container {
  margin-top: 30px;
}

.hobbies-content {
  display: flex;
  flex-direction: column;
}

.hobby-item {
  display: grid;
  grid-template-columns: 30px auto;

  color: rgba(255, 255, 255, 0.6);

  margin-right: 25px;
  margin-bottom: 10px;

  transition: 0.5s;

  &:hover {
    color: rgba(255, 255, 255, 0.8);
    transition: 0.5s;
  }
}

.hobby-item__icon {
  font-size: 1.3em;
}

.hobby-item__icon-label {
  top: 2.5px;
  position: relative;
}

.subheadline {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1.2em;

  display: block;
  margin-bottom: 10px;
}
</style>
