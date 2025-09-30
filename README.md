# 这个插件是 local history 我只是给提示和设置那些改成了中文

(原插件地址 [local history](https://marketplace.visualstudio.com/items?itemName=xyz.local-history))

# 本地历史记录 (Local History)

一个用于维护文件本地历史记录的源代码可视化插件。

每次修改文件时，旧内容的副本都会保存在本地历史记录中。

您可以随时将文件与历史记录中的任何旧版本进行比较。

当您意外更改或删除文件时，它可以为您提供帮助。

当您的工作区出现灾难性问题时，历史记录也能帮上忙。

每个文件版本都存储在工作区目录的 .history 文件夹中的单独文件中

（您也可以配置其他位置，请参见 local-history.path 设置）。

例如：.history/foo/bar/myFile_20151212205930.ts

您可以通过资源管理器窗格中的 本地历史记录树轻松浏览历史文件。

点击文件时，会显示与当前版本的比较。

您还可以通过上下文菜单访问其他命令。

![Image of tree](images/Tree.png)

您可以使用不同的视图进行过滤：

全部文件

当前文件（默认）

指定文件（可以输入搜索模式）

## 设置

    "local-history.daysLimit":  30  // 清理本地历史记录的天数限制 (0: 不清理)
    "local-history.maxDisplay": 10 // 使用本地历史记录命令时显示的最大文件数量
    "local-history.saveDelay": 0 // 将文件保存到本地历史记录的延迟秒数 {0: 无延迟}
    "local-history.dateLocale": // 显示日期时使用的区域设置 (例如："fr-CH" 或 "en-GB" 等)
    "local-history.path": // 为 .history 文件夹指定其他位置 (null: 使用工作区文件夹)
        此设置必须是绝对路径。
        路径可以以下列内容开头：
        ${workspaceFolder}: 当前工作区文件夹
            例如：${workspaceFolder}/.vscode 将历史记录保存到每个工作区文件夹的 .vscode/.history 中
        ${workspaceFolder: index}: 特定工作区索引
            例如：工作区文件夹 A, B, C。但始终保存到 A/.history => ${workspaceFolder: 0}
        也可以在路径中使用特定变量：
        - %variable%: 环境变量 (例如：%AppData%)
        - ~: 主目录 (Linux)
        
    "local-history.absolute": // 在 local-history.path 中保存绝对路径或相对路径
        true: (绝对路径) // <local-history.path>/.history/<绝对路径>
        false: (相对路径) // (默认) <local-history.path>/.history/<工作区文件夹名称>/<相对路径>
    "local-history.enabled":
        0: 从不启用 // 可能为某些项目禁用扩展
        1: 总是启用 // (默认) 也为没有工作区文件夹的单个文件保存（必须定义 "local-history.path"）
        2: 仅工作区 // 仅保存工作区文件夹内的文件
    "local-history.exclude": // 不保存的文件或文件夹
        // (默认) ['**/.history/**', '**/.vscode**', '**/node_modules/**', '**/typings/**', '**/out/**']
    "local-history.treeLocation": // 指定树形视图的位置
        explorer (默认): // 在资源管理器项目中显示树形视图
        localHistory: // 在特殊的活动栏项目中显示树形视图

## 命令

    local-history.showAll // 显示所有可用的历史记录（受 maxDisplay 设置限制）
    local-history.showCurrent // 显示当前版本（如果历史版本处于活动状态）
    local-history.compareToCurrent // 将当前版本与历史记录中的另一个版本进行比较
    local-history.compareToActive // 将活动文件与历史记录中的另一个版本进行比较
    local-history.compareToPrevious // 将历史记录中的一个版本与其上一个版本进行比较

## 注意

当 .history 文件夹存储在工作区中时，您可以添加 "files.exclude" 设置。

这会隐藏 .history 文件夹并避免一些问题（例如 csproj 扩展）。
感谢 @pabloarista (issue [#13](https://github.com/zabel-xyz/local-history/issues/13))
