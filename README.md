# webpack
knowledge of how to use webpack
1 不使用webpack.config.js的时候
require('./file-name/...js');
require('./file-name/style-loader!css-loader!...css');
注意：从后往前面编译，css-loader是先解析成webpack可以理解的css样式，style-loader是转成浏览器显示的css样式
webpack --config --progress --color --display-module --display-reasons 
webpack --module-bind 'css=style-loader!css-loader' ____________CLI方法
也可以在json文件中改变：
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "webpack": "webpack --config --progress --color --display-module --display-reasons"
  }
 然后执行 npm run webpack就可以了
 hash chunkhash的区别：
 hash是在每次打包过程改变，同义词
 

2 使用webpack.config.js
插件：
html-webpack-plugin:
参数：title filename template minify inject(false: 取消默认插入 head)
属性：files 包括：publicPath chunks(entry) js css manifest
     options 常用 minify(removeComment删除注释)
chunks:[] excludeChunks:[] 
初始化脚本直接写入到页面中的方法：
compilation.assets[].source();
如果有publicPath的时候： htmlWebpackPlugin.files.chunks.main.entry.substring(htmlWebpackPlugin.files.publicPath.length)

loader:传参数可以使用？
1.  babel-loader babel-core babel-preset-env(在json文件中“babel”: {"presets": ["env"]})
module: {
rules: [
{
test://,
loader:
exclude: path.resolve(__dirname,''),
include:

}
]
}
2. css-loader style-loader
3. postcss-loader 包括 autoprefixer
autoprefixer的配置：新建一个文件
module.exports = {
  plugins: {
  	'autoprefixer': {browsers: ['last 5 versions']}
  }
}
loader: 'style-loader!css-loader?importLoaders=1!postcss-loader' 如果有@import的时候，可以传入参数指定import的数量
注意：postcss-loader 放置在css-loader 和 less-loader之间
如果css中@import需要传入参数 但是less中@import的时候不需要 同理sass

处理模板文件
html-loader:
ejs-loader: 模板引擎 
jsx已经集成到了buble中 

处理图片 file-loader
1. css中添加了一个图片 直接指定loader即可
2. 根目录的index.html中有一个图片标签 直接loader 
以上两种不论是绝对还是相对路径，都会被loader最后替换成为绝对路径
3. 模板引擎中的图片相对路径不会被替换，最好使用绝对地址。否则 src="${require('../../assets/bg.png')}"
改变图片放置的地址

base64编码
url-loader 当文件或图片大于一定限制，就会转化为base64编码
Base64是一种用64个字符来表示任意二进制数据的方法。
用记事本打开exe、jpg、pdf这些文件时，我们都会看到一大堆乱码，因为二进制文件包含很多无法显示和打印的字符，所以，如果要让记事本这样的文本处理软件能处理二进制数据，就需要一个二进制到字符串的转换方法。Base64是一种最常见的二进制编码方法。
Base64的原理很简单，首先，准备一个包含64个字符的数组：
['A', 'B', 'C', ... 'a', 'b', 'c', ... '0', '1', ... '+', '/']
然后，对二进制数据进行处理，每3个字节一组，一共是3x8=24bit，划为4组，每组正好6个bit：
这样我们得到4个数字作为索引，然后查表，获得相应的4个字符，就是编码后的字符串。
所以，Base64编码会把3字节的二进制数据编码为4字节的文本数据，长度增加33%，好处是编码后的文本数据可以在邮件正文、网页等直接显示。
Base64是一种任意二进制到文本字符串的编码方法，常用于在URL、Cookie、网页中传输少量二进制数据。
