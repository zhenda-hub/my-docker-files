# windows WSL2

## 配置WSL防止内存过大

### WSL2 配置的官方文档
<https://learn.microsoft.com/en-us/windows/wsl/wsl-config#configure-global-options-with-wslconfig>

1. 创建 C:\Users\username\.wslconfig
2. 写入以下内容

    ```
    [wsl2]
    # 配置 WSL 的核心数
    # processors=2
    # 配置 WSL 的内存最大值
    memory=8GB
    # 配置交换内存大小，默认是电脑内存的 1/4
    #swap=8GB
    # 关闭默认连接以将 WSL 2 本地主机绑定到 Windows 本地主机
    #localhostForwarding=true
    # 设置临时文件位置，默认 %USERPROFILE%\\AppData\\Local\\Temp\\swap.vhdx
    # swapfile=D:\\\\temp\\\\wsl-swap.vhdx
    ```

## 设置daemon.json

~/.docker/daemon.json
