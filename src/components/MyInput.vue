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
  data: () => {
    return {
      search: null
    };
  },
  methods: {
    genContent() {
      return [this.genDefaultSlot()];
    },
    genDefaultSlot() {
      return this.$createElement(VSheet, {}, [
        this.genTextFieldSlot(),
        this.genMenuSlot()
      ]);
    },
    genTextFieldSlot() {
      return this.$createElement(VTextField, {
        staticClass: 'mb-1',
        on: {
          input: val => {
            this.search = val;
          }
        },
        directives: [
          {
            name: 'model',
            value: this.search
          }
        ],
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
      return this.$createElement(VTreeview, {});
    },
    genMenuSlot() {
      return this.$createElement(VCard, { staticClass: 'absolute w-full' }, [
        this.genMenuContent()
      ]);
    },
    genMenuContent() {
      return this.$createElement(
        VCardText,
        {
          staticClass: 'pr-0 overflow-y-auto'
        },
        []
      );
    }
  },
  render(h) {
    return h('div', { class: 'relative my-custom-input' }, this.genContent());
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
