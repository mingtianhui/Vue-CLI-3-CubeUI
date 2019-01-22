vue-cli3项目安装指导：
1、初始项目

2、安装依赖
根目录下：cnpm install
npm i axios -S
npm i vuex -S
npm i webpack-spritesmith -S    // 雪碧图自动生成
main.js中使用use

3、修改配置
（1）按需引用：可在main.js中按需引用cube组件

4、雪碧图生成配置
vue.config.js中
+ const SpritesmithPlugin = require('webpack-spritesmith');
添加+
const templateFunction = function (data) {
    const shared = `.sprite { background: url(I) no-repeat; background-size: ${data.spritesheet.width}px ${data.spritesheet.height}px;}`
        .replace('I', "../../" + data.spritesheet.image);
    const perSprite = data.sprites.map(function (sprite) {
        return '.icon-N { width: Wpx; height: Hpx; background-position: Xpx Ypx; }'
            .replace('N', sprite.name)
            .replace('W', sprite.width + 6)
            .replace('H', sprite.height + 6)
            .replace('X', sprite.offset_x + 3)
            .replace('Y', sprite.offset_y + 3);
    }).join('\n');
    return shared + '\n' + perSprite;
};
 configureWebpack: {
         plugins: [
             new SpriteSmithPlugin({
                 src: {
                     cwd: path.resolve(__dirname, './src/assets/images/sprite_icons/'),
                     glob: '*.png'
                 },
                 target: {
                     image: path.resolve(__dirname, './src/assets/images/css_sprites.png'),
                     css: [
                         [path.resolve(__dirname, './src/stylus/base/sprites.css'), {
                             format: 'function_based_template'
                         }]
                     ]
                 },
                 apiOptions: {
                     cssImageRef: 'assets/images/css_sprites.png'
                 },
                 customTemplates: {
                     'function_based_template': templateFunction
                 },
                 spritesmithOptions: {
                     algorithm: 'binary-tree',
                     padding: 20
                 }
             })
         ]
     }
5、px单位自动转为rem
卸载默认的postcss-px2rem，改用postcss-pxtorem（拥有更多的配置参数）
.postcssrc.js中修改为：
-> "postcss-pxtorem": {
      rootValue: 75,
      unitPrecision: 5,   // 精度，小数点后5位
      propWhiteList: ['*'],   // 白名单，全部
      selectorBlackList: [/^.cube-/,/^.wheel-/,/^.px-/], // 黑名单
      replace: true,
      mediaQuery: false,
      minPixelValue: 2    // 最小转化值，1px则不转换
    }

