# MeCab.DotNet

A Japanese language morphological analysis engine for .NET Core.

![MeCab.DotNet](Images/MeCab.DotNet-120.png)

[![NuGet MeCab.DotNet](https://img.shields.io/nuget/v/MeCab.DotNet.svg?style=flat)](https://www.nuget.org/packages/MeCab.DotNet)

# What's this?

["MeCab"](https://github.com/taku910/mecab) is a Japanese language morphological analysis engine.

["NMeCab"](https://ja.osdn.net/projects/nmecab/) is a re-implementation of MeCab engine on .NET Framework 2.0 managed library, but didn't update long time (looks like suspended...)

"MeCab.DotNet" (this project) is a ported of NMeCab on .NET Core 1/2/3 and .NET Frameworks and packed into NuGet format.

# How to use

MeCab.DotNet targetted platforms:
* .NET Core 1/2/3 (Built on .NET Standard 1.3/2.0/2.1)
* .NET Framework 4.0/4.5 or upper.

Changed from NMeCab:
* Wider .NET platform supporting and depricated PCL libraries, .NET Framework 3.5 and lower.
* Changed namespace `NMeCab` to `MeCab`.
* Added more usable methods.

Enabling steps:
1. [Install from NuGet named "MeCab.DotNet"](https://www.nuget.org/packages/MeCab.DotNet).
2. Usually you'll use default dictionary named IPADIC, the package will append `dic` folder into your project automatically. But have to declare `MeCabUseDefaultDictionary` property and set value to `False` inside `PropertyGroup` in csproj if you wanna use your own dictionary.
3. Build and run!

# First step sample code

```csharp
using System;
using MeCab;

namespace ConsoleApp
{
    public static class Program
    {
        public static void Main(string[] args)
        {
            var sentence = "行く川のながれは絶えずして、しかも本の水にあらず。";

            var parameter = new MeCabParam();
            var tagger = MeCabTagger.Create(parameter);

            foreach (var node in tagger.ParseToNodes(sentence))
            {
                if (node.CharType > 0)
                {
                    var features = node.Feature.Split(',');
                    var displayFeatures = string.Join(", ", features);

                    Console.WriteLine($"{node.Surface}\t{displayFeatures}");
                }
            }
        }
    }
}
```

Results:

```
行く    動詞, 自立, *, *, 五段・カ行促音便, 基本形, 行く, イク, イク
川      名詞, 一般, *, *, *, *, 川, カワ, カワ
の      助詞, 連体化, *, *, *, *, の, ノ, ノ
ながれ  動詞, 自立, *, *, 一段, 連用形, ながれる, ナガレ, ナガレ
は      助詞, 係助詞, *, *, *, *, は, ハ, ワ
絶えず  副詞, 一般, *, *, *, *, 絶えず, タエズ, タエズ
し      動詞, 自立, *, *, サ変・スル, 連用形, する, シ, シ
て      助詞, 接続助詞, *, *, *, *, て, テ, テ
、      記号, 読点, *, *, *, *, 、, 、, 、
しかも  接続詞, *, *, *, *, *, しかも, シカモ, シカモ
本      名詞, 一般, *, *, *, *, 本, ホン, ホン
の      助詞, 連体化, *, *, *, *, の, ノ, ノ
水      名詞, 一般, *, *, *, *, 水, ミズ, ミズ
に      助詞, 格助詞, 一般, *, *, *, に, ニ, ニ
あら    動詞, 自立, *, *, 五段・ラ行, 未然形, ある, アラ, アラ
ず      助動詞, *, *, *, 特殊・ヌ, 連用ニ接続, ぬ, ズ, ズ
。      記号, 句点, *, *, *, *, 。, 。, 。
```

# License
Under GPL2, LGPL2.1 derived from NMeCab project.
