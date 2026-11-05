# imx6ull/linux

i.MX6ULL（正点原子 ATK-DL6Y2C）的 Linux 内核仓库。

- 基线：`linux-imx-4.1.15-2.1.0`（NXP i.MX 4.1.15 BSP，正点原子分支）
- 分支：`main`
- Gerrit：<http://localhost:8080/>
- GitHub 镜像：<https://github.com/WorkerHMan/imx6ull_linux>

## 目录约定

内核源码放在仓库根（`Makefile`、`arch/`、`drivers/` 一级）。

## 编译（在 VM / WSL 里，工具链 `arm-linux-gnueabihf-`）

```bash
# 正点原子出厂配置
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- imx6ull_alientek_emmc_defconfig
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j$(nproc) zImage
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- imx6ull-alientek-emmc.dtb

# 产物
#   arch/arm/boot/zImage
#   arch/arm/boot/dts/imx6ull-alientek-emmc.dtb
```

## 提交规范（Gerrit）

```bash
curl -sS -o .git/hooks/commit-msg http://localhost:8080/tools/hooks/commit-msg
chmod +x .git/hooks/commit-msg

git commit -am "feat: xxx"          # hook 自动加 Change-Id
git push origin HEAD:refs/for/main  # 走评审，不要直推 main
```

## 相关仓库

| 仓库 | 作用 |
|---|---|
| `imx6ull/uboot` | U-Boot v2026.10 + SPL |
| `imx6ull/linux` | 本仓库 |
| `imx6ull/build` | 板级构建脚本与分区方案 |
| `imx6ull/docs` | 项目文档 |

工程用 repo 管理：`repo init -u ssh://guoqiangh@localhost:29418/imx6ull/manifest -b main -m linux.xml`
