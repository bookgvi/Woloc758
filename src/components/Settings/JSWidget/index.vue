<script>
export default {
  data () {
    return {}
  },
  render (h) {
    const { routes } = this.$router.options
    return h('div', {
      style: {
        marginTop: '100px',
        color: 'grey'
      }
    }, [
      h('ul', 'Some element'),
      h('ul', this.drawAllRoutes(h, routes))
    ])
  },
  methods: {
    drawAllRoutes (h, obj) {
      return obj.map(elem => h('li', [(() => {
        if (elem.children) {
          return h('ul', [
            h('div', {
              style: {
                paddingTop: '10px',
                color: 'green',
                cursor: 'pointer'
              },
              on: {
                click: this.showHideSubMenu
              }
            }, elem.path),
            h('ul', {
              attrs: {
                id: elem.path
              },
              style: {
                display: 'none'
              }
            }, this.drawAllRoutes(h, elem.children))
          ])
        } else {
          return elem.path
        }
      })()]
      ))
    },
    showHideSubMenu (e) {
      const targetElem = document.getElementById(e.target.innerHTML)
      if (targetElem.style.display === 'none') {
        targetElem.style.display = 'block'
      } else {
        targetElem.style.display = 'none'
      }
    }
  }
}
</script>
