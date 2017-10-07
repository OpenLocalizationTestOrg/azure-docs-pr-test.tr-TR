---
title: "aaaUse C# ile MapReduce hdınsight'ta - Azure hadoop'ta | Microsoft Docs"
description: "Bilgi nasıl Azure hdınsight'ta Hadoop ile toouse C# toocreate MapReduce çözümler."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>C# MapReduce hdınsight'ta Hadoop akış ile kullanma

Bilgi nasıl toouse C# toocreate hdınsight'ta MapReduce çözümü.

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md).

Hadoop akış, bir komut dosyası veya yürütülebilir dosyası kullanan toorun MapReduce işleri sağlayan bir yardımcı programıdır. Bu örnekte, .NET kullanılan tooimplement hello Eşleyici ve word sayısı çözüm reducer ' dir.

## <a name="net-on-hdinsight"></a>Hdınsight üzerinde .NET

__Linux tabanlı Hdınsight__ kümeleri kullanım [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET uygulamaları. Mono sürüm 4.2.1 Hdınsight sürüm 3.5 ile dahil edilir. Hdınsight ile dahil Mono hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md). toouse Mono, belirli bir sürümünü görmek hello [yükleme veya güncelleştirme Mono](hdinsight-hadoop-install-mono.md) belge.

.NET Framework sürümleri Mono uyumluluğu hakkında daha fazla bilgi için bkz: [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/).

## <a name="how-hadoop-streaming-works"></a>Hadoop akış nasıl çalışır

Bu belgede akış için kullanılan Hello temel işlem aşağıdaki gibidir:

1. Hadoop veri toohello Eşleyici (Bu örnekte mapper.exe) üzerinde STDIN geçirir.
2. Merhaba Eşleyici hello veri işler ve sekmeyle anahtar/değer çiftleri tooSTDOUT yayar.
3. Merhaba çıktı tarafından Hadoop okuyun ve ardından toohello reducer (Bu örnekte reducer.exe) üzerinde STDIN geçirildi.
4. Merhaba reducer sekmeyle hello anahtar/değer çiftleri okur, hello verileri işler ve STDOUT üzerinde sekmeyle anahtar/değer çiftleri olarak hello sonuç yayar.
5. Merhaba çıktı Hadoop tarafından okunabilir ve toohello çıktı dizini yazılabilir.

