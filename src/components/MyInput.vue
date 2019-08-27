<script>
import { VCard, VCardText, VSheet, VTextField, VTreeview } from 'vuetify/lib';

export default {
  name: 'MyInput',
  props: {
    label: {
      default: 'Search...',
      type: String
    }
  },
  data: () => ({
    content: null,
    isFocused: false,
    isMenuActive: false,
    items: [
      {
        id: 1,
        name: 'Applications :',
        children: [
          { id: 2, name: 'Calendar : app' },
          { id: 3, name: 'Chrome : app' },
          { id: 4, name: 'Webstorm : app' }
        ]
      },
      {
        id: 5,
        name: 'Documents :',
        children: [
          {
            id: 6,
            name: 'vuetify :',
            children: [
              {
                id: 7,
                name: 'src :',
                children: [
                  { id: 8, name: 'index : ts' },
                  { id: 9, name: 'bootstrap : ts' }
                ]
              }
            ]
          },
          {
            id: 10,
            name: 'material2 :',
            children: [
              {
                id: 11,
                name: 'src :',
                children: [
                  { id: 12, name: 'v-btn : ts' },
                  { id: 13, name: 'v-card : ts' },
                  { id: 14, name: 'v-window : ts' }
                ]
              }
            ]
          }
        ]
      },
      {
        id: 15,
        name: 'Downloads :',
        children: [
          { id: 16, name: 'October : pdf' },
          { id: 17, name: 'November : pdf' },
          { id: 18, name: 'Tutorial : html' }
        ]
      },
      {
        id: 19,
        name: 'Videos :',
        children: [
          {
            id: 20,
            name: 'Tutorials :',
            children: [
              { id: 21, name: 'Basic layouts : mp4' },
              { id: 22, name: 'Advanced techniques : mp4' },
              { id: 23, name: 'All about app : dir' }
            ]
          },
          { id: 24, name: 'Intro : mov' },
          { id: 25, name: 'Conference introduction : avi' }
        ]
      }
    ],
    search: null
  }),
  computed: {
    directives() {
      return this.isFocused
        ? [
            {
              name: 'click-outside',
              value: this.blur,
              args: {
                closeConditional: this.closeConditional
              }
            }
          ]
        : undefined;
    }
  },
  mounted() {
    this.content = this.$refs.content;
  },
  methods: {
    blur() {
      console.log('bur');
      this.isMenuActive = false;
      this.isFocused = false;
      // this.$refs.input && this.$refs.input.blur();
    },
    closeConditional(e) {
      return (
        // Click originates from outside the menu content
        !!this.content &&
        !this.content.contains(e.target) &&
        // Click originates from outside the element
        !!this.$el &&
        !this.$el.contains(e.target) &&
        e.target !== this.$el
      );
    },
    genInput() {
      return this.$createElement(VSheet, { staticClass: 'mb-1' }, [
        this.genTextFieldSlot()
      ]);
    },
    genTextFieldSlot() {
      return this.$createElement(VTextField, {
        on: {
          focus: this.onClick,
          input: val => {
            this.search = val;
          }
        },
        ref: 'input',
        props: {
          'prepend-inner-icon': 'search',
          clearable: true,
          'hide-details': true,
          label: this.label,
          'single-line': true,
          solo: true /* ,
          value: this.search*/
        }
      });
    },
    genTreeviewSlot() {
      return this.$createElement(VTreeview, {
        staticClass: 'overflow-y-auto',
        props: {
          items: this.items,
          search: this.search
        }
      });
    },
    genMenuSlot() {
      return this.$createElement(
        VCard,
        {
          staticClass: 'absolute w-full',
          directives: [{ name: 'show', value: this.isMenuActive }]
        },
        [this.genMenuContent()]
      );
    },
    genMenuContent() {
      return this.$createElement(
        VCardText,
        {
          staticClass: 'pr-0 overflow-y-auto'
        },
        [this.genMenuContentSlot()]
      );
    },
    genMenuContentSlot() {
      return this.$createElement(
        'div',
        {
          ref: 'content'
        },
        [this.genTreeviewSlot()]
      );
    },
    onClick() {
      this.isFocused = true;
      this.isMenuActive = true;
    }
  },
  render(h) {
    return h(
      'div',
      {
        directives: this.directives,
        class: 'relative my-custom-input'
      },
      [this.genInput(), this.genMenuSlot()]
    );
  }
};
</script>

<style lang="scss" scoped>
.relative {
  position: relative;
}

.overflow-y-auto {
  overflow-y: auto;
}

.w-full {
  width: 100%;
}

.absolute {
  position: absolute;
}

.h-max-300 {
  max-height: 300px;
}
</style>
