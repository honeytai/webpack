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
