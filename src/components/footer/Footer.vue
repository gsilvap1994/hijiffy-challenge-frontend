<template>
  <footer class="footer">
    <div class="footer__top">
      <div class="community">
        <strong>
          <a href="#">
            Community
          </a>
        </strong>
      </div>
      <div class="company">
        <strong>
          <a href="https://hijiffy.com/pt/" target="_blank" rel="noopener noreferrer">
            Company
          </a>
        </strong>
      </div>
      <div class="logo">
        <img :src="require(`@/assets/images/logo/logo.png`)" alt="Hijiffy company logo">
      </div>
      <div class="help-desk">
        <strong>
          <a href="#">
            Help Desk
          </a>
        </strong>
      </div>
      <div class="blog">
        <strong>
          <a href="https://medium.com/hijiffy" target="_blank" rel="noopener noreferrer">
            Blog
          </a>
        </strong>
      </div>
    </div>
    <div class="footer__bottom">
      <div class="social-media">
        <a 
          class="media linkedin"
          href="https://www.linkedin.com/company/hijiffy/" 
          target="_blank"
          rel="noopener noreferrer"
        >
          <img :src="require(`@/assets/images/social-media/linkedin.png`)" alt="Hijiffy Linkedin Profile link">
        </a>
        <a 
          class="media facebook"
          href="https://www.facebook.com/hijiffy/"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img :src="require(`@/assets/images/social-media/facebook.png`)" alt="Hijiffy Facebook Profile link">
        </a>
        <a 
          class="media twitter"
          href="https://twitter.com/hijiffy"
          rel="noopener noreferrer"
          target="_blank"
        >
          <img :src="require(`@/assets/images/social-media/twitter.png`)" alt="Hijiffy Twitter Profile link">
        </a>
        <a
          class="media youtube"
          href="https://www.youtube.com/channel/UCjNTWDNTK_kUBrIOmuYuERA"
          rel="noopener noreferrer"
          target="_blank"
        >
          <img :src="require(`@/assets/images/social-media/youtube.png`)" alt="Hijiffy Youtube Profile link">
        </a>
      </div>
    </div>
    <div class="footer__copyright">
      <span>
        © HiJiffy 2021. We love our users.
      </span>
    </div>
  </footer>
  
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
  .footer {
    background-color: $light-primary-light-grey;

    &__top {
      display: flex;
      justify-content: space-evenly;
      padding: 2rem 0 2rem;
      margin: 0 2rem 2rem;
      border-bottom: 1px solid #000;
      a {
        color: #000;
        text-decoration: none;
      }

      .logo img {
        max-width: 52px;
      }
    }

    &__bottom {
      margin: 0 2rem 2rem;
      display: flex;
      justify-content: center;
      align-items: center;

      .social-media {
        display: flex;
        .media {
          margin: 0 1rem;
          width: 36px;
          height: 36px;
          display: flex;
          align-items: center;
          justify-content: center;
          border-radius: 1000px;

          &.linkedin {
            background-color: #0077b5;
          }

          &.facebook {
            background-color: #385899;
          }

          &.twitter {
            background-color: #1DA1F2;
          }

          &.youtube {
            background-color: #FF0000
          }

          img {
            width: 50%;
          }
        }
      }
    }

    &__copyright {
      color: #000;
      text-align: center;
      margin-bottom: 0.5rem;
      font-weight: 100;
    }
  }
</style>