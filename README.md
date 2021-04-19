[![CI](https://github.com/taiga-tech/lambda-edge-image-convert/actions/workflows/main.yml/badge.svg)](https://github.com/taiga-tech/lambda-edge-image-convert/actions/workflows/main.yml)

クックパッド開発者ブログ (http://techlife.cookpad.com/entry/2018-05-25-lambda-edge) 用のサンプルコード

|キー|値|デフォルト|最大値|補足|
|---|---|---|---|---|
|w|最大横幅(ピクセル)を指定|1200|1200|変換元の画像より大きな値は無効(=拡大しない)|
|h|最大縦幅(ピクセル)を指定|同上|同上|同上|
|p|t (true)：WebP 形式へ変換するf (false)：WebP 形式へ変換しない|f (false)|-|-|

- lamda: runtine node 10.x
- handler: /src/index.handler

## command

```shell
% node -v # 10.x
% npm i
% npm run create-package # create a zip package
```
