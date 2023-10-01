# Raspberry Pi PicoをC/C++で開発

## Overview

C/C++でRaspberry Pi Picoのコードを書きたい

## Usage

### SDK preparation

[SDK Setup](https://www.raspberrypi.com/documentation/microcontrollers/c_sdk.html#sdk-setup)にある[getting started](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf?_gl=1*1prca6p*_ga*MTg2Mjc3MTU2NC4xNjkzNDU4NzQ5*_ga_22FD70LWDS*MTY5NjE1MDMyOS4yLjEuMTY5NjE1MDM1MC4wLjAuMA..) のChapter 2.The SDKを参考にSDKをインストールします。今回は `~/pico-sdk` にリポジトリをクローンし、インストールしたものとします。

`export PICO_SDK_PATH=~/pico-sdk` をシェルのprofileに追加し、シェルを再起動します。

### Build project

このリポジトリをクローンし、通常通りCMakeを構成して (`mkdir build && cd build && cmake ..`) ビルドします。 (`ninja` とか `make` とか)…  
完了すると `/build/src/rpi_pico_blink.uf2` が生成されます。これをRPi Picoに書き込みます。

### Federation with VSCode (CMake Tools)

VSCodeのCMake拡張機能と連携する場合は、コマンドパレットを表示し `cmake:edit user-local cmake kits` と入力して確定します。
構成エディタが開きますので、以下の内容を追記します。

```json
{
  "name": "Raspberry Pi Pico",
  "compilers": {
    "C": "/path/to/arm-none-eabi-gcc",
    "CXX": "/path/to/arm-none-eabi-g++"
  },
  "toolchainFile": "/<homedir>/pico-sdk/cmake/preload/toolchains/pico_arm_gcc.cmake",
  "environmentVariables": {
    "PICO_SDK_PATH": "/<homedir>/pico-sdk"
  },
  "isTrusted": true
}
```

ウィンドウ下のキット選択ボタンをクリックすると「Raspberry Pi Pico」が追加されているはずです。これを選択して「ビルド」をクリックすることで、Raspberry Pi Pico用にプロジェクトをビルドすることができるようになります。
また、この操作によりIntelliSenseが正しく構成され、補完が効くようになります。

## License

This repository is published under [MIT License](LICENSE).
