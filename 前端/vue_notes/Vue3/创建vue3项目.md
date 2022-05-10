## 使用vue-cli创建

```javascript
// 命令行中查看脚手架版本是否支持vue3，确保@vue/cli版本在4.5.0以上
vue -V

// 若版本太低，执行命令，默认安装最新版本（覆盖安装）
npm install -g @vue/cli

// 创建（与vue2版本一致）
vue create vue_test
```



## 使用vite创建

- 什么是vite？——新一代前端构建工具。
- 优势如下：
  - 开发环境中，无需打包操作，可快速的冷启动。
  - 轻量快速的热重载（HMR）。
  - 真正的按需编译，不再等待整个应用编译完成。
- 传统构建与vite构建对比图
                   <img src="F:\study_notes\前端\vue_notes\Vue3\创建vue3项目、.assets\image-20220509224438294.png" alt="image-20220509224438294" style="zoom:80%;" />

<img src="F:\study_notes\前端\vue_notes\Vue3\创建vue3项目、.assets\image-20220509224457211.png" alt="image-20220509224457211" style="zoom:80%;" />

```javascript
// 创建工程
npm init vite-app <project-name>
// 官网目前更新的命令：npm create vite@latest，上面
// 进入工程目录
cd <project-name>
// 安装依赖
npm install
// 运行
npm run dev
```

