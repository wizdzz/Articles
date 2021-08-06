lldb 命令

Windows lldb 下载：
https://github.com/vadimcn/llvm/releases/download/r313613/LLVM-6.0.0-r313613-win32.exe

## 启动 server（Android studio 调试过 so 之后会在 /data/data/app 目录中生成 server，似乎 /data/local/tmp 目录下也会生成）:
```
adb shell su
/data/local/tmp/lldb-server platform --server --listen "*:1234" &
/data/local/lldb-server platform --server --listen "*:1234"
```

## 端口转发：
```
adb forward tcp:1234 tcp:1234
```

## 选择 platform, 连接 server:
```
platform select remote-android
platform connect ://:1234
```

## Attach 进程（首次附加可能会卡顿很久，因为复制 so 到本地或者传文件）：
```
attach 1111
```

## 查找关键字相关的命令/设置：
```
apropos xxx  // apropos Architecture  查找指令架构相关的命令/设置
```

## 断点列表：
```
br l
```

## 地址断点 (thumb 指令时目标地址需要加一)：
```
br s -a 0x4153a3c9                                      //breakpoint set -address
```

## 方法名断点：
```
br s -F time  // 完整名
br s -n time  // 函数名，对于被名称粉碎的方法很方便
```

## 给断点添加命令：
```
br com add 1                                           //command add
```

## 条件断点（很卡，不好使）:
```
br s -a 0x4153a3c9 -c '(int)strcmp($r1,"getPayload") == 0'          //--condition
```

## 内存断点(即使相同硬件，有些内核版本可能导致断点无效)：
```
wa s e -s 1 -- 0x752D0004     // 在0x752D0004 地址设置监视长度为 1 的内存断点，写
wa s e -w r -s 1 -- 0x76FE8040  // 读断点
wa s e -w read_write -s 1 -- 0x7754c23d  // 读写断点
```

## 寄存器：
```
re[gister] r[ead] r0 r1 
re r -a[ll]
```

## 查看内存：
```
x 0x75cc6a68 -c256 
x -s4 -fx -c4 0xbffff3c0                                    //--size 4 --format x --count 4
x 0x7d242700 -fs --force --size 2600
```

## 写内存：
```
memory write 0x757df678 0xde 0x3a 0x30 f7 9c 18 0b f3
```

## 显示汇编代码：
```
di -s 0x759651f2
di -s 0x759651f2 -A thumb 强制以 thumb 指令集反汇编
```

## 单步：
```
si, ni, s, n  (实际上真正有效的 step-over 指令为 step -a True)
```

## 执行到返回：
```
finish
```

## 模块列表：
```
image list
```

## 跳过 8 字节：
```
register write pc `$pc+8`  (注意 ` 不是 ‘)
```

## 强制中断：
```
process interrupt
```

## 查看地址信息 (相对模块的偏移)：
```
i[mage] loo[kup] --address 0x6be4d288
```

## 读取内存到文件：
```
me read --force -b -o D:\tmp\stv_live_debug\ijkdump.so 0x802f4000 0x802f4000+0x7abf74
me read --force -b -o D:\tmp\stv_live_debug\ytv_sm_enc_dump.so -b $r1 $r1+$r2
```

## 添加 .lldbinit 文件：
在 C:\Users\Administrator 目录新建 .lldbinit 文件，里面加上要导入的脚本

## .lldbinit
```
# 文件在 xxx/user/Administrator/ 目录

script import os, sys
command script import "D:\Program files (x86)\LLVM\lldb_script\dis_capstone.py"
```

## 读取保存的断点文件
```
breakpoint read -f F:\aa\xx\yy.txt  // 注意不能像其他命令一样省略单词
```

## 在 dlsym 下断
```
br s -F __dl_dlsym
```

