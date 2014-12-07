rename-js
=========

rename files/directories in the command line, use the javascript RegExp rules to rename files.  
在命令行批量重命名文件、目录，使用 javascript 的正则来匹配和替换文件名


Install:
----------
```shell
$ npm install rename-js -g
```

Usage:
---------
directory `public` has some files: 

1. index.js 
2. index.css 
3. index.html

, and i want to rename all files with `index` prefix to another name,
then:

```shell
$ cd /path/to/public
$ rename 'index\.(\w+)$' 'anotherName.$1'
```

the real script is:

```javascript
var newName = originName.replace(new RegExp('index\.(\w+)$'), 'anotherName.$1')
```

then got:

1. anotherName.js
2. anotherName.css
3. anotherName.html


Advanced Usage
----------------
directory `public` has some files: 

1. 4.jpg
2. 10.jpg
3. 99.jpg
4. folder/45.jpg

, and i want to rename all files to three-digits name, like `099.jpg`,
then write a script named `processor.js`:

processor.js
```javascript
function pad(num, len, _char){
	if(len <= num.length) return num
	return (new Array((len - num.length) + 1)).join(_char) + num
}
// type: 'file'|'directory'|'blockDevice'|'symbolicLink'|'characterDevice'|'FIFO'|'socket'
// see `https://github.com/coolaj86/node-walk` for more info.
module.exports = function(filename, type){
    // if(type == 'file') xxx
    // filename: folder/45.jpg
    var m = filename.match(/^(folder\/)?(\d+)(\.jpg)$/)
    if(m){
        return (m[1] || '') + pad(m[2], 3, '0') + m[3]
    }
    // return the same string or undefined will not rename the file
    return filename
}
```
then run commands:

```shell
$ cd /path/to/public
$ rename -f ./processor
```
last got:

1. 004.jpg
2. 010.jpg
3. 099.jpg
4. folder/045.jpg