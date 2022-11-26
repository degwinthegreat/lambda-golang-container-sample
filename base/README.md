1. RIEをインストール
```
mkdir -p ~/.aws-lambda-rie && curl -Lo ~/.aws-lambda-rie/aws-lambda-rie \
                   https://github.com/aws/aws-lambda-runtime-interface-emulator/releases/latest/download/aws-lambda-rie \
                   && chmod +x ~/.aws-lambda-rie/aws-lambda-rie
```
1. docker build
`docker build -t hello-lambda-base .`

1. RIEを差し込みつつ、docker run
`docker run -d -v ~/.aws-lambda-rie:/aws-lambda -p 9000:8080 --entrypoint /aws-lambda/aws-lambda-rie hello-lambda-base "/main"`

1. 実行
```
 curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{ "name": "lambda"}'
"Hello lambda!"⏎
```
