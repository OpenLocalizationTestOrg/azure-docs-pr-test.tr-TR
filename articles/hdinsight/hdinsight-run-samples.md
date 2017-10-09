---
title: "aaaRun hello Hadoop örnekleri Hdınsight - Azure | Microsoft Docs"
description: "Hello Azure Hdınsight hizmeti sağlanan hello örnekleriyle kullanmaya başlayın. MapReduce programları veri kümelerinde çalışan bir PowerShell komut dosyası kullanın."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a>Hadoop MapReduce Windows tabanlı Hdınsight'ta örneklerini çalıştırma
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Örnekleri bir dizi MapReduce işleri kullanma Azure Hdınsight Hadoop kümeleri üzerinde çalışan başlamak toohelp sağlanır. Bu örneklerin her hello Hdınsight oluşturduğunuz yönetilen kümeleri kullanılabilir hale getirilir. Bu örnekleri çalıştırma hakkında bilgi edinin, Azure PowerShell cmdlet'leri toorun işleri Hadoop kümeleri kullanarak.

* [**Word sayısı**][hdinsight-sample-wordcount]: bir metin dosyasındaki word oluşum sayar.
* [**C# sözcük sayımı akış**][hdinsight-sample-csharp-streaming]: bir metin dosyası kullanarak sayıları word oluşum hello Hadoop akış arabirimi.
* [**Pi tahmin**][hdinsight-sample-pi-estimator]: bir istatistik kullanır (yarı Monte Carlo) yöntemi tooestimate hello pi değerini.
* [**10 GB Graysort**][hdinsight-sample-10gb-graysort]: Hdınsight kullanarak genel amaçlı GraySort bir 10 GB dosyasını çalıştırın. Üç işleri toorun vardır: Teragen toogenerate hello veri, Terasort toosort hello veri ve Teravalidate tooconfirm hello veri doğru sıralanmıştır.

> [!NOTE]
> Merhaba kaynak kodu hello ek bulunabilir.

Java tabanlı MapReduce programlama ve akış ve Windows PowerShell içinde kullanılan hello cmdlet'leri ile ilgili belgeler gibi Hadoop ilgili teknolojileri için hello Web'de çok ek belgeler mevcut betik oluşturma. Bu kaynaklar hakkında daha fazla bilgi için bkz:

* [Hdınsight'ta Hadoop için Java MapReduce programlar geliştirmek](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [HDInsight'ta Hadoop işlerini gönderme](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Giriş tooAzure Hdınsight][hdinsight-introduction]

Günümüzde, çoğu kişi Hive veya Pig MapReduce seçin.  Daha fazla bilgi için bkz.

* [Hdınsight'ta Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta pig kullanma](hdinsight-use-pig.md)

**Önkoşullar**:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Hdınsight kümesi**. Merhaba, bu tür kümeler oluşturulabilir çeşitli yollar hakkında yönergeler için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).
* **Azure PowerShell içeren bir iş istasyonu**.

    > [!IMPORTANT]
    > Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışıdır** ve 1 Ocak 2017 tarihine kadar kaldırılacaktır. Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.
    >
    > Hello adımları [yüklemek ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs) tooinstall hello en son Azure PowerShell sürümü. Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="hdinsight-sample-wordcount"></a>Sayısı - Java word
MapReduce proje toosubmit, önce bir MapReduce işi tanımı oluşturun. Merhaba iş tanımında hello MapReduce program jar dosyasını ve hello jar dosyasını hello konumunu belirtin **wasb:///example/jars/hadoop-mapreduce-examples.jar**hello sınıf adı ve hello bağımsız değişkenler.  Merhaba wordcount MapReduce program iki bağımsız değişkeni alır: kullanılan toocount sözcükleri ve çıktı hello konumunu hello kaynak dosya.

Merhaba kaynak kodu hello bulunabilir [ek A](#apendix-a---the-word-count-MapReduce-program-in-java).

Java MapReduce geliştirmenin hello yordamı için program için bkz: - [hdınsight'ta Hadoop için Java MapReduce geliştirmek programlar](hdinsight-develop-deploy-java-mapreduce-linux.md)

**toosubmit bir word sayısı MapReduce işi**

1. Açık **Windows PowerShell ISE**. Yönergeler için bkz: [yükleyin ve Azure PowerShell yapılandırma][powershell-install-configure].
2. PowerShell Betiği aşağıdaki hello yapıştırın:

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    Merhaba MapReduce işi adlı bir dosya oluşturur *bölümü r 00000*sözcükleri içerir ve hello sayar. Merhaba komut dosyası kullanan hello **findstr** tüm hello toolist sözcükleri komutu içeren *"yok"*.
3. Merhaba ilk üç değişkenleri ayarlayın ve hello komut dosyasını çalıştırın.

## <a name="hdinsight-sample-csharp-streaming"></a>Sayısı - C# akış word
Hadoop, toowrite eşleme sağlar ve Java dışındaki dillerde işlevleri azaltmak akış bir API tooMapReduce sağlar.

> [!NOTE]
> Bu öğreticide Hello adımlar yalnızca tooWindows tabanlı Hdınsight kümeleri geçerlidir. Linux tabanlı Hdınsight kümeleri için akış örneği için bkz: [programları Hdınsight için akış Python geliştirme](hdinsight-hadoop-streaming-python.md).

Merhaba örneği, hello Eşleyici ve hello reducer hello girdiden okunan yürütülebilir dosyalar [stdin] [ stdin-stdout-stderr] (--satır) ve hello çıkış çok yayma[stdout] [stdin-stdout-stderr]. Merhaba program hello metin tüm hello sözcükleri sayar.

İçin yürütülebilir bir dosya belirtildiğinde **mappers**, hello Eşleyici başlatıldığında hello ayrı bir işlem yürütülebilir her Eşleyici görev başlatır. Merhaba Eşleyici görev çalıştırır, kendi giriş satırlarına dönüştürür ve akışları hello satırları toohello [stdin] [ stdin-stdout-stderr] hello işleminin.

Hello bu arada, hello Eşleyici hello satır yönelimli çıktı hello işlem hello stdout'tan toplar. Merhaba Eşleyici hello çıkış olarak toplanan bir anahtar/değer çifti her satırın dönüştürür. Varsayılan olarak, toohello ilk sekme karakteri hizalamak hello öneki hello anahtar ve hello kalan (Merhaba sekme karakteri hariç) hello satırının başlangıç değeridir. Merhaba satırda sekme karakteri varsa, tüm satırı başlangıç anahtarı olarak kabul edilir ve hello değeri null.

İçin yürütülebilir bir dosya belirtildiğinde **reducers**, hello reducer başlatıldığında hello ayrı bir işlem yürütülebilir her reducer görev başlatır. Merhaba reducer görev çalıştırır, kendi giriş anahtar/değer çiftleri satırlarına dönüştürür ve hello satırları toohello akışları [stdin] [ stdin-stdout-stderr] hello işleminin.

Hello hello reducer bu arada, hello hello satır yönelimli çıkış toplar [stdout] [ stdin-stdout-stderr] hello işleminin. Merhaba reducer hello çıkış olarak toplanan her satır tooa anahtar/değer çifti dönüştürür. Varsayılan olarak, toohello ilk sekme karakteri hizalamak hello öneki hello anahtar ve hello kalan (Merhaba sekme karakteri hariç) hello satırının başlangıç değeridir.

**word sayısı iş akışında toosubmit C#**

* Merhaba yordamı izleyin [sayısı - Java Word](#word-count-java)ve hello iş tanımı satır aşağıdaki hello ile değiştirin:

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    Merhaba çıktı dosyası olacaktır:

        example/data/StreamingOutput/wc.txt/part-00000

## <a name="hdinsight-sample-pi-estimator"></a>PI tahmin
Merhaba pi tahmin bir istatistik kullanır (yarı Monte Carlo) yöntemi tooestimate hello pi değerini. Rastgele bir birim içinde yerleştirilen noktaları kare ayrıca kalan içinde bu kare hello daire ile bir olasılık eşit toohello alanı içinde bir daire içinde pi/4. pi değerini Hello R hello oranı hello daire toohello toplam sayısı hello kare içinde noktalarını içinde olduğunda puan hello sayısının olduğu 4R başlangıç değerinden tahmin edilebilir. Merhaba büyük hello kullanılan noktaları, hello daha iyi hello tahmin örneğidir.

Bu örnek için sağlanan hello betik Hadoop jar işi gönderir ve bir değerle toorun yukarı 16 haritalar, her biri gerekli toocompute 10 milyon örnek noktaları hello parametre değerlerini tarafından olduğu ayarlanır. Bu parametre değerleri olabilir tooimprove tahmini hello pi değerini değiştirildi. Başvuru için hello ilk 10 ondalık pi'nin 3.1415926535 yerlerdir.

**toosubmit pi tahmin işi**

* Merhaba yordamı izleyin [sayısı - Java Word](#word-count-java)ve hello iş tanımı satır aşağıdaki hello ile değiştirin:

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <a name="hdinsight-sample-10gb-graysort"></a>10 GB Graysort
Bu örnek uygun bir 10 GB veri kullanır, böylece oldukça hızlı bir şekilde çalıştırılabilir. Merhaba MapReduce uygulamaları Owen O'Malley ve 2009 0.578 TB/dak (100 TB 173 dakika cinsinden) oranı ile Merhaba yıllık genel amaçlı ("daytona") terabayt sıralama Kıyaslama won Arun Murthy tarafından geliştirilen kullanır. Bu ve diğer sıralama değerlendirmeleri hakkında daha fazla bilgi için bkz: Merhaba [Sortbenchmark](http://sortbenchmark.org/) site.

Bu örnek, MapReduce programlar üç kümesi kullanır:

1. **TeraGen** veri toosort toogenerate hello satırlarını kullanabileceğiniz bir MapReduce programdır.
2. **TeraSort** hello giriş verisi örnekleri ve toplam sıralamaya MapReduce toosort hello verilerini kullanır. TeraSort standart sıralama MapReduce işlevlerin her azaltın hello anahtar aralığını tanımlamak örneklenen N-1 anahtarları sıralı listesini kullanan özel bir bölümleyici dışında ' dir. Özellikle, [i-1] örnek tüm anahtarları böyle < = anahtar < örnek [i] tooreduce gönderilen ediyorum. Bu hello çıktısını azaltmak i + 1 değerinden hello çıkışları i azaltmak garanti tüm.
3. **TeraValidate** bu hello çıkışı doğrulayan bir MapReduce programı genel sıralanmış olan. Merhaba çıktı dizini içinde dosya başına bir harita oluşturur ve her eşleme her anahtar değerinden küçük veya buna eşit olmasını sağlar toohello öncekinin. Hello harita işlevi de oluşturur hello kayıtlarının ilk ve son anahtarları her dosya ve hello azaltmak işlevi bu hello sağlar i dosyasının ilk anahtar hello son anahtarı dosyası i-1 büyük. Herhangi bir sorun hello bir çıkış olarak bildirilen bozuk hello anahtarlarla azaltın.

Merhaba giriş ve çıkış biçimi, tüm üç uygulamaları tarafından kullanılan okur ve hello metin dosyaları hello doğru biçimde yazar. Merhaba Hello çıktısını azaltmak hello Kıyaslama bağlamı bağlamı hello çıktı verilerini toomultiple düğümlerinde çoğaltılması gerektirmediğinden çoğaltma hello varsayılan 3, yerine too1 ayarladı.

Üç görev hello örnek, karşılık gelen her tooone hello girişte açıklanan hello MapReduce programlar tarafından gereklidir:

1. Merhaba çalıştırarak sıralamak için hello verileri oluşturmak **TeraGen** MapReduce işi.
2. Merhaba çalıştırarak hello verileri sıralama **TeraSort** MapReduce işi.
3. Merhaba verileri doğru şekilde hello çalıştırarak sıralandıktan olduğunu onaylayın **TeraValidate** MapReduce işi.

**toosubmit hello işleri**

* Merhaba yordamı izleyin [sayısı - Java Word](#word-count-java), kullanım hello izleyerek iş tanımları:

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a>Sonraki adımlar
Bu makale ve her hello örnekleri hello makalelerde, nasıl toorun hello örnekleri ile Merhaba Hdınsight kümeleri Azure PowerShell kullanarak dahil öğrendiniz. Hdınsight ile Pig, Hive ve MapReduce kullanma hakkında daha fazla öğreticileri için aşağıdaki konularda hello bakın:

* [Hadoop ile Hive Hdınsight tooanalyze mobil ahize kullanımda kullanmaya başlama][hdinsight-get-started]
* [Hdınsight'ta Hadoop ile pig kullanma][hdinsight-use-pig]
* [Hdınsight'ta Hadoop ile Hive kullanma][hdinsight-use-hive]
* [Hdınsight'ta Hadoop işleri gönderme][hdinsight-submit-jobs]
* [Azure Hdınsight SDK Belgeleri][hdinsight-sdk-documentation]

## <a name="appendix-a---hello-word-count-source-code"></a>Ek A - hello Word sayısı kaynak kodu

```java
package org.apache.hadoop.examples;
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
    extends Mapper<Object, Text, Text, IntWritable>{

private final static IntWritable one = new IntWritable(1);
private Text word = new Text();

public void map(Object key, Text value, Context context
                ) throws IOException, InterruptedException {
    StringTokenizer itr = new StringTokenizer(value.toString());
    while (itr.hasMoreTokens()) {
    word.set(itr.nextToken());
    context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
    extends Reducer<Text,IntWritable,Text,IntWritable> {
private IntWritable result = new IntWritable();

public void reduce(Text key, Iterable<IntWritable> values,
                    Context context
                    ) throws IOException, InterruptedException {
    int sum = 0;
    for (IntWritable val : values) {
    sum += val.get();
    }
    result.set(sum);
    context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
Configuration conf = new Configuration();
String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
if (otherArgs.length != 2) {
    System.err.println("Usage: wordcount <in> <out>");
    System.exit(2);
    }
Job job = new Job(conf, "word count");
job.setJarByClass(WordCount.class);
job.setMapperClass(TokenizerMapper.class);
job.setCombinerClass(IntSumReducer.class);
job.setReducerClass(IntSumReducer.class);
job.setOutputKeyClass(Text.class);
job.setOutputValueClass(IntWritable.class);
FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
    }
```

## <a name="appendix-b---hello-word-count-streaming-source-code"></a>Ek B - kaynak kodu akış hello sözcük sayımı
Merhaba azaltmak gibi arabirimi toocount hello bir belgeden akışı sözcük sayısını hello MapReduce program hello konsoluna bir eşleme arabirimi toostream hello metin olarak Merhaba cat.exe uygulaması ve Merhaba wc.exe uygulaması kullanır. Merhaba Eşleyici ve reducer hello standart giriş akışından (stdin) karakterleri, satır satır, okuma ve toohello standart çıktı akışı (stdout) yazma.

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

Merhaba hello cat.cs dosya kullandığı Eşleyici kodda bir [StreamReader] [ streamreader] nesne tooread hello karakter günlüklerden hello akış toohello standart çıktı akışı hello gelen akış toohello konsolunun Merhaba statik ile [Console.Writeline] [ console-writeline] yöntemi.

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

Merhaba hello wc.cs dosya kullanır reducer kodda bir [StreamReader] [ streamreader] tooread karakter akışından çıkış hello cat.exe Eşleyicisi tarafından kaldırılmış hello standart giriş nesnesi. Merhaba hello karakterlerle okuduğu [Console.Writeline] [ console-writeline] yöntemi, bu sayıları hello sözcükler alanları ve her sözcüğün hello sonuna satır sonu karakterleri sayma. Ardından hello toplam toohello standart çıktı akışı hello ile Yazar [Console.Writeline] [ console-writeline] yöntemi.

## <a name="appendix-c---hello-pi-estimator-source-code"></a>Ek C - hello Pi tahmin kaynak kodu
Merhaba pi tahmin hello Eşleyici ve reducer işlevleri içeren Java kod incelemesi aşağıdaki kullanılabilir. Merhaba Eşleyici program rastgele bir birim kare içinde yerleştirilen noktaları belirtilen sayıda oluşturur ve ardından hello hello daire içinde bu noktalarını sayar. Merhaba reducer program tarafından hello mappers sayılan noktaları toplanır ve hello R hello oranı hello daire toohello toplam sayısı hello kare içinde noktalarını içinde sayılan puan hello sayısının olduğu hello formül 4R gelen pi değerini tahmin eder.

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a>Ek D - hello 10gb graysort kaynak kodu
Merhaba kod hello TeraSort MapReduce program için bu bölümdeki İnceleme için sunulur.

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
