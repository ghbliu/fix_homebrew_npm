# fix_homebrew_npm

解决npm在MAC系统上通过brew install node方式安装完成后报错的问题
brew install node 后
node -v 正常
npm -v 

出现类似下面的错误：
module.js:211
    throw err;
    ^
Error: Cannot find module 'npmlog'
at Function.Module._resolveFilename (module.js:337:15)

此时，应该用下面方法解决问题：

强制删除node_modules
rm -rf /usr/local/lib/node_modules
卸载原node
brew uninstall node
安装node但不安装npm包
brew install node --without-npm
直接手动安装npm
echo prefix=~/.npm-packages >> ~/.npmrc
curl -L https://www.npmjs.com/install.sh | sudo sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  6263  100  6263    0     0   3138      0  0:00:01  0:00:01 --:--:--  3137Password:

tar=/usr/bin/tar
version:
bsdtar 2.8.3 - libarchive 2.8.3
install npm@latest
fetching: http://registry.npmjs.org/npm/-/npm-3.8.7.tgz
/Users/xxx/.npm-packages/bin/npm -> /Users/xxx/.npm-packages/lib/node_modules/npm/bin/npm-cli.js
/Users/xxx/.npm-packages/lib

此时node已经安装好了，没有问题，可以通过node -v查看。
但npm -v可能还是不工作，没关系
我们需要把 ~/.npm-packages/bin 加入 PATH 这样npm就变成全局变量。
sudo nano ~/.profile
添加
export PATH="$HOME/.npm-packages/bin:$PATH"
继续
sudo ln -s ~/.npm-packages/bin/npm /usr/local/bin/npm
这样npm 就可以运行了。

