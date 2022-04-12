<template>
  <a-cascader
    :options="options"
    v-model="valueOfCascader"
    style="width: 100%"
    @change="onChange"
  >
    <template slot="displayRender" slot-scope="{ labels, selectedOptions }">
      <span v-for="(label, index) in labels" :key="selectedOptions[index].value">
        <span v-if="index === labels.length - 1">
          {{ label }} (<a @click="e => handleAreaClick(e, label, selectedOptions[index])">{{
            selectedOptions[index].code
          }}</a
          >)
        </span>
        <span v-else @click="onChange"> {{ label }} / </span>
      </span>
    </template>
  </a-cascader>
</template>
<script>
export default {
  data() {
    return {
      valueOfCascader : ['zhejiang', 'hangzhou', 'xihu'],
      options: [
        {
          value: 'zhejiang',
          label: 'Zhejiang',
          children: [
            {
              value: 'hangzhou',
              label: 'Hangzhou',
              children: [
                {
                  value: 'xihu',
                  label: 'West Lake',
                  code: 752100,
                },
              ],
            },
          ],
        },
        {
          value: 'jiangsu',
          label: 'Jiangsu',
          children: [
            {
              value: 'nanjing',
              label: 'Nanjing',
              children: [
                {
                  value: 'zhonghuamen',
                  label: 'Zhong Hua Men',
                  code: 453400,
                },
              ],
            },
          ],
        },
      ],
    };
  },
  methods: {
    onChange() {
      console.log(this.valueOfCascader);
    },
    handleAreaClick(e, label, option) {
      e.stopPropagation();
      console.log('clicked', label, option);
    },
  },
};
</script>
