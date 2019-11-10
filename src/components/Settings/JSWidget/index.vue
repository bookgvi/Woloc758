<script>
export default {
  data () {
    return {}
  },
  render (h) {
    const routes = this.$router.options.routes.filter(item => item.path !== '*')
    return h('div', {
      style: {
        marginTop: '100px',
        color: 'grey'
      }
    }, [
      h('div', 'Some element'),
      h('div', this.drawAllRoutes(h, routes))
    ])
  },
  methods: {
    drawAllRoutes (h, obj) {
      return obj.map(elem => h('li', [(() => {
        if (elem.children) {
          return h('div', [
            h('q-btn', {
              class: {
                'bg-primary': true
              },
              style: {
                paddingTop: '10px',
                color: 'white',
                cursor: 'pointer'
              },
              attrs: {
                label: elem.path,
                noCaps: true
              },
              on: {
                click: this.showHideSubMenu
              }
            }),
            h('ul', {
              attrs: {
                id: elem.path
              },
              style: {
                display: 'none'
              }
            }, this.drawAllRoutes(h, elem.children))
          ])
        } else if (elem.path !== '') {
          return h('div', {
            style: {
              width: '100px'
            },
          }, elem.path)
        }
      })()]
      ))
    },
    showHideSubMenu (e) {
      const targetElem = document.getElementById(e.target.innerText)
      if (targetElem.style.display === 'none') {
        targetElem.style.display = 'block'
      } else {
        targetElem.style.display = 'none'
      }
    }
  }
}
</script>
