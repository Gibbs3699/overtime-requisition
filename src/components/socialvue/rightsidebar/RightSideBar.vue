<script>
import loader from '../../../assets/images/logo.png'
import darkLoader from '../../../assets/images/logo-white.png'
import { mapActions } from 'vuex'
export default {
  name: 'RightSideBarStyle1',
  data () {
    return {
      miniClass: '',
      // showChat: true,
      animated: { enter: 'zoomIn', exit: 'zoomOut' },
      animateClass: [
        { value: { enter: 'zoomIn', exit: 'zoomOut' }, text: 'Zoom' },
        { value: { enter: 'fadeInUp', exit: 'fadeOutDown' }, text: 'Fade' },
        { value: { enter: 'slideInLeft', exit: 'slideOutRight' }, text: 'Slide' },
        { value: { enter: 'rotateInDownLeft', exit: 'rotateOutDownLeft' }, text: 'Roll' }
      ],
      logo: loader,
      rtl: false,
      users: [
        {
          img: require('../../../assets/images/user/01.jpg'),
          name: 'Anna Sthesia',
          time: 'Just now'
        },
        {
          img: require('../../../assets/images/user/02.jpg'),
          name: 'Paul Molive',
          time: 'Admin'
        },
        {
          img: require('../../../assets/images/user/03.jpg'),
          name: 'Anna Mull',
          time: 'Admin'
        },
        {
          img: require('../../../assets/images/user/04.jpg'),
          name: 'Paige Turner',
          time: 'Admin'
        },
        {
          img: require('../../../assets/images/user/05.jpg'),
          name: 'Bob Frapples',
          time: 'Admin'
        },
        {
          img: require('../../../assets/images/user/06.jpg'),
          name: 'Barb Ackue',
          time: 'Admin'
        },
        {
          img: require('../../../assets/images/user/07.jpg'),
          name: 'Greta Life',
          time: 'Admin'
        },
        {
          img: require('../../../assets/images/user/08.jpg'),
          name: 'ra Membrit',
          time: 'Admin'
        },
        {
          img: require('../../../assets/images/user/09.jpg'),
          name: 'Pete Sariya',
          time: 'Admin'
        },
        {
          img: require('../../../assets/images/user/10.jpg'),
          name: 'ra Membrit',
          time: 'Admin'
        }
      ]
    }
  },
  props: {
    toggleClass: { type: String, default: '' }
  },
  computed: {
    hasIconSlot () {
      return !!this.$slots.icon
    },
    hasOpenIconSlot () {
      return !!this.$slots.openIcon
    },
    hasCloseIconSlot () {
      return !!this.$slots.closeIcon
    }
  },
  methods: {
    toggleMini () {
      this.rightSideBarMini = !this.rightSideBarMini
      this.checkRightSideBar()
    },
    checkRightSideBar () {
      console.log(this.rightSideBarMini)
      if (this.rightSideBarMini) {
        this.miniClass = 'right-sidebar'
      } else {
        this.miniClass = ''
      }
    },
    themeMode (mode) {
      this.dark = mode
      this.modeChange({ rtl: this.rtl, dark: mode })
      if (mode) {
        this.logo = darkLoader
      } else {
        this.logo = loader
      }
      this.$emit('onLogo', this.logo)
    },
    rtlChange (mode) {
      this.rtl = mode
      this.modeChange({ rtl: mode, dark: this.darkMode })
      if (this.darkMode) {
        this.logo = darkLoader
      } else {
        this.logo = loader
      }
    },
    reset () {
      this.animated = { enter: 'zoomIn', exit: 'zoomOut' }
      this.themeMode(false)
      this.rtlChange(false)
    },
    ...mapActions({
      modeChange: 'Setting/layoutModeAction'
    })
  }
}
</script>
