### 安装插件  path autocomplete

#### 然后在setting.json中添加如下配置

> 如遇到@路径时没有自动提示，可查看setting.json文件中该代码是否没有高亮，如果没有高亮，插件卸载重装即可

```javascript
//导入文件时是否携带文件的扩展名
"path-autocomplete.extensionOnImport": true,
//配置@的路径提示
"path-autocomplete.pathMappings": {
 "@": "${folder}/src"
},
```

