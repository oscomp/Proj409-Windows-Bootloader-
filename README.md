### 项目名称
Windows环境下Bootloader链式加载的实现

### 项目描述
高校计算机机房通常需承担多门课程的教学任务，因此往往需要配置多种操作系统环境以满足不同教学需求。为了确保系统的稳定性和可用性，操作系统的保护、克隆与还原功能对高校机房至关重要。
VHDX是微软推出的虚拟硬盘格式，在Windows 8和Windows Server 2012及更高版本中广泛使用。差分磁盘是VHDX的一项核心功能，允许基于一个父磁盘创建多个子磁盘，仅记录子磁盘相对于父磁盘的差异数据。我们可以通过该机制创建差分系统，实现Windows系统的克隆与还原。﻿
﻿https://uploader.shimo.im/f/LaqDzuZkyswgUoST.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE3NDQ3ODg3MzUsImZpbGVHVUlEIjoiNXJrOUt5WTJtMnNsekQzeCIsImlhdCI6MTc0NDc4ODQzNSwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwicGFhIjoiYWxsOmFsbDoiLCJ1c2VySWQiOjU1MTQ4MDkyfQ.yubk5XFznCUS12-OiDxAu7TU9FsPbs0A-YdT-RmZNeY![image](https://github.com/user-attachments/assets/590567f2-b0c6-4dbf-ba82-012b2f9d3017)
Ventoy是一个多系统启动盘制作工具，通过动态加载多系统镜像文件（如ISO/WIM/VHDX）并模拟为虚拟磁盘，由GRUB生成启动菜单，实现灵活启动不同操作系统的机制。但GRUB不具备文件系统的写入权限，需要调用外部程序创建VHDX镜像。例如Clonezilla是一个分区和磁盘克隆工具，通过GRUB引导Clonezilla实现创建VHDX，进而实现系统保护与还原，但Clonezilla无法引导进入系统，需要重启再通过GRUB进入差分系统。我们可以对Windows或者linux中的Bootloader进行修改，使其能够通过文件系统修改、覆盖vhdx差分文件还原差分系统，并引导进入该差分系统的Bootloader；同时，还可实现Windows系统和Linux系统的Bootloader之间跨内核跳转。

###  预期目标
- 实现通过主系统的Bootloader覆盖、还原本地系统中VHDX差分磁盘。
- 实现从主系统的Bootloader跳转到差分系统的Bootloader。
- 实现Bootloader的链式加载机制，即支持如下两种方式：
- 从a系统直接跳转到b系统或c系统；
- 从a系统依次跳转到b系统，再跳转到c系统。
- 实现多系统的创建、克隆、备份和还原功能。

### 特征
- 不限主系统Bootloader版本，但必须实现Windows vhdx差分系统Bootloader的跳入。
- 实现树状系统差分结构，例如从a系统中派生出b和c两个差分系统，并且必须能够通过Ventoy或其他方式直观地选择要进入的系统。
- 不限制系统覆盖还原工具，可以使用Clonezilla。
- 链式加载必须要实现启动vhdx的Bootloader。

### 参考资料
- 使用VHDX（本机启动）部署Windows（https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/deploy-windows-on-a-vhd--native-boot?view=windows-10）
- Windows中的引导选项概述（https://learn.microsoft.com/en-us/windows-hardware/drivers/devtest/boot-options-in-windows）
- GRUB官方文档（https://www.gnu.org/software/grub/manual/grub/）
- Ventoy官网（https://www.ventoy.net/）
- Clonezilla官网（https://clonezilla.org/）

### 赛题分类
2.2 固件支撑大类 --> 2.2.2 Bootloader开发

### 参赛要求
- 以小组为单位参赛，最多三人一个小组，且小组成员是来自同一所高校的本科生或研究生
- 允许学生参加大赛的多个不同题目，最终自己选择一个题目参与评奖
- 请遵循“2025全国大学生操作系统比赛”的章程和技术方案要求

### 难度
中等

### License
GPL-3.0 License

### 项目导师
- 姓名：刘羽
- 单位：首都师范大学
- email：liuyu@cnu.edu.cn
