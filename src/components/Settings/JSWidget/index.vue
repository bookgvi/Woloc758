<script>
export default {
  data () {
    return {}
  },
  render (h) {
    const routes = this.$router.options.routes.filter(item => item.path !== '*')
    console.log(routes)
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
      return obj.map(elem => {
        if (!elem.path) return
        return h('li', [(() => {
          if (elem.children) {
            return [
              h('q-btn', {
                class: {
                  'q-mt-sm': true,
                  'q-py-none': true,
                  'q-pl-none': true
                },
                style: {
                  paddingTop: '10px',
                  cursor: 'pointer'
                },
                attrs: {
                  label: elem.path,
                  noCaps: true,
                  flat: true
                },
                on: {
                  click: this.showHideSubMenu
                }
              }),
              h('span', {
                class: {
                  'q-ma-none': true,
                  'q-pt-sm': true
                },
                attrs: {
                  id: elem.path
                },
                style: {
                  display: 'none'
                }
              }, this.drawAllRoutes(h, elem.children))
            ]
          } else if (elem.path !== '') {
            return h('span', {
              style: {
                width: '100px'
              },
            }, elem.path)
          }
        })()]
        )
      })
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
