# 3.0project

本项目主要是体验vue-cli3版本脚手架，以及更便捷的webpack配置，但是发现 快速原型开发 挺不错的，顺手做了两个小demo



## 快速原型开发

```
npm install -g @vue/cli-service-global

vue serve 和 vue build 命令对单个 *.vue
```


## 创建项目

```
vue create [app-name]
```




- iview-design input bug
- html转换成pdf（图片）


### html 转换 pdf 

- [ ] 直接使用 jspdf 需要
- [x] html2pdf本质是图片（success）【jspdf】
- [ ] pdf(还没试过)

> 图片需要设置宽高，不然会出现重绘问题导致部分元素渲染失败