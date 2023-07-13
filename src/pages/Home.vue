<template>
  <div class="home">
    <div class="content">
      <h1 class="website-title">
        <b>{{ 'Evan ' }}</b>
        <span class="last-name">Welsh</span>
      </h1>
      <div class="social-links">
        <p>
          Full-Stack Developer @{{ ' ' }}
          <a
            href="https://modernhealth.com"
            class="job"
            rel="noreferrer"
            target="_blank"
            >Modern Health</a
          >
        </p>
        <p class="location">San Francisco Bay Area</p>

        <div>
          <b-row>
            <b-col cols="auto">
              <bubble header="email" link="mailto:contact@evanwelsh.com">
                <mail-icon size="2x" />
              </bubble>
            </b-col>

            <b-col cols="auto">
              <bubble
                header="linkedin"
                link="https://www.linkedin.com/in/evan-welsh-291577141/"
              >
                <linkedin-icon size="2x" />
              </bubble>
            </b-col>

            <b-col cols="auto">
              <bubble link="https://github.com/ewlsh/" header="github">
                <github-icon size="2x" />
              </bubble>
            </b-col>

            <b-col cols="auto">
              <bubble
                header="gnome gitlab"
                link="https://gitlab.gnome.org/ewlsh"
              >
                <GnomeLogo width="32" height="32" />
              </bubble>
            </b-col>
          </b-row>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
#moreInfoModal {
  .modal-footer {
    border: none;
    padding-top: 0;
  }

  .modal-header {
    padding-bottom: 0;
    border: none;
  }
}
</style>

<style lang="scss" scoped>
@import '../scss/variables';

.home {
  font-size: 1.25rem;
  color: #fefefe;
  background-color: #000;
  min-height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  //justify-content: center;
}

.content {
  margin-left: max(40px, 10%);
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.job {
  color: $primary;
  text-decoration: underline;
  font-weight: bold;
  white-space: nowrap;
}

.projects {
  margin: 1rem;
}

.website-title {
  padding-top: 5%;
  font-weight: 700;
  font-size: 5rem;
  color: #fefefe;
  a {
    color: #fefefe;
    text-decoration: none;

    &:hover {
      text-decoration: none;
    }
  }
}

.website-subtitle {
  padding-bottom: 1%;
  text-align: left;
  font-family: 'Merriweather', 'serif';
  font-size: 0.75rem;
  color: #fefefe;
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.5s;
  z-index: 2001;
}
.modal-enter,
.modal-leave-to {
  opacity: 0;
}

.social-link {
  color: #fff;
}

.website-title {
  margin: 0;
  font-size: 3rem;
  text-align: left;
  font-family: 'Raleway';

  .last-name {
    color: $primary;
  }
}

.loading {
  text-align: center;
  margin-top: 30px;
}

.about-sidebar {
  background-color: #000;
  padding: 2rem;
  height: 100%;
  width: 100%;
}

@media (max-width: 767px) {
  .about-img {
    margin-bottom: 2rem;
    padding-right: 10vw;
    padding-left: 10vw;
  }

  .about-img-container {
    margin-left: auto;
    margin-right: auto;
  }
}

.social-links {
  .bubble {
    margin: 3px;
  }
}

.about-img {
  max-width: 100%;
  max-height: 40vh;
}

.modal-body-header {
  padding-top: 1rem;
}

.modal-image {
  width: 100%;
  height: 5rem;
  object-fit: cover;
}

.header {
  margin: 2rem 0;
  font-size: 2.5rem;
  font-weight: 600;
  text-align: left;
}
</style>

<script>
import Component from 'vue-class-component';
import Vue from 'vue';
import PortfolioHeader from '@/components/PortfolioHeader';
import ProjectCard from '@/components/ProjectCard';
import SocialMediaBubble from '@/components/SocialMediaBubble';

import {
  MailIcon,
  HomeIcon,
  GithubIcon,
  LinkedinIcon,
  InstagramIcon,
  TwitterIcon
} from 'vue-feather-icons';

import GnomeLogo from '@/assets/GnomeLogo.svg?inline';

@Component({
  components: {
    PortfolioHeader,
    ProjectCard,
    MailIcon,
    HomeIcon,
    GithubIcon,
    TwitterIcon,
    InstagramIcon,
    LinkedinIcon,
    bubble: SocialMediaBubble,
    GnomeLogo
  }
})
export default class Home extends Vue {
  projects = null;
  isShowing = false;
  modalProject = null;

  created() {
    import('@/assets/projects.json')
      .then(({ default: results }) => {
        this.projects = [...Array.from(results.projects)];
      })
      .catch(err => {
        console.error(err);
      });
  }

  displayMoreInfoModal(projectId) {
    if (this.projects) {
      this.modalProject = Array.from(this.projects).find(
        v => v.id === projectId
      );
      this.$refs.moreInfoModal.show();
    }
  }
}
</script>
