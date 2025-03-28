# 在CloudCone VPS的CentOS 6.x系统上安装Google BBR加速教程

## 为什么需要手动安装BBR？

CloudCone VPS的CentOS 7系统模板默认已集成BBR加速功能，但CentOS 6.x系统却需要手动安装。这是由于系统底层配置差异导致的特殊需求。本文将详细介绍在CentOS 6.x环境下完美部署Google BBR加速的完整流程。

👉 [【点击查看】2025年最新CloudCone优惠码及特价云服务器方案汇总](https://bit.ly/Cloudcone)

## 详细安装步骤

### 第一步：修正系统配置
执行以下命令修复内核模块加载问题：
bash
sed -i "s/blk_init_queue/blk_cleanup_queue/g" /usr/share/dracut/modules.d/90kernel-modules/installkernel

### 第二步：更新安全组件
安装必要的安全更新并导入ELRepo密钥：
bash
yum -y update nss
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org

### 第三步：执行BBR安装脚本
运行自动化安装脚本（注意：执行后5秒内需按Enter键确认）：
bash
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh

**重要提示**：脚本执行完成后会出现重启提示，输入`y`确认重启使配置生效。

## 验证安装结果

### 检查BBR状态
使用以下命令验证BBR是否激活成功：
bash
sysctl net.ipv4.tcp_available_congestion_control

### 预期输出
成功安装后会显示包含`bbr`字段的返回信息：

net.ipv4.tcp_available_congestion_control = reno cubic bbr

### 故障处理
若未检测到BBR模块，建议通过CloudCone控制面板重装系统后重新按照本教程操作。

## 性能优化建议
BBR加速可显著提升网络传输效率，特别适合部署在CloudCone等国际VPS上使用。建议定期检查内核更新以获得最佳性能表现。