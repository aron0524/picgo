# Typora破解教程（2023版）

## 1. 需要`python`环境，没有的话自行安装一下

## 2. 克隆脚本文件

```javascript
git clone https://github.com/Mas0nShi/typoraCracker.git
```

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202301171459494.png)

安装依赖:

```javascript
pip install -r requirements.txt
```

复制

## 3. 找到Typora安装目录下的`resources`目录下的`app.asar`文件

默认应该是在 `C:\Program Files\Typora\resources\app.asar`

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202301171500930.png)

Typora2022破解教程

## 4. 执行解包命名：

Windows下如果路径是有空格的，需要用`""`包起来，如果提示权限问题，用管理员身份运行命令行，建议后续都用管理员身份执行。

```javascript
python typora.py "C:\Program Files\Typora\resources\app.asar" workstation\outfile\
```

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202301171500191.jpeg)

## 5. 使用脚本文件夹`example\path\License.js`替换掉`workstation\outfile\dec_app\License.js`文件

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202301171501657.png)

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202301171501885.png)

## 6. 打包`app.asar`文件

```javascript
python typora.py -u workstation\outfile\dec_app workstation\outappasar
```



我直接执行会报错:

```javascript
PS C:\Code\mine\typoraCracker> python typora.py -u workstation/outfile/dec_app workstation/outappasar
2021-12-03 15:25:59.623 | ERROR | __main__:packWenc:103 - plz input Directory for app.asar
Traceback (most recent call last):
  File "C:\Code\mine\typoraCracker\typora.py", line 151, in <module>
 main()
  File "C:\Code\mine\typoraCracker\typora.py", line 146, in main
 args.mode(args.asarPath, args.dirPath, args.format)
  File "C:\Code\mine\typoraCracker\typora.py", line 104, in packWenc
 raise NotADirectoryError
NotADirectoryError
```



手动在脚本路径下创`workstation/outappasar`文件夹就行了:

```javascript
mkdir workstation/outappasar
python typora.py -u workstation\outfile\dec_app workstation\outappasar
```



## 7. 将打包回来的`app.asar`文件重新丢到`Typora`的`resources`目录下

## 8. 授权码生成

需要安装`nodejs`环境，如果没有安装请自行安装。

```javascript
验证node安装:
node -v
```

```javascript
node example/keygen.js
```

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202301171502472.png)

## 9. 激活

授权码输入生成的码，邮箱输入`crack@example.com`，完事。