rename-js
=========

rename files/directories in the command line, use the javascript RegExp rules to rename files.  
在命令行批量重命名文件、目录，使用 javascript 的正则来匹配和替换文件名


example:
---------
directory public has some files: 

1. index.js 
2. index.css 
3. index.html

, and i want to rename all files with `index` prefix to another name,
then:

```javascript
node rename.js 'index\.(\w+)$' 'anotherName.$1'
```

the real script is:

```javascript
var newName = originName.replace(new RegExp('index\.(\w+)$'), 'anotherName.$1')
```

then got:

1. anotherName.js
2. anotherName.css
3. anotherName.html
