---
title: "C# ile Hive veya Pig hdınsight'ta - Azure hadoop'ta aaaUse | Microsoft Docs"
description: "Bilgi nasıl toouse C# kullanıcı tanımlı işlevler (UDF) Hive veya Pig Azure Hdınsight'ta akış ile."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>C# kullanıcı tanımlı işlevler Hive veya Pig hdınsight'ta Hadoop akış ile kullanma

Nasıl toouse C# kullanıcı Hdınsight üzerinde Apache Hive ve Pig işlevleri (UDF) tanımlanan öğrenin.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Linux tabanlı hem de Windows tabanlı Hdınsight kümeleri ile çalışır. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md).

Her ikisi de Hive ve Pig veri tooexternal uygulamaları işlemek için geçirebilirsiniz. Bu işlem olarak bilinir _akış_. .NET applciation kullanırken hello veri üzerinde STDIN toohello uygulama geçirilen ve Merhaba uygulaması STDOUT üzerinde hello sonuçları döndürür. tooread ve STDIN ve STDOUT yazma, kullanabileceğiniz `Console.ReadLine()` ve `Console.WriteLine()` bir konsol uygulamasından.

## <a name="prerequisites"></a>Ön koşullar

* Yazma ve .NET Framework 4.5 hedefleyen C# kod oluşturma ile benzer.

    * İstediğiniz ne olursa olsun IDE kullanın. Öneririz [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, veya [Visual Studio Code](https://code.visualstudio.com/). Merhaba, bu belgenin kullanımı Visual Studio 2017 adımları.

* Bir şekilde tooupload .exe dosyalarını toohello küme ve çalışma Pig ve Hive işleri. Merhaba Data Lake araçları Visual Studio, Azure PowerShell ve Azure CLI için öneririz. Merhaba bu belgedeki adımları hello Data Lake araçları Visual Studio tooupload hello dosyaları için kullanan ve hello örnek Hive sorgusu çalıştırmak.

    Diğer yolları toorun Hive sorguları ve Pig işleri hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

    * [Apache Hive Hdınsight ile kullanma](hdinsight-use-hive.md)

    * [Hdınsight ile Apache Pig kullanma](hdinsight-use-pig.md)

* Hdınsight kümesi Hadoop'ta. Küme oluşturma ile ilgili daha fazla bilgi için bkz: [bir Hdınsight kümesi oluşturmayı](hdinsight-provision-clusters.md).

## <a name="net-on-hdinsight"></a>Hdınsight üzerinde .NET

* __Linux tabanlı Hdınsight__ kullanarak kümeleri [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET uygulamaları. Mono sürüm 4.2.1 Hdınsight sürüm 3.5 ile dahil edilir.

    .NET Framework sürümleri Mono uyumluluğu hakkında daha fazla bilgi için bkz: [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/).

    toouse Mono, belirli bir sürümünü görmek hello [yükleme veya güncelleştirme Mono](hdinsight-hadoop-install-mono.md) belge.

* __Windows tabanlı Hdınsight__ kümeleri hello Microsoft .NET CLR toorun .NET uygulamalarını kullanın.

Merhaba .NET framework ve Hdınsight sürümleriyle dahil Mono hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md).

## <a name="create-hello-c-projects"></a>Merhaba C oluşturmak\# projeleri

### <a name="hive-udf"></a>UDF yığını

1. Visual Studio'yu açın ve bir çözüm oluşturun. Merhaba proje türü için **konsol uygulaması (.NET Framework)**ve ad hello yeni proje **HiveCSharp**.

    > [!IMPORTANT]
    > Seçin __.NET Framework 4.5__ Linux tabanlı Hdınsight kümesi kullanıyorsanız. .NET Framework sürümleri Mono uyumluluğu hakkında daha fazla bilgi için bkz: [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/).

2. Merhaba Değiştir **Program.cs** hello aşağıdaki ile:

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. Merhaba projeyi oluşturun.

### <a name="pig-udf"></a>Pig UDF

1. Visual Studio'yu açın ve bir çözüm oluşturun. Merhaba proje türü için **konsol uygulaması**ve ad hello yeni proje **PigUDF**.

2. Merhaba Hello içeriğini değiştirin **Program.cs** koddan hello dosyasıyla:

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    Bu uygulama Pig gönderilen hello satırları ve ile başlayan yeniden biçimlendirme satırları ayrıştırır `java.lang.Exception`.

3. Kaydet **Program.cs**ve ardından Merhaba projeyi oluşturun.

## <a name="upload-toostorage"></a>Toostorage karşıya yükle

1. Visual Studio'da açın **Sunucu Gezgini**.

2. **Azure** seçeneğini ve sonra **HDInsight** seçeneğini genişletin.

3. İstenirse, Azure aboneliği kimlik bilgilerinizi girin ve ardından **oturum**.

4. Bu uygulamaya toodeploy istediğiniz hello Hdınsight kümesini genişletin. Bir giriş hello metinle __(varsayılan depolama hesabı)__ listelenir.

    ![Sunucu Gezgini Hello hello küme için depolama hesabı gösterme](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Bu girdi şekilde genişletilebilir, kullanmakta olduğunuz bir __Azure depolama hesabı__ hello küme için varsayılan depolama birimi olarak. Merhaba küme için hello varsayılan depolama tooview hello dosyaları hello girişini genişletin hello çift tıklayın ve ardından __(varsayılan kapsayıcı)__.

    * Bu girdi genişletilemiyor, kullanmakta olduğunuz __Azure Data Lake Store__ hello küme için hello varsayılan depolama birimi olarak. Merhaba küme için hello varsayılan depolama tooview hello dosyaları çift hello __(varsayılan depolama hesabı)__ girişi.

6. tooupload hello .exe dosyaları, yöntemler aşağıdaki hello birini kullanın:

    * Kullanılıyorsa bir __Azure depolama hesabı__hello karşıya yükleme simgesine tıklayın ve ardından toohello Gözat **bin\debug** hello için klasör **HiveCSharp** projesi. Son olarak, hello seçin **HiveCSharp.exe** dosya ve tıklayın **Tamam**.

        ![simgeyi karşıya yükleyin](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Kullanıyorsanız __Azure Data Lake Store__hello dosya listesindeki boş bir alana sağ tıklayın ve ardından __karşıya__. Son olarak, hello seçin **HiveCSharp.exe** dosya ve tıklayın **açık**.

    Bir kez hello __HiveCSharp.exe__ karşıya yükleme tamamlandı, yineleme hello karşıya yükleme işlemi hello için __PigUDF.exe__ dosya.

## <a name="run-a-hive-query"></a>Hive sorgusu çalıştırma

1. Visual Studio'da açın **Sunucu Gezgini**.

2. **Azure** seçeneğini ve sonra **HDInsight** seçeneğini genişletin.

3. Merhaba dağıtılan sağ hello küme **HiveCSharp** için uygulama ve ardından **Hive sorgusu yaz**.

4. Metin hello Hive sorgusu için aşağıdaki hello kullan:

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > Merhaba açıklamadan çıkarın `add file` kümeniz için kullanılan varsayılan depolama hello türüyle eşleşen deyimi.

    Bu sorgu hello seçer `clientid`, `devicemake`, ve `devicemodel` alanlarını `hivesampletable`ve toohello HiveCSharp.exe uygulama hello alanları geçirir. Merhaba sorgu bekliyor olarak depolanan hello uygulama tooreturn üç alanları, `clientid`, `phoneLabel`, ve `phoneHash`. Merhaba sorgu de toofind HiveCSharp.exe hello kök hello varsayılan storage kapsayıcısının bekliyor.

5. Tıklatın **gönderme** toosubmit hello iş toohello Hdınsight kümesi. Merhaba **Hive işi Özet** penceresi açılır.

6. Tıklatın **yenileme** toorefresh hello kadar Özet **iş durumu** çok değiştirir**tamamlandı**. tooview hello iş çıktısı, tıklatın **iş çıktısı**.

## <a name="run-a-pig-job"></a>Pig işi çalıştırma

1. Yöntemleri tooconnect tooyour Hdınsight kümesi aşağıdaki hello birini kullanın:

    * Kullanıyorsanız bir __Linux tabanlı__ Hdınsight küme, SSH kullanın. Örneğin, `ssh sshuser@mycluster-ssh.azurehdinsight.net`. Daha fazla bilgi için bkz: [SSH kullanma withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
    
    * Kullanıyorsanız bir __Windows tabanlı__ Hdınsight kümesi [Uzak Masaüstü kullanarak bağlan toohello küme](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. Komut toostart hello Pig komut satırı izleyen bir hello kullan:

        pig

    > [!IMPORTANT]
    > Windows tabanlı bir küme kullanıyorsanız, komutları bunun yerine aşağıdaki hello kullanın:
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    A `grunt>` komut istemi görüntülenir.

3. Toorun hello .NET Framework uygulama kullanan bir Pig işi aşağıdaki hello girin:

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    Merhaba `DEFINE` deyimi bir diğer ad oluşturur `streamer` hello pigudf.exe uygulamalar için ve `CACHE` hello kümenin varsayılan depolama biriminden yükler. Daha sonra `streamer` hello ile kullanılan `STREAM` işleci tooprocess hello günlük ve dönüş hello veri sütunları bir dizi olarak bulunan tek satır.

    > [!NOTE]
    > Merhaba tarafından akış için kullanılan hello uygulama adı çevrelenen \` (backtick) ne zaman karakter diğer adı, ve ' (tek tırnak) ile kullanıldığında `SHIP`.

4. Merhaba son satırı girdikten sonra hello iş başlamanız gerekir. Metin aşağıdaki çıktı benzer toohello döndürür:

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>Sonraki adımlar

Bu belgede, öğrendiğiniz nasıl toouse bir .NET Framework uygulamasından Hive veya Pig hdınsight'ta. Toolearn nasıl toouse Hive veya Pig, ile Python görmek isterseniz [kullanım Python Hive veya Pig hdınsight'ta ile](hdinsight-python.md).

Diğer yolları toouse Pig ve Hive ve MapReduce kullanma hakkında toolearn için belgeler aşağıdaki hello bakın:

* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [Hdınsight ile MapReduce kullanma](hdinsight-use-mapreduce.md)
