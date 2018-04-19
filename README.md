# webpack
knowledge of how to use webpack
1 不使用webpack.config.js的时候
require('./file-name/...js');
require('./file-name/style-loader!css-loader!...css');
注意：从后往前面编译，css-loader是先解析成webpack可以理解的css样式，style-loader是转成浏览器显示的css样式
webpack --config --progress --color --display-module --display-reasons 
webpack --module-bind 'css=style-loader!css-loader'
也可以在json文件中改变：
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "webpack": "webpack --config --progress --color --display-module --display-reasons"
  }
 然后执行 npm run webpack就可以了
 hash chunkhash的区别：
 hash是在每次打包过程改变，同义词
 

2 使用webpack.config.js
