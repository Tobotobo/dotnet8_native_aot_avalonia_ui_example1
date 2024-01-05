# dotnet8_native_aot_avalonia_ui_example1

## 概要

.NET 8 で Avalonia UI + NativeAOT が可能か検証する。  

Avalonia UI  
https://avaloniaui.net/  

## とりあえず普通に動かす

Create and Run a Project  
https://docs.avaloniaui.net/docs/get-started/test-drive/create-a-project

```
dotnet new install Avalonia.Templates
```

```
dotnet new avalonia.app -o GetStartedApp
```

```
dotnet run --project GetStartedApp
```

![実行結果イメージ](doc/image/2024-01-06-03-13-51.png)

## NativeAOT化

### 結果  
→　起動できた(※)  
→　PDB ファイルを抜くと約 35 MB (exe 以外に dll があり計 4 ファイル) 

※ビルド中に色々警告は出てたので、全ての機能が正常に動くかは不明

### 詳細

GetStartedApp\GetStartedApp.csproj
```xml
<PropertyGroup>
    <PublishAot>true</PublishAot>　★追加
</PropertyGroup>
```

```
dotnet publish GetStartedApp
```
何か色々警告出てるけど…

![](doc/image/2024-01-06-03-23-52.png)

![](doc/image/2024-01-06-03-25-24.png)

普通に動いてワロタ

![](doc/image/2024-01-06-03-26-28.png)

### 参考

NativeAOT せず SingleFile でビルドした場合  
→　約 90 MB (※)

※PDF ファイル込みだとこっちの方が小さい。なんで？

```xml
<PropertyGroup>
    <!-- <PublishAot>true</PublishAot> -->
    <PublishSingleFile>true</PublishSingleFile>
</PropertyGroup>
```

![](doc/image/2024-01-06-05-04-57.png)

## クロスコンパイル可能か

とりあえず NativeAOT では無理。  
そもそも NativeAOT がクロスコンパイルをサポートしていない。

TODO  
SingleFile の場合はクロスコンパイル可能か。