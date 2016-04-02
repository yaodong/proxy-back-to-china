# 身在曹营心在汉的小米盒子

这里是我在海外使用的代理设置。

这个方案中，我将小米盒子的所有流量都转发到本地的 Squid。然后按照规则对流量做分流：

- 图片、音频和视频文件，都直接设置其直接访问。
- 而其他流量根据具体情况转发到大陆的 Squid 上。

这样的设置，在大陆内的 Squid Server 的要求很低。使用一台配置最低带宽的最低配的 VPS 就可以支持小米盒子流畅观看大陆的节目。极大节省了成本。
当然，你也可以只是用大陆内的 Squid 来达到目的，但是这样对这台 Squid Server 的要求会稍高，相应地，成本也会增加。

## 如何使用

1. 准备两台 Linux 服务器，一台在大陆以外，一台在大陆内。
2. 在两个 Linux 上都安装 Squid。（以下称海外的 Squid 为 Squid-Oversea，大陆内的 Squid 为 Squid-CN ）
3. 使用 `squid-cn` 和  `squid-oversea` 内的配置文件，分别配置两个 Squid。
  3.1 使用前需要修改两个 `squid.conf` 里面的 `YOUR_PROXY_IP` 还有 `YOUR_PROXY_PORT`。修改为 Squid-CN 的 IP 地址和 Squid 实例的端口。
4. 将小米盒子的流量都重定向到海外的 Squid.

## 我的部署

- Squid-CN Server 使用的是 QingCloud VPS (Debian)。
- Squid-Oversea Server 使用的是位于海外的一个 Raspberry Pi (Raspbain)。
- 重定向网络流量使用的是 RouterOS (v6.32.3) 的内置功能。
