# jianghujs-snippets README

快捷生成 Jianghujs 代码片段

## html.code-snippets

### jh-doUiAction

```js
async doUiAction(uiActionId, uiActionData) {
    try {
    switch (uiActionId) {
        default:
        console.error("[doUiAction] uiActionId not find", {uiActionId});
        break;
    }
    } catch (error) {
    window.jhMask && window.jhMask.hide();
    throw error;
    } finally {
    window.jhMask && window.jhMask.hide();
    }
},
```

### jh-jianghuAxios

```js
const { rows, count } = (
  await window.jianghuAxios({
    data: {
      appData: {
        pageId: "$1",
        actionId: "$2",
        actionData: {},
        where: {},
        whereLike: {},
        whereIn: {},
        orderBy: [],
      },
    },
  })
).data.appData.resultData;
```

### jh-table

```html
<v-data-table
  :headers="headers"
  :items="tableDataComputed"
  :search="searchInput"
  :footer-props="{ itemsPerPageOptions: [20, 50, 200, -1], itemsPerPageText: '每页', itemsPerPageAllText: '所有'}"
  :items-per-page="-1"
  mobile-breakpoint="0"
  :loading="isTableLoading"
  checkbox-color="success"
  :class="{'zebraLine': true }"
  fixed-header
  class="jh-fixed-table-height elevation-0 mt-0 mb-xs-4"
>
  <!-- 表格操作按钮 -->
  <template v-slot:item.action="{ item }">
    <!-- pc端 -->
    <template v-if="!isMobile">
      <span
        role="button"
        class="success--text font-weight-medium font-size-2 mr-2"
        @click="doUiAction('viewRecordHistory', item)"
      >
        <v-icon size="16" class="success--text">mdi-eye-outline</v-icon>xxx
        <span v-if="item.count > 0" style="color: red">({{item.count}})</span>
      </span>
    </template>
    <!-- 手机端 -->
    <v-menu offset-y v-if="isMobile">
      <template v-slot:activator="{ on, attrs }">
        <span
          role="button"
          class="success--text font-weight-medium font-size-2"
          v-bind="attrs"
          v-on="on"
        >
          <v-icon size="20" class="success--text">mdi-chevron-down</v-icon>操作
        </span>
      </template>
      <v-list dense>
        <v-list-item @click="doUiAction('viewRecordHistory', item)">
          <v-list-item-title
            >xxx<span v-if="item.count > 0" style="color: red"
              >({{item.count}})</span
            ></v-list-item-title
          >
        </v-list-item>
      </v-list>
    </v-menu>
  </template>
  <!-- 没有数据 -->
  <template v-slot:loading>
    <div class="jh-no-data">数据加载中</div>
  </template>
  <template v-slot:no-data>
    <div class="jh-no-data">暂无数据</div>
  </template>
  <template v-slot:no-results>
    <div class="jh-no-data">暂无数据</div>
  </template>
  <!-- 表格分页 -->
  <template v-slot:footer.page-text="pagination">
    <span>{{pagination.pageStart}}-{{pagination.pageStop}}</span>
    <span class="ml-1">共{{pagination.itemsLength}}条</span>
  </template>
</v-data-table>
```

### jh-drawer

```html
<v-navigation-drawer
  v-model="isPageDrawerShown"
  :permanent="isPageDrawerShown"
  fixed
  temporary
  right
  width="80%"
  class="elevation-24"
>
  $1
  <v-btn
    elevation="0"
    color="success"
    fab
    absolute
    top
    left
    small
    tile
    class="drawer-close-float-btn"
    @click="isPageDrawerShown = false"
  >
    <v-icon>mdi-close</v-icon>
  </v-btn>
</v-navigation-drawer>
```

### jh-header

```html
<!-- 头部内容 >>>>>>>>>>>>> -->
<div class="jh-page-second-bar px-3 px-sm-8">
    <v-row class="align-center" no-gutters>
    <v-col cols="12" sm="12" md="4" xl="3" :cols="12" :sm="6" :md="4" >
        <div class="py-4 text-body-1 font-weight-bold align-center d-flex align-center">$1
        <!-- 帮助页按钮 -->
        <v-icon size="15" class="black--text ml-1" @click="isHelpPageDrawerShown = true">mdi-help-circle</v-icon>
        </div>
    </v-col>
    <!-- 自定义搜索内容 -->
    <v-spacer ></v-spacer>
    <!-- 服务端搜索 -->
    <v-col cols="12" xs="12" sm="12" md="8" xl="9" class="pl-md-2 mb-2 mb-md-0" >
        <v-row class="jh-backend-form-container justify-end py-md-3" no-gutters>
        <div class="jh-backend-search-btn ml-2">

        </div>
        </v-row>
    </v-row>
</div>
<!-- <<<<<<<<<<<<< 头部内容 -->
```

## javascript.code-snippets

### jh-head

```js
headContent: [
    { tag: 'jh-page-title', value: "页面访问日志", attrs: { cols: 12, sm: 6, md: 4 }, helpBtn: true, slot: [] },
    { tag: 'v-spacer' },
    {
      tag: 'jh-search',
      value: [
        { tag: 'v-select', attrs: { vModel: 'logFileSelected', items: 'constantCollection.logFile', prefix: '文件：', hideDetails: true } },
      ],
      searchBtn: true
    }
  ],
```

### jh-content

```js
pageContent: [
  {
    tag: "v-col",
    attrs: { cols: 12 },
    value: [
      /*html*/ `
        $1
        `,
    ],
  },
];
```

### jh-table

```js
{
      tag: 'jh-table',
      attrs: {},
      colAttrs: { clos: 12 },
      cardAttrs: { class: 'rounded-lg elevation-0' },
      headActionList: [
        { tag: 'v-btn', value: '新增', attrs: { small: true, color: 'success', '@click': 'doUiAction("startCreateItem")' } },
        { tag: 'v-spacer' },
        {
          tag: 'v-col',
          attrs: { cols: '12', sm: '6', md: '2', class: 'pa-0' },
          value: [
            { tag: 'v-text-field', attrs: { prefix: '筛选', 'v-model': 'searchInput', class: 'jh-v-input', ':dense': true, ':filled': true, ':single-line': true } },
          ],
        }
      ],
      value: [
         /*html*/`
         `
      ],
      rowActionList: [
      ],
}
```

### jh-drawer

```js
{
    tag: 'jh-drawer',
    key: "$1",
    attrs: {},
    title: '$2',
    headSlot: [
    { tag: 'v-spacer' }
    ],
    contentList: [
    {
        "label": "",
        "type": "form",
        "formItemList": [
            {
                "label": "初始密码*必填",
                "model": "$1.clearTextPassword",
                "tag": "v-text-field",
                "attrs": {},
                "rules": "validationRules.requireRules"
            }
        ],
        action: [
            { tag: 'v-btn', value: '保存', attrs: { small: true, class: 'ml-2', color: 'success', '@click': "doUiAction('resetPassword')" } },
            ]
        }
    ]
}
```

### dataExpression

```js
dataExpression: {
    appInfo: 'window.appInfo',
},
```
