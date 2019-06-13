# Paul Theme Typecho Introduction

Design Prototype: <https://paul.ren>

<a href="../master/README-CN.md">Chinese Document</a>

More Star, More Demands, More Upgrade.

## Preview

![image](https://user-images.githubusercontent.com/41265413/59440844-2ca08a00-8e2a-11e9-95bf-3acc5a2acc6d.png)

![image](https://user-images.githubusercontent.com/41265413/59444149-e9e1b080-8e2f-11e9-94b8-2e45c59fcf8b.png)

![image](https://user-images.githubusercontent.com/41265413/59440870-39bd7900-8e2a-11e9-879b-04e7a792235c.png)

![image](https://user-images.githubusercontent.com/41265413/59440890-40e48700-8e2a-11e9-8b71-3d1b4c5479b9.png)

![image](https://user-images.githubusercontent.com/41265413/59440935-55288400-8e2a-11e9-8dc2-84a42e61343a.png)

![image](https://user-images.githubusercontent.com/41265413/59440958-5eb1ec00-8e2a-11e9-8176-42e60bff4164.png)

![image](https://user-images.githubusercontent.com/41265413/59441089-99b41f80-8e2a-11e9-9a97-bd0c19946756.png)

![image](https://user-images.githubusercontent.com/41265413/59441120-a9cbff00-8e2a-11e9-87ef-241ff0edccdc.png)

You can also go to this url <https://paul.ren>, called Paul's Home ,to visit its prototype.

## information

See [Pual Typecho主题发布](https://shizuri.net/archives/131/).

## Feature

- [x] Write diary
- [x] Exhibit says
- [x] Nice home index page
- [x] Awesome article page
- [x] Beautiful Works page
- [x] Commit
- [x] Like, Views, Word Count (need VOID_Plugin)
- [x] Player
- [x] Others

## Before Start

This is a theme for Typecho, which suit to write diary and display your home page.

This theme stems from <https://paul.ren>, this is not perfect now, probably had more bugs. Cause of them, on the one hand, because of the Typecho's limit.On the other hand, time is in a hurry. 

## Quickly Start

Clone this repo, and go to dashboard -- theme -- Paul, enable it. In the this theme's setting, you should fill out form.

## Index Page

On the index page, you will see four of nav button on the top of the window, Index, about, donate and dream. It will display according to your create the necessary pages. It will display `index` button , if your don't do anything, it is default. So you should do like following.

about page: you should create independent page, select the `首页模板` template, and you can write any content you like.

dream page: you should create independent page, select the `首页模板` template, and you can write any content you like.

donate page: you should create independent page, select the `首页模板` template, and you can write any content you like.

index page had four columns, personal information, recent articles, recent diaries, projects.

personal information should fill out form in the theme setting or Typecho setting.

recent blog articles parse according to RSS url which you fill out.

recent diaries will exhibit four items, every items output about 50 words.

works according to if it is exists, and display them.

## Diary Page

diary page is the most important page in this theme. It is the core. So you must be create it necessary and correctly.

diary page: you should create independent page, select the `日记页面` template, and you can write any content you like, because it will ingore you content which you worte. How many diary will display according to your setting in the theme config. But, because of the limit of the typecho, other articles also can access by enter the permanent link.

## Other Page [Option]

works page: you should create independent page, select the `作品页面` template, and the content format should write like following.

```json5
[{
"name": "project one",  // name
"img": "",       // img url, if none, will display default img
"url": "https://i.shizuri.net/" // Url
},
{"name": "project two",
"img": "",
"url": "https://i.yiny.me/"
}]
```

says page: you should create independent page, select the `语录页面` template, and the content format should write like following. (says body --- say's avatar, every says should have a blank line)

```
可能，是命运的安排，让我们自愿走上了这条艰难的道路，然后，在这条布满荆棘的曲折小路上慢慢去寻找人生的乐趣。然而，此时，我才发现，真正美妙而有意义的人生，大概就从我坚定不移地追求自己梦想的时候，才正式开始。———— 《愿你历经千帆，归来仍是少年》

生命的本质是苦难的。我不追求天赐荣华富贵，那会让我诚惶诚恐，消受不起，只是觉得，每天睁开眼睛发现自己还活着，没有缺胳膊少腿，还可以通过自己的努力和命运的黑色幽默较量搏斗，还可以勇敢的有尊严地与困难较量，这种感觉很踏实。———— 《愿你历经千帆，归来仍是少年》
```

project information page: you can create a independent page which used `作品介绍页` template, this template will render page like <https://paul.ren/project/style>. And the format also used JSON.

```json5
{
"info": "示例介绍", // information
"project_img": "", // project image, if none, will used default image.
"url": "https://works.paugram.com/style", // url
"doc_url": "", // document url, if none, will not display it.
"imgs": ["https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=3344978418,213176529&fm=27&gp=0.jpg","https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3689685426,1442582010&fm=27&gp=0.jpg"],  // images
"body": "<p>Kico Style 是一个简洁的前端样式框架，只提供页面布局等基础功能。代码轻量、不冗余，适合前端初学者和探索者。</p>" // content body.
}
```

To turn other music in the bottom of the player, you need open the file named `paul.js` in `src` directory. Find follow this.

```js
var paul_music = new function () {
    var that = this;
    this.list = ["520570570", "541432715"];  // replace your music id, the source of music id come from Netease Music
    this.action = {};
    var status = {playing: 0, lyric: [], lyric_index: 0};
    this.setList = function () {
        var newList = [];
        ks("[data-sid]").each(function (item, key) {
            newList.push(item.dataset["sid"]);
            item.onclick = function (t) {
                if (that.list !== newList) that.list = newList;
                document.body.classList.add("has-player");
                status.playing = key;
                that.play();
            }
        });
    };
}
```

To like one article, you should use VOID_Plugin, because this demand based on VOID_Plugin, you should move the `VOID` directory to the `../plugins/`, and go to dashboard to enable it. '

Enjoy.

## Copyright & Open Source

Belong to @Dreamer-Paul & @Innei. MIT Licence.

## Used Open Source

- fontawesome 4
- Kico Style
- Kico Player
- VOID_Plugin

## Thanks

- [@Dreamer-Paul](https://github.com/Dreamer-Paul)
- [@moesoha](https://github.com/moesoha)