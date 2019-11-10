<script>
export default {
  render (h) {
    const routes = this.$router.options.routes.filter(item => item.path !== '/login' && item.path !== '*')
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
                  'q-py-none': true,
                  'text-primary': true
                },
                style: {
                  cursor: 'pointer'
                },
                attrs: {
                  label: this.tagData(elem.path, '/', 'Root'),
                  noCaps: true,
                  flat: true
                },
                on: {
                  click: this.showHideSubMenu
                }
              }),
              h('span', {
                attrs: {
                  id: this.tagData(elem.path, '/', 'Root'),
                },
                style: {
                  display: 'none'
                }
              }, this.drawAllRoutes(h, elem.children))
            ]
          } else if (elem.path !== '') {
            return h('span', {
              style: {
                width: '100%'
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
    },
    tagData (value, orig, newValue) {
      return value === orig ? newValue : value
    }
  }
}
</script>
