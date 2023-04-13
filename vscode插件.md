# 图片文件管理器

修改： 复制的时候，生成的是一个组件，并包含宽和高的属性。

mac 步骤（先下载插件）： vscode 下载 “图片文件管理” 插件 作者： kimtakuang

1.  cd ./.vscode/extensions
2.  修改插件代码
    2.1. npm install image-size
    2.2 webview.js 中

        ```
        // 引入 image-size
        const sizeOf = require("image-size");

        // sendData 函数修改如下：
        const src = context.path;
        const pic = [".png", ".jpg", ".jpeg", ".svg"];
        const result = [];
        // 读取文件夹下图片数据
        const arr = fs.readdirSync(src);
        arr.forEach((el) => {
          const dimensions = sizeOf(path.join(src, el));
          console.log(dimensions.width, dimensions.height);

          const stat = fs.statSync(path.join(src, el));
          if (!stat.isDirectory()) {
            const filepath = path.join(src, el);
            const onDiskPath = vscode.Uri.file(filepath);
            const url = panel.webview.asWebviewUri(onDiskPath).toString();
            const ext = path.extname(path.join(src, el));
            if (pic.includes(ext)) {
              result.push({
                url,
                path: filepath,
                name: el,
                w: dimensions.width,
                h: dimensions.height,
              });
            }
          }
        });
        panel.webview.postMessage({ type: "update", piclist: result });
        ```

    2.3 index.js 中 fileCopy 函数中增加：

    ```
      let w = (target.dataset["w"] / 3).toFixed(2);
      let h = (target.dataset["h"] / 3).toFixed(2);
      let c =`<image-com :src="@/assets/${name}" :w="${w}" :h="${h}" class="" ></image-com>`;

    ```

3.  执行 npm install && vsce package, 然后安装新生成的插件即可。
