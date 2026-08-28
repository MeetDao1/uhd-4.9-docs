# UHD 4.9 Documentation

UHD v4.9.0.0 文档源仓库（Read the Docs）。本仓库为构建 UHD 手册所需的**最小源码集**：
`host/`（手册 `.dox`、API 头文件、Sphinx 外壳）、`fpga/docs/`（FPGA 手册 Markdown）、
`images/`（镜像清单）。Doxygen 生成手册 HTML，Sphinx 仅作为 Read the Docs 外壳
（与用户手册相同的方式，"cheat Sphinx by running Doxygen instead"）。

## 在线 & 离线文档

- **项目页**：https://app.readthedocs.org/projects/uhd-49-docs/
- **在线文档**：https://uhd-49-docs.readthedocs.io/en/latest/
- **离线下载（Offline formats，已启用）**：https://readthedocs.org/projects/uhd-49-docs/downloads/
  - `htmlzip` — **完整手册离线包**（全部 Doxygen HTML 页面 + 搜索索引，推荐离线使用）
  - `pdf` / `epub` — 由 Sphinx 生成的附加格式（简版）

UHD 4.9（v4.9.0.0）提供完整离线文档：设备手册（Part I）、开发手册与 API 参考（Part II）、
FPGA 手册（Part III）。每次推送本仓库会自动重新构建并更新所有格式。

## 构建流程（Read the Docs 自动执行）

配置见 `.readthedocs.yaml`：

1. conda 环境：`host/docs/sphinx/environment.yml`
   （含 sphinx、cmake、compilers、**doxygen**）
2. Sphinx 配置：`host/docs/sphinx/source/conf.py`
   - 调用 `cmake ../.. -DUHD_BOOST_REQUIRED=OFF -DENABLE_LIBUHD=OFF
     -DENABLE_MAN_PAGES=OFF -DENABLE_DOXYGEN_FULL=ON` 并 `make doxygen_docs`
   - 生成的 `html_extra_path` 直接发布 Doxygen 手册 HTML

## 本地验证（可选）

```bash
cd host/docs/sphinx/source
sphinx-build -b html . ../../build_doxygen_local   # 需先安装 doxygen、cmake
```

## 更新手册源码

本仓库仅包含构建文档所需子集。如需同步上游完整源码：

```bash
git remote add upstream https://github.com/EttusResearch/uhd.git
git fetch upstream v4.9.0.0
```
