<template>
  <div>
    <Loader />
    <section class="sign-in-page">
      <div id="container-inside">
        <div id="circle-small"></div>
        <div id="circle-medium"></div>
        <div id="circle-large"></div>
        <div id="circle-xlarge"></div>
        <div id="circle-xxlarge"></div>
      </div>
      <b-container class="container p-0">
        <div class="row no-gutters">
          <div class="col-md-6 text-center pt-5">
            <div class="sign-in-detail">
              <div class="item tracking-in-expand content-padding">
                <img src="../../assets/images/pichonkun.gif" class="logo-size" alt="logo">
                  <div class="text-size">
                    <h4 class="text-white">DEDE Over Time Request</h4>
                    <p>Please Sign In to access over time request.</p>
                  </div>
              </div>
            </div>
          </div>
          <div class="col-sm-6 bg-white pt-5">
            <div class="sign-in-from">
              <router-view></router-view>
            </div>
          </div>
        </div>
      </b-container>
    </section>
  </div>
</template>
<script>
import Loader from '../../components/socialvue/loader/Loader'
import logo from '../../assets/images/logo-white.png'
import { socialvue } from '../../config/pluginInit'
import bgImage from '../../assets/images/login/login-2.jpg'
export default {
  name: 'AuthLayout1',
  components: {
    Loader
  },
  mounted () {
    socialvue.index()
  },
  data () {
    return {
      slickOptions: {
        slidesToShow: 1,
        arrows: false
      },
      logo: logo,
      bgImageURL: bgImage
    }
  }
}
</script>

<style lang="css" scoped>
.logo-size{
  width: 9rem ;
  height: 11rem;
}
.content-padding{
  width: -10rem;
}
.text-size{
  font-size:1rem;
}
.tracking-in-expand {
  -webkit-animation: tracking-in-expand 0.7s cubic-bezier(0.215, 0.610, 0.355, 1.000) both;
  animation: tracking-in-expand 0.7s cubic-bezier(0.215, 0.610, 0.355, 1.000) both;
}
@-webkit-keyframes tracking-in-expand {
  0% {
    letter-spacing: -0.5em;
    opacity: 0;
  }
  40% {
    opacity: 0.6;
  }
  100% {
    opacity: 1;
  }
}
@keyframes tracking-in-expand {
  0% {
    letter-spacing: -0.5em;
    opacity: 0;
  }
  40% {
    opacity: 0.6;
  }
  100% {
    opacity: 1;
  }
}
</style>
