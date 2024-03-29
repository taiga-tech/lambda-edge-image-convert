# lambda-edge-image-convert

<!-- https://github.com/lambci/docker-lambda -->

[![CI](https://github.com/taiga-tech/lambda-edge-image-convert/actions/workflows/main.yml/badge.svg)](https://github.com/taiga-tech/lambda-edge-image-convert/actions/workflows/main.yml)

["COOKPAD" the sample code for developers blog was in reference](http://techlife.cookpad.com/entry/2018-05-25-lambda-edge)
Resize images in real time with AWS Lambda @ Edge & convert to WebP format

## Usage

```html
<img src="https://<cloudFrontUrl>/<S3_PATH>?<query>">

<!-- format: webp, height: 200px -->
<img src="https://d2eerjykv09g3.cloudfront.net/demo/img/demo_11.jpg?p=t&h=200">
```

<!-- format: jpg, height: 100px -->
<!-- <img src="https://d2eerjykv09g3.cloudfront.net/demo/img/demo_11.jpg?p=f&h=100"> -->

## Demo

- format: webp, height: 200px
<img src="https://cdn.takahiro-and-michika.com/demo/img/demo_11.jpg?p=t&h=200" alt="demo">

- format: jpg, height: 100px
<img src="https://cdn.takahiro-and-michika.com/demo/img/demo_11.jpg?p=t&h=100" alt="demo">

## Query

| Key | Value                                                       | Delfault  | Maximum | addition                                        |
| --- | ----------------------------------------------------------- | --------- | ------- | ----------------------------------------------- |
| w   | Maximum width(px)                                           | 1200      | 1200    | Values larger than the source image are invalid |
| h   | Maximum hight(px)                                           | 1200      | 1200    | same as above                                   |
| p   | t (true): WebP conversion, <br />f (false): WebP conversion | f (false) | -       | -                                               |


## Command

```shell
% node -v # 14.x
% npm i
% npm run create-package # create a zip package
```

## Lambda Settings

- runtine: node 14.x
- handler: /src/index.handler

## Todo
- [x] Automatic deployment with github actions
- [x] Added format that can be converted
- [x] support for png, but still worried so will fix it.
- [ ] Describes how to install "sharp" on Amazon Linux 2

## References

- https://github.com/aws-actions/configure-aws-credentials
- https://github.com/appleboy/lambda-action
