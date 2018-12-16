<template>
  <v-container>
    <v-layout
      text-xs-center
      wrap
    >
      <p>{{year}}年、あなたが始めるテクノロジーは?</p>
    </v-layout>
    <v-layout
      text-xs-center
      wrap
    >
      <v-flex xs12 sm6>
        <v-text-field
          v-model="name"
          label="お名前" placeholder="MARY（アルファベットで入れてね！）"
          :error-messages='message'
          width="300"
          v-on:keyup="keyup"
        ></v-text-field>
      </v-flex>
      <v-btn color="info" v-on:click="exec">占う</v-btn>
    </v-layout>
    <v-layout
      text-xs-center
      wrap
    >
      <p><span v-html="result.summary"></span></p>
    </v-layout>
    <v-layout
      text-xs-center
      wrap
    >
      <v-flex xs12 sm6>
        <v-img :src='result.img' :alt='result.tech'></v-img>
      </v-flex>
    </v-layout>
    <v-layout
      text-xs-center
      wrap
    >
      <v-flex xs12 sm6>
        <p style="margin-top:1rem;">{{result.desc}}</p>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    methods: {
      exec: function () {
        const A = 65;
        var nextYear = "";
        switch (this.year)
        {
          case 2019: nextYear = "TWENTYNINETEEN"; break;
          case 2020: nextYear = "TWENTYTWENTY"; break;
          case 2021: nextYear = "TWENTYTWENTYONE"; break;
          case 2022: nextYear = "TWENTYTWENTYTWO"; break;
          case 2023: nextYear = "TWENTYTWENTYTHREE"; break;
          case 2024: nextYear = "TWENTYTWENTYFOUR"; break;
          case 2025: nextYear = "TWENTYTWENTYFIVE"; break;
          default: nextYear = ""; break;
        }
        let isValid = this.name.toUpperCase().match(/^[A-Z]+$/gi);
        if (isValid) 
        {
          // 来年と名前をシャッフルする
          var candidates = (this.name + nextYear).toUpperCase().split("");
          candidates.sort(function() {return Math.random()-.5});
          var idx = Math.floor(Math.random() * candidates.length);
          // console.log("選択された頭文字は、" + candidates[idx]);
          var innerList = this.list[candidates[idx].charCodeAt(0) - A];
          this.result = 
            innerList[Math.floor(Math.random() * innerList.length)];
          this.result.summary = 
            "来年は<span style='font-weight:bold; font-size:x-large;'>" 
            + this.result.tech + "!!</span>";
          this.message = "";
      } 
        else 
        {
          this.result = { tech : "", summary : "" };
          this.message = "アルファベットのみで入力してください";
        }
      },
      keyup: function (e) {
        const ENTER = 13;
        if (e.keyCode === ENTER) {
          this.exec();
        }
      }
    },
    data: () => ({
      name: "", 
      message: "",
      list : [
        [ 
          { tech : "Ada", img: "https://upload.wikimedia.org/wikipedia/commons/c/c0/Ada_Lovelace_Chalon_portrait.jpg", desc : "エイダは史上初のプログラマ。" }, 
          { tech : "AWS", img: "https://casa.nrao.edu/casadocs/casa-5.4.1/casa-on-amazon-web-services/aws-logo.jpg", desc : "ちゃんと課金チェックしないとあかんよ。" },
          { tech : "Azure", img: "https://stackify.com/wp-content/uploads/2017/10/microsoft-azure-managed-services-2-1-793x397.png", desc : "AWSばっかりやってないで、Azureはどうですか？" },
          { tech : "ARDUINO", img: "http://mag.switch-science.com/wp-content/uploads/2015/06/Arduino-436x291.png", desc : "Rasberry Pieから初めてもいいけど、チカチカLEDしましょう！" },
        ],
        [ 
          { tech : "Brainf*ck", img: "https://cdn.zmescience.com/wp-content/uploads/2017/01/brainfuck.png", desc : "エイプリールフールにどうぞ！" } ,
          { tech : "Bash", img: "https://cdn-ak.f.st-hatena.com/images/fotolife/c/chanmoro999/20140927/20140927195501.png", desc : "おいら、pipeが使えません。。。" } ,
        ],
        [ 
          { tech : "Chef", img: "https://www.chef.io/wp-content/uploads/2017/07/chef-software_facebook-share_min.png", desc : "レシピが全てや〜！" },
        ],
        [ 
          { tech : "Docker", img: "https://cdn-images-1.medium.com/max/1600/1*Yo7ixCaV3BGK-vrNKdPwAg.png", desc : "軽量に仮想環境を作るぞ〜！" },
        ],
        [ 
          { tech : "ExpressJS", img: "https://amandeepmittal.gallerycdn.vsassets.io/extensions/amandeepmittal/expressjs/2.0.0/1509881293872/Microsoft.VisualStudio.Services.Icons.Default", desc : "ExpressJSはおいらが初めて使いこなしたFrameworkです！" },
          { tech : "ECMAScript", img: "https://cdn-images-1.medium.com/max/2000/1*Z-9unq6Am3vekNOa5fD1xg.png", desc : "CoffeeScriptを覚えたら、すぐにEcmascriptに書き換えることになった〜（泣）" },
        ],
        [ 
          { tech : "Firebase", img: "https://cdn-images-1.medium.com/max/1600/1*lLoa30p6NYO9je-BGUsPpw.png", desc : "brabrabra..1" },
        ],
        [ 
          { tech : "Go言語", img: "https://upload.wikimedia.org/wikipedia/commons/thumb/2/23/Golang.png/1200px-Golang.png", desc : "Gopher君がかわいい。。。（受け売りです。）" },
          { tech : "Google Cloud Platform", img: "https://i0.wp.com/roguer.info/wp-content/uploads/2018/01/CloudPlatform_VerticalLockup.png?w=1267", desc : "GoでFunctionを書きますか？" },
        ],
        [ 
          { tech : "Haskell", img: "https://upload.wikimedia.org/wikipedia/commons/thumb/1/1c/Haskell-Logo.svg/1920px-Haskell-Logo.svg.png", desc : "純粋関数型言語、そろそろやらんとな〜♪" },
          { tech : "Heroku", img: "https://tech-camp.in/note/wp-content/uploads/Heroku.png", desc : "heroku push master!" },
        ],
        [ 
          { tech : "Itamae", img: "http://cdn-ak.f.st-hatena.com/images/fotolife/u/upamune/20160501/20160501233415.png", desc : "環境作成は「へいお待ち！」" },
        ],
        [ 
          { tech : "Java", img: "https://cdn-ak.f.st-hatena.com/images/fotolife/c/c-pattamada/20180406/20180406164916.jpg", desc : "おいらの人生初のプログラミング言語はJavaでした！" },
        ],
        [ 
          { tech : "Kitematic", img: "https://kitematic.com/img/feature2.e048.png", desc : "DockerをGUIで扱えるなんて便利やわ〜。" },
          { tech : "Kotlin", img: "https://cdn-ak.f.st-hatena.com/images/fotolife/s/saburesan/20160906/20160906091652.jpg", desc : "Android Studioで開発する場合はみんなKotlinですか〜？" },
        ],
        [ 
          { tech : "Laravel", img: "https://www.terakoya.work/wp-content/uploads/2018/07/laravel-feature-view.png", desc : "嗚呼、artisanコマンド、忘れたわ。" },
        ],
        [ 
          { tech : "MySQL", img: "https://cdn-images-1.medium.com/max/1600/1*DZyivhX9QpnKxovKyQjZEw.png", desc : "MariaDBっていうのもあるけどね。" },
        ],
        [ 
          { tech : "Node.js", img: "https://camo.qiitausercontent.com/482e6f91f1a4eab6203f96ac05fd5148df962ff4/68747470733a2f2f71696974612d696d6167652d73746f72652e73332e616d617a6f6e6177732e636f6d2f302f3234373633382f38613237643066302d323835382d636365612d663365302d3936356537353965393436652e706e67", desc : "個人的には大好きだわ。" },
        ],
        [ 
          { tech : "Oracle", img: "https://d2v9k5u4v94ulw.cloudfront.net/assets/images/164953/original/45817b05-4463-4787-92a9-a5ba37726afa.png?1438566421", desc : "あんまり触る機会ないなあ。。。" },
        ],
        [ 
          { tech : "Python", img: "https://s3-ap-northeast-1.amazonaws.com/samurai-blog-media/blog/wp-content/uploads/2017/08/python-640x366.jpg", desc : "Google スピーカーのRestAPIをPythonで書いてたのに、Node.jsにしてもうた。。。" },
          { tech : "Postgresql", img: "https://cdn-ak.f.st-hatena.com/images/fotolife/h/hirooooo-lab/20160627/20160627121830.jpg", desc : "Postgresqlはずっと使ってます！" },
          { tech : "PHP", img: "https://hrf-tricks.com/wp-content/uploads/2018/07/php-1024x538.png", desc : "PHPerにまだなれない。。。" },
          { tech : "Processing", img: "https://cdn-images-1.medium.com/max/1600/1*lLoa30p6NYO9je-BGUsPpw.png", desc : "brabrabra..1" },
          { tech : "Perl", img: "https://rr.img.naver.jp/mig?src=https%3A%2F%2Frahman371.files.wordpress.com%2F2014%2F09%2Fperl.gif&twidth=1200&theight=1200&qlt=80&res_format=jpg&op=r", desc : "ラクダ〜ラクダ〜ラクダ〜♪" },
        ],
        [ 
          { tech : "(Q_Q)<なんや？", img: "https://news.mynavi.jp/article/20180321-604140/images/001.jpg", desc : "思い浮かばれへん。。。" },
        ],
        [ 
          { tech : "Rasberry Pi", img: "https://images.techhive.com/images/article/2017/01/intro-100703562-large.3x2.jpg", desc : "話題のLoTやろ！" },
          { tech : "R", img: "https://exploratory.io/note/kanaugust/25-R-4689376389099355/viz_images/thumbnail.png", desc : "君の統計解析元年や！" },
        ],
        [ 
          { tech : "Sketch", img: "https://cdn-images-1.medium.com/max/2000/1*8LZO5BfDELOfsK0NarlIuA@2x.png", desc : "Figma派もいるけど、おいらはSketch派！" },
          { tech : "Scratch", img: "https://it-agency.in/wp-content/uploads/2018/02/DTCakT5WsAEApJT.jpg", desc : "童心に戻って！" },
          { tech : "Swift", img: "https://cdn-ak.f.st-hatena.com/images/fotolife/g/gaku2n/20180527/20180527225858.png", desc : "iOSアプリ、みんな作れるか。" },
        ],
        [ 
          { tech : "TypeScript", img: "https://www.gaprot.jp/wp-content/uploads/2017/05/typescript-logo.png", desc : "JavaScriptで静的型付けできるわ〜♪" },
        ],
        [ 
          { tech : "Unity", img: "https://assets.media-platform.com/gizmodo/dist/images/2016/08/20160824nuni-w1280.jpg", desc : "C#でゲームを作るぞ〜♪" },
        ],
        [ 
          { tech : "Vue", img: "https://jp.vuejs.org/images/logo.png", desc : "このアプリもVueでできていますよ！" },
        ],
        [ 
          { tech : "Windows", img: "http://tanweb.net/wordpress/wp-content/uploads/2018/01/ec-windows10.png", desc : "Macbookばかり触ってないで、Windowsもわりと使いやすい！" },
          { tech : "Wine", img: "https://static.makeuseof.com/wp-content/uploads/2015/12/linux-wine-670x335.jpg", desc : "LinuxでWindowsアプリ動かさないですかー？" },
        ],
        [ 
          { tech : "Xamarin", img: "https://cdn-images-1.medium.com/max/1600/1*lLoa30p6NYO9je-BGUsPpw.png", desc : "クロスプラットフォームアプリをC#でゴリゴリ〜♪" },
        ],
        [ 
          { tech : "Yarn", img: "https://cdn-images-1.medium.com/max/1600/1*m6zlwvyKm9BPeFQCKvGQEQ.png", desc : "npmから卒業？" },
        ],
        [ 
          { tech : "zsh", img: "https://camo.qiitausercontent.com/41bf7d491783c21b77e9d4e0189917622967e346/68747470733a2f2f71696974612d696d6167652d73746f72652e73332e616d617a6f6e6177732e636f6d2f302f3134323831302f62303536343561642d386165612d346134312d396166372d3839396664303564623864612e706e67", desc : "もう浮かばん。。。" },
        ],
      ],
      result : { tech : "", summary : "" }
    }),
    props: ['year']
  }
</script>
<style>
</style>