Akış ile ilgili daha fazla bilgi için bkz: [Hadoop akış (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).

## <a name="prerequisites"></a>Ön koşullar

* Yazma ve .NET Framework 4.5 hedefleyen C# kod oluşturma ile benzer. Merhaba, bu belgenin kullanımı Visual Studio 2017 adımları.

* Bir şekilde tooupload .exe dosyaları toohello kümesi. Merhaba bu belgedeki adımları hello Data Lake araçları Visual Studio tooupload hello dosyaları tooprimary hello kümesi için kullanır.

* Azure PowerShell veya SSH istemcisi.

* Hdınsight kümesi Hadoop'ta. Küme oluşturma ile ilgili daha fazla bilgi için bkz: [bir Hdınsight kümesi oluşturmayı](hdinsight-provision-clusters.md).

## <a name="create-hello-mapper"></a>Merhaba Eşleyici oluşturma

Visual Studio'da yeni bir oluşturma __konsol uygulaması__ adlı __Eşleyici__. Merhaba uygulaması için kod aşağıdaki hello kullan:

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

Merhaba uygulaması oluşturduktan sonra tooproduce hello yapı `/bin/Debug/mapper.exe` hello proje dizininde dosya.

## <a name="create-hello-reducer"></a>Merhaba reducer oluşturma

Visual Studio'da yeni bir oluşturma __konsol uygulaması__ adlı __reducer__. Merhaba uygulaması için kod aşağıdaki hello kullan:

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

Merhaba uygulaması oluşturduktan sonra tooproduce hello yapı `/bin/Debug/reducer.exe` hello proje dizininde dosya.

## <a name="upload-toostorage"></a>Toostorage karşıya yükle

1. Visual Studio'da açın **Sunucu Gezgini**.

2. **Azure** seçeneğini ve sonra **HDInsight** seçeneğini genişletin.

3. İstenirse, Azure aboneliği kimlik bilgilerinizi girin ve ardından **oturum**.

4. Bu uygulamaya toodeploy istediğiniz hello Hdınsight kümesini genişletin. Bir giriş hello metinle __(varsayılan depolama hesabı)__ listelenir.

    ![Sunucu Gezgini Hello hello küme için depolama hesabı gösterme](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Bu girdi şekilde genişletilebilir, kullanmakta olduğunuz bir __Azure depolama hesabı__ hello küme için varsayılan depolama birimi olarak. Merhaba küme için hello varsayılan depolama tooview hello dosyaları hello girişini genişletin hello çift tıklayın ve ardından __(varsayılan kapsayıcı)__.

    * Bu girdi genişletilemiyor, kullanmakta olduğunuz __Azure Data Lake Store__ hello küme için hello varsayılan depolama birimi olarak. Merhaba küme için hello varsayılan depolama tooview hello dosyaları çift hello __(varsayılan depolama hesabı)__ girişi.

5. tooupload hello .exe dosyaları, yöntemler aşağıdaki hello birini kullanın:

    * Kullanılıyorsa bir __Azure depolama hesabı__hello karşıya yükleme simgesine tıklayın ve ardından toohello Gözat **bin\debug** hello için klasör **Eşleyici** projesi. Son olarak, hello seçin **mapper.exe** dosya ve tıklayın **Tamam**.

        ![simgeyi karşıya yükleyin](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Kullanıyorsanız __Azure Data Lake Store__hello dosya listesindeki boş bir alana sağ tıklayın ve ardından __karşıya__. Son olarak, hello seçin **mapper.exe** dosya ve tıklayın **açık**.

    Bir kez hello __mapper.exe__ karşıya yükleme tamamlandı, yineleme hello karşıya yükleme işlemi hello için __reducer.exe__ dosya.

## <a name="run-a-job-using-an-ssh-session"></a>Bir işi çalıştırın: bir SSH oturumu kullanma

1. SSH tooconnect toohello Hdınsight kümesi kullanın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Komut toostart hello MapReduce işi aşağıdaki hello birini kullanın:

    * Kullanıyorsanız __Data Lake Store__ varsayılan depolama olarak:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * Kullanıyorsanız __Azure Storage__ varsayılan depolama olarak:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    Her bir parametreyi yaptığı listesi aşağıdaki hello açıklanmaktadır:

    * `hadoop-streaming.jar`: MapReduce işlevselliği akış hello içeren hello jar dosyasını.
    * `-files`: Ekler Merhaba `mapper.exe` ve `reducer.exe` dosyaları toothis işi. Merhaba `adl:///` veya `wasb:///` her dosya hello yolu toohello hello kümesi için varsayılan depolama köküdür önce.
    * `-mapper`: Hello Eşleyici hangi dosya uygulayan belirtir.
    * `-reducer`: Merhaba reducer hangi dosya uygulayan belirtir.
    * `-input`: hello giriş verileri.
    * `-output`: hello çıktı dizini.

3. Merhaba MapReduce işi tamamlandıktan sonra tooview hello sonuçları aşağıdaki hello kullan:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Merhaba aşağıdaki metni, bu komutu tarafından döndürülen hello veri örneğidir:

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>Bir işi çalıştırın: PowerShell'i kullanma

PowerShell komut dosyası toorun bir MapReduce işi aşağıdaki hello kullanın ve hello sonuçları indirin.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

Bu komut dosyası hello küme oturum açma hesabı adı ve parola, hello Hdınsight küme adı ile birlikte ister. Merhaba işi tamamlandıktan sonra indirilen toohello hello çıkış olduğu `output.txt` olan hello dizin hello betik dosyasında çalıştı. Merhaba aşağıdaki metni hello hello verilerde örneğidir `output.txt` dosyası:

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>Sonraki adımlar

Hdınsight ile MapReduce kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile MapReduce kullanma](hdinsight-use-mapreduce.md).

C# Hive veya Pig kullanma hakkında daha fazla bilgi için bkz: [C# kullanıcı tanımlı işlev Hive veya Pig kullanmak](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).

C# Hdınsight üzerinde Storm ile kullanma hakkında daha fazla bilgi için bkz: [Hdınsight üzerinde Storm için C# topolojileri](hdinsight-storm-develop-csharp-visual-studio-topology.md).