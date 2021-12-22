# 问题记录

## 一、vue1.0和vue2.0差异


#### 1、添加搜索

- 1.0 直接使用filterBy 加上索引条件即可
```
<tr v-for="(index,entry) in dataList | filterBy searchKey">
```
- 2.0 需要实现一个索引函数
```html
<tr v-for="(person, index) in filterdPeople ">
```
```javascript
filterdPeople: function(){
    var self = this;
    return self.people.filter(function(people){
        return people.name.indexOf(self.searchData) !== -1
    })
```

 #### 2、vue2.0 v-for语句index在后面，1.0在前面
```html
<!-- vue2.0 index在后面-->
<tr v-for="(person, index) in filterdPeople ">
```
```html
<!-- vue1.0 index在前面-->
<tr v-for="(index, person) in filterdPeople ">
```
 #### 3、vue2.0组件模板必须只有一个根节点，vue1.0可以多个
```html
<template id="grid-template">
    <!-- 2.0下只有一个根节点-->
    <div>
        <table>
            <thead>
                <tr>
                    <th v-for="col in columns">
                        {{ col.name }}
                    </th>
                    <th>
                        删除
                    </th>
                </tr>
            </thead>
            <tbody>
                <!--
                <tr v-for="(index,entry) in dataList | filterBy searchKey">
                -->
                <tr v-for="(entry,index) in dataList">	
                    <td v-for="col in columns">
                        {{entry[col.name]}}
                    </td>
                    <td class="text-center">
                        <button class="btn-danger" @click="deleteItem(entry)">删除</button>
                    </td>
                </tr>
            </tbody>
        </table>
        <div class="container">
            <button @click="openNewItemDialog('添加新联系人')">添加联系人</button>
        </div>

        <modal-dialog :mode="mode" :title="title" :fields="columns" :item="item" v-on:create-item="createItem">
        </modal-dialog>
    </div>
</template>
```
#### 4、vue2.0组件模板必须只有一个根节点，vue1.0可以多个