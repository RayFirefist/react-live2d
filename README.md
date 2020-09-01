<h1 align="center">react-live2d</h1>

![npm](https://img.shields.io/npm/dt/react-live2d)
![NPM](https://img.shields.io/npm/l/react-live2d)
![npm](https://img.shields.io/npm/v/react-live2d)


[示例地址](http://test2.supmiao.com)

![示例图片](img/example.png)

示例服务器配置较差，网站首次打开，看板娘需要加载较大的皮肤纹理高清图，请耐心等候


## 目录说明

```
·
├─ Core                         # Cubism Core 核心库

└─ Samples                      

   └─ TypeScript

      └─ Demo                   # 项目目录

         └─ Resources           # live2D的模型及动作导出的文件

         └─ Framework           # 包含渲染和动画功能等的源代码

         └─ src                 # 核心代码
```

## 🖥 Environment Support
|  | Windows | macOS | Linux | Android | iOS |
| ----- | :-----: | :-----: | :-----: | :-----: | :-----: |
| Google Chrome | ✔ | ✔ | ✔ | ✔ | ✔ |
| Firefox | ✔ | ✔ | ✔ | ✔ | ✔ |
| Safari | - | ✔ | - | - | ✔ |
| Microsoft Edge | ✔ | ✔ | - | ✔ | ✔ |
| Internet Explorer 11 | ✔ | - | - | - | - |

## 📦 Install

```bash
npm install react-live2d
```


## 🔨 Usage for SPA
#####  如：create-react-app


基础包直接使用script引入，在你个人的react项目的->public->index.html先插入，Core里可获得该min.js
```
<script src = "http://publicjs.supmiao.com/live2dcubismcore.min.js"></script>
```

```jsx
import ReactLive2d from 'react-live2d';

const App = () => (
  <>
    <ReactLive2d
        width={300}
        height={500}
    />
  </>
);
```

比如你想要给页面加入模型Hiyori，那就在你的react项目中的public目录下，将Hiyori放入Resources资源文件夹,如

```
·
└─ public                     

   └─ Resources

       └─ Hiyori
```


## 🔨 Usage for SSR
#####  如：create-next-app

项目根目录创建components文件夹，并在其中创建Header.js
```jsx
import React from 'react'
import Head from 'next/head'

const Header = () => (
  <div className="header">
    <Head>
    <title></title>
    <meta name="viewport" content="initial-scale=1.0, width=device-width" />
    <script>
        {
        `             
    with(document)0[(getElementsByTagName('head')[0]||body).appendChild(createElement('script')).src='http://publicjs.supmiao.com/live2dcubismcore.min.js'];
    `
        }
    
    </script>
    </Head>
 </div>
)

export default Header
```

```jsx
import dynamic from 'next/dynamic'


const DynamicComponentWithNoSSR = dynamic(import('../components/Header'), {
  ssr: false
})

const ReactLive2d = dynamic(import('react-live2d'), {
  ssr: false
})

export default function Home() (
  <>
    <DynamicComponentWithNoSSR></DynamicComponentWithNoSSR>
    <ReactLive2d
      width = { 300}
      height = { 500}
      bottom = { '10px'}
      right = { '10px'}
      ModelList = { ['Haru']}
      TouchBody = { ['啊啊啊啊啊你要干嘛', '哼', '坏人']}
      PathFull='http://publicjs.supmiao.com/Resources/'
    />
  </>
);
```

SSR使用看板娘需要允许跨域的资源域名，nginx参考配置如下：
```
server {　　 
    ....
    add_header Access-Control-Allow-Origin *;
    add_header Access-Control-Allow-Methods 'GET,POST';
    add_header Access-Control-Allow-Headers 'DNT,X-Mx-ReqToken,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Authorization';  
}
```

## 🌍 More Model
最新的SDK是支持moc3格式的模型，并且官方以后保证了新版本也向前兼容（除了2以前的）。
所以使用的大大们记得使用时去寻找moc3模型^ ^
如何辨别是moc3格式模型：
![示例图片](img/model.png)


更多模型，请动手在github搜索'live2d 模型'即可，模型大多有版权，请慎勿用于商业~

api 文档 （待完善，如有需要功能欢迎提[issue](https://github.com/chendishen/Live2DBase/issues)）

| 成员 | 说明 | 类型 | 默认值 |
| :-----: | ----- | ----- | ----- |
| width | 盒子宽度 | Number | 300 |
| height | 盒子高度 | Number | 500 |
| top | position：relative的top值 | String | '' |
| right | position：relative的right值 | String | '0' |
| bottom | position：relative的bottom值 | String | '0' |
| left | position：relative的left值 | String | '' |
| ModelList | 模型列表，暂时只展示数组的第一个模型 | Array<String> | ['Hiyori'] |
| TouchBody | 点击身体时聊天框随机出现数组的值 | Array<String> | ['啊呀，你的手在摸哪里嘛~','哼，坏人'] |
| TouchHead | 点击头部时聊天框随机出现数组的值,该值当模型未存入头部事件时无效 | Array<String> | ['讨厌,不要掐人家的脸嘛~','希望明天也能感受到你的触摸呢'] |
| color | 聊天框背景颜色 | String | '#C8E6FE' |
| PathFull | 当SSR框架时，必须传入此参数，用以额外指定绝对路径资源域名地址 | String | '' |


