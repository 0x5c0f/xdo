# 非粘贴型密码输入  
---  

`windows`下有一个叫 [`非粘贴型密码输入工具`](https://www.aliyundrive.com/s/7zvxAmNdm7L) ，非常好用，奈何`linux`下似乎没有，然后我自己写了个简单的，基本能满足自己需求。  

原理是利用`gnome`自定义快捷键加上 [`xdotool`](https://www.semicomplete.com/projects/xdotool/) 的键鼠模拟功能实现的  

## 运行环境:

- `fedora32`
- `gnome 3.36.9`

## 说明及注意事项

1. 配置名称重复视为修改键位绑定
2. 支持新增，但不支持删除，删除需在`设置`-`键盘快捷键`中手动删除按键绑定
3. 支持直接从剪切板粘贴
4. 按键初始化理论支持所有`gnome`环境
5. 输入功能理论支持所有`linux`桌面环境
6. ... 

## 获取代码

```bash
sudo dnf install xdotool jq xsel -y 

mkdir $HOME/.xdotool && cd $HOME/.xdotool

git clone https://github.com/0x5c0f/xdo.git .

chmod +x $HOME/.xdotool/xdo
```

# 配置参数说明

```bash
# 示例配置(json格式)
# 默认位置在 ${HOME}/.xdotool/config
# name: 快捷键名称(系统-键盘快捷键中展示名称)
# bindKey: 绑定到那个按键(F7、<Alt>7)
# bindScript: 执行脚本的位置,不指定默认/usr/local/bin/xdo
# text: 配置要发送的内容，一般这个是用来发送密码的 
# 所以配置这里是base64加密了的值，在脚本里面有解密 
# 若此项不配置，则代表从剪切板直接粘贴内容 
[
  {
    "name": "",
    "bindKey": "",
    "bindScript": null,
    "text": null 
  }
]

```

# 配置

```bash
# 首次使用需在调整好配置文件后初始化一下按键绑定
# 也可自己在 设置-键盘快捷键 中手动创建快捷键，指定运行脚本为当前xdo，参数为快捷键名的md5值(默认5为)
$HOME/.xdotool/xdo init     
```

`init` 后就可以愉快的使用绑定快捷键录入内容了
