---
title: Hadoop - Microsoft Avro Library - Azure aaaSerialize verileri | Microsoft Docs
description: "Bilgi nasıl tooserialize ve hello Microsoft Avro Library toopersist toomemory, veritabanı veya dosya kullanarak hdınsight'ta Hadoop verileri seri durumdan."
keywords: Avro, hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a>Merhaba Microsoft Avro Library hadoop'ta verilerle serileştirme

>[!NOTE]
>Merhaba Avro SDK artık Microsoft tarafından desteklenir. Merhaba, açık kaynak topluluğu desteklenen kitaplığıdır. Merhaba kaynakları hello kitaplığı içinde bulunur [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

Bu konuda gösterilmektedir nasıl toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize nesneleri ve diğer veri yapıları akışları toopersist bunları toomemory, bir veritabanı veya dosya. Ayrıca gösterir nasıl toodeserialize bunları toorecover hello orijinal nesneler.

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a>Apache Avro
Merhaba <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> uygulayan hello hello Microsoft.NET ortamı için Apache Avro verileri seri hale getirme sistem. Apache Avro sıkıştırılmış ikili veri değişim biçimi serileştirme için sağlar. Kullandığı <a href="http://www.json.org" target="_blank">JSON</a> toodefine dil birlikte çalışabilirliğini sağlayan bir dilden bağımsız şemasını. Tek bir dilde seri verilerini başka bir programda okuyabilir. Şu anda C, C++, C#, Java, PHP, Python ve Ruby desteklenir. Merhaba biçim hakkında ayrıntılı bilgi hello bulunabilir <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro belirtimi</a>. 

>[!NOTE]
>Merhaba Microsoft Avro Library hello uzaktan yordam çağrılarını (RPC) bu belirtiminin bir parçası desteklemez.
>

Merhaba Avro sistem bir nesneyi seri hale getirilmiş hello gösterimini iki bölümden oluşur: şema ve gerçek değer. Merhaba Avro şemasının JSON ile seri hale getirilmiş hello veri hello dilden bağımsız veri modeli açıklar. Veri ikili gösterimidir yan yana sunulur. Merhaba ikili gösterimden ayrı Hello şemasına sahip seri hale getirme hızlı ve hello gösterimi küçük yapma hiçbir değer başına ek yüklerine karşılık ile yazılan her nesne toobe izin verir.

## <a name="hello-hadoop-scenario"></a>Merhaba Hadoop senaryosu
Merhaba Apache Avro seri hale getirme biçimi, Azure Hdınsight hem de diğer Apache Hadoop ortamlarında yaygın olarak kullanılır. Avro uygun şekilde toorepresent Hadoop MapReduce işi karmaşık veri yapılarını sağlar. Avro dosyalarının (Avro nesne kapsayıcısı dosyası) Hello biçimi tasarlanmış toosupport hello dağıtılmış MapReduce programlama modelini olmuştur. Merhaba dağıtımına olanak sağlayan hello anahtar hello dosyaların "bölünebilir" olması bir dosyada herhangi bir noktaya arama ve böylelikle belirli bir bloktan itibaren okumaya başlamanız hello herkese açık olmasını özelliğidir.

## <a name="serialization-in-avro-library"></a>Avro Kitaplığı'nda seri hale getirme
Merhaba Avro için .NET kitaplığı biçimlendiricisi nesnelerinin iki yolla destekler:

* **Yansıma** -hello JSON şeması hello türleri için serileştirilmiş hello .NET türleri toobe sözleşme özniteliklerini hello verilerinden otomatik olarak oluşturulur.
* **Genel kayıt** -A JSON şeması hello tarafından temsil edilen bir kayıttaki belirtilen açıkça [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) hiçbir .NET türleri hello veri toobe için mevcut toodescribe hello şema olduğunda sınıfı seri hale getirilmiş.

Merhaba veri şeması tooboth hello yazıcı ve okuyucu hello akışın bilindiğinde hello veri olmadan, şema gönderilebilir. Avro nesne kapsayıcısı dosyası kullanıldığında durumlarda hello şema hello dosyasında depolanır. Veri sıkıştırma için kullanılan hello codec gibi diğer parametrelerle belirtilebilir. Bu senaryolar daha ayrıntılı olarak özetlenen ve kod örnekleri aşağıdaki hello gösterilmiştir:

## <a name="install-avro-library"></a>Avro kitaplığını yükle
Merhaba kitaplığı yüklemeden önce hello gerekli şunlardır:

* <a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a>
* <a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 veya üzeri)

Bu hello Newtonsoft.Json.dll bağımlılık hello Microsoft Avro Library hello yüklemesiyle otomatik olarak karşıdan unutmayın. Merhaba yordamı bölümden hello sağlanır:

Merhaba Microsoft Avro Library Visual Studio'dan aşağıdaki yordamı hello yüklenebilir bir NuGet paketi olarak dağıtılır:

1. Select hello **proje** sekmesi -> **NuGet paketlerini Yönet...**
2. Merhaba, "Microsoft.Hadoop.Avro" için arama **arama çevrimiçi** kutusu.
3. Merhaba tıklatın **yükleme** sonraki çok düğmesini**Microsoft Azure Hdınsight Avro Kitaplığı**.

Bu hello Newtonsoft.Json.dll unutmayın (> 6.0.4 =) bağımlılık da karşıdan otomatik olarak Microsoft Avro Library hello ile.

Merhaba Microsoft Avro Library kaynak kodunu şu adreste [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

## <a name="compile-schemas-using-avro-library"></a>Avro kitaplığını kullanarak şemaları derleme
Merhaba Microsoft Avro Library, otomatik olarak hello üzerinde temel C# türleri oluşturma sağlayan yardımcı JSON şeması önceden tanımlanmış bir kod oluşturma içerir. Başlangıç kodu oluşturma yardımcı programı bir ikili yürütülebilir dağıtılmaz ancak aşağıdaki yordamı hello kolayca oluşturulabilir:

1. Hdınsight SDK kaynak kodundan hello en son sürümü ile Merhaba .zip dosyasını indirdikten <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">için Microsoft .NET SDK Hadoop</a>. (Tıklatın hello **indirin** simgesi, değil hello **indirir** sekmesini.)
2. .NET Framework 4 ile Merhaba makinede Hdınsight SDK tooa dizine yüklü ve gerekli bağımlılık NuGet paketlerini indirmek için toohello Internet bağlı hello ayıklayın. Aşağıda, hello kaynak kodu ayıklanan tooC:\SDK olduğunu varsayın.
3. C:\SDK\src\Microsoft.Hadoop.Avro.Tools toohello klasörüne gidin ve build.bat çalıştırın. (Merhaba dosya MSBuild gelen çağrıları hello .NET Framework hello 32-bit dağıtımı. Toouse hello 64-bit sürümü, düzenleme build.bat isterseniz aşağıdaki içinde hello dosya yorumlar hello.) Merhaba yapı başarılı olduğundan emin olun. (Bazı sistemlerinde MSBuild uyarılar oluşturabilir. Derleme hataları var olduğu sürece bu uyarılar hello yardımcı programı etkilemez.)
4. derlenmiş hello yardımcı programı C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools içinde bulunur.

tooget hello komut satırı sözdizimi ile tanıdık komutu hello kod oluşturma yardımcı programı bulunduğu hello klasöründen aşağıdaki hello yürütün:`Microsoft.Hadoop.Avro.Tools help /c:codegen`

tootest hello yardımcı programı, dosyadan hello kaynak kodu ile sağlanan hello örnek JSON şeması C# sınıfları oluşturabilirsiniz. Merhaba aşağıdaki komutu yürütün:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

Bu tooproduce iki C# dosyalarını hello geçerli dizinde olması: SensorData.cs ve Location.cs.

Merhaba JSON şeması tooC # türleri, dönüştürülürken hello kod oluşturma yardımcı programını kullanarak toounderstand hello mantığı GenerationVerification.feature C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc içinde bulunan hello dosyasına bakın.

Ad alanları hello JSON şemadan hello önceki paragrafta bahsedilen hello dosyasında açıklanan hello mantığı kullanarak ayıklanır. Ad alanları Hello şemadan ayıklanan ne olursa olsun hello yardımcı programı komut satırında hello /n parametresiyle sağlanan üzerinden önceliklidir. Merhaba şema içinde yer alan toooverride hello ad alanları istiyorsanız hello /nf parametresini kullanın. Örneğin, toochange hello SampleJSONSchema.avsc toomy.own.nspace, tüm ad alanlarını yürütme hello komutu:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a>Merhaba örnekleri hakkında
Bu konuda sağlanan altı örnekleri Microsoft Avro Library hello tarafından desteklenen farklı senaryolar gösterilmektedir. Merhaba Microsoft Avro Library akış ile tasarlanmış toowork ' dir. Bu örneklerde, veri veya bellek akışları yerine dosya akışları için veritabanları Basitlik ve tutarlılık aracılığıyla yönetilebilir. bir üretim ortamında gerçekleştirilecek hello yaklaşım hello tam senaryo gereksinimleri, veri kaynağı ve birim, performans ile ilgili kısıtlamalar ve diğer etkenlere bağlıdır.

ilk iki örneklerde nasıl hello tooserialize ve yansıma ve genel kayıtları kullanarak veri akışı arabelleklerini seri durumdan. Merhaba bu iki durumlarda şema hello okuyucuları ve yazıcıları arasında paylaşılan toobe varsayılır bant dışı.

Merhaba üçüncü ve dördüncü örneklerde nasıl tooserialize ve hello Avro nesne kapsayıcısı dosyaları kullanarak veri serisi. Veriler bir Avro kapsayıcı dosyasında depolanır, hello şema çıkarma için paylaşılan gerekir çünkü şemasına her zaman ile depolanır.

Merhaba örnek içeren hello ilk dört örnekler hello indirilebilir <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure Kod örnekleri</a> site.

Merhaba beşinci örnekteki nasıl toouse Avro için özel sıkıştırma codec nesne kapsayıcısı dosyaları. Bu örnek hello indirilebilir hello kodu içeren bir örnek <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure Kod örnekleri</a> site.

Merhaba altıncı örnek nasıl toouse Avro serileştirme tooupload veri tooAzure Blob depolamaya ve Hdınsight (Hadoop) kümesi ile Hive kullanarak Analiz göstermektedir. Merhaba indirilebilir <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure Kod örnekleri</a> site.

Merhaba konuda tartışılan toohello altı örnekleri bağlantılar şunlardır:

* <a href="#Scenario1">**Yansıma ile seri hale getirme** </a> -hello JSON şeması türleri toobe seri için sözleşme öznitelikleri hello verilerinden otomatik olarak oluşturulur.
* <a href="#Scenario2">**Seri hale getirme Genel kaydıyla** </a> -.NET türü yansıma için kullanılabilir duruma geldiğinde hello JSON şeması bir kayıtta açıkça belirtilen.
* <a href="#Scenario3">**Yansıma ile nesne kapsayıcısı dosyaları kullanarak serileştirme** </a> -hello JSON şeması otomatik olarak oluşturulur ve bir Avro nesne kapsayıcısı dosyası aracılığıyla serileştirilmiş hello verilerine birlikte paylaşılan.
* <a href="#Scenario4">**Genel kaydıyla nesne kapsayıcısı dosyaları kullanarak serileştirme** </a> -hello JSON şeması açıkça hello seri hale getirme önce belirtilen ve Avro nesne kapsayıcısı dosyası aracılığıyla hello verilerine birlikte paylaşılan.
* <a href="#Scenario5">**Özel sıkıştırma codec ile nesne kapsayıcısı dosyaları kullanarak serileştirme** </a> -hello örnek, nasıl toocreate bir Avro nesne kapsayıcı dosya hello Deflate veri sıkıştırma codec, özelleştirilmiş bir .NET uygulama gösterir.
* <a href="#Scenario6">**Microsoft Azure Hdınsight hizmeti hello için avro tooupload verileri kullanarak** </a> -hello örnekte, Avro serileştirme hello Hdınsight hizmeti ile nasıl etkileşim kurduğu gösterilmektedir. Bir etkin Azure aboneliği ve erişim tooan Azure Hdınsight küme toorun Bu örnek gereklidir.

## <a name="Scenario1"></a>Örnek 1: Yansıma seri hale getirme
Merhaba JSON şeması hello türleri için otomatik olarak serileştirilmiş hello C# nesnelerini toobe sözleşme özniteliklerini hello Microsoft Avro Library hello verilerden yansıma yoluyla tarafından oluşturulabilir. Merhaba Microsoft Avro Library oluşturur bir [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) serileştirilmiş tooidentify hello alanları toobe.

Bu örnekte, nesneleri (bir **SensorData** üyesi sınıfıyla **konumu** yapısı) serileştirilmiş tooa bellek akışı olan ve bu akış sırayla seri. Bu hello tooconfirm ilk karşılaştırılan toohello örnek sonra hello sonucudur **SensorData** kurtarılan aynı toohello özgün nesnesidir.

Bu örnekte Hello şema hello Avro nesne kapsayıcısı biçimi gerekli olmamasını sağlayacak şekilde hello okuyucuları ve yazıcıları, arasında paylaşılan toobe varsayılır. Bir örnek için nasıl tooserialize ve verileri seri durumdan hello şema hello verilerle paylaşılan gerekir kullanarak yansıma hello nesne kapsayıcısı biçimi ile bellek arabelleği bkz <a href="#Scenario3">yansımailenesnekapsayıcısıdosyalarıkullanarakserihalegetirme</a>.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a>Örnek 2: Genel bir kayıtla seri hale getirme
Veri sözleşmesi ile .NET sınıfları aracılığıyla Hello veri gösterilemez yansıma kullanılamaz bir JSON şeması açıkça bir genel kayıtta belirtilebilir. Bu yöntem, yansıma kullanmaktan daha yavaştır. Böyle durumlarda, hello şeması hello veriler için de başka bir deyişle, derleme zamanında bilinmiyor dinamik olabilir. Veri dönüştürülmüş kadar şema toohello Avro biçimi çalışma zamanında dinamik senaryo bu tür bir örneğidir bilinmiyor (CSV) dosyaları virgülle ayrılmış değerler olarak gösterilir.

Bu örnekte gösterilir nasıl toocreate ve bir [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly belirtin JSON şeması nasıl toopopulate hello veri ve ardından nasıl ile tooserialize ve bu seri. Merhaba sonuç sonra karşılaştırıldığında kurtarılan kayıt hello toohello ilk örnek tooconfirm aynı toohello özgün olduğunu.

Bu örnekte Hello şema hello Avro nesne kapsayıcısı biçimi gerekli olmamasını sağlayacak şekilde hello okuyucuları ve yazıcıları, arasında paylaşılan toobe varsayılır. Bir örnek için nasıl tooserialize ve verileri seri durumdan hello hello şema hello serileştirilmiş verilerle birlikte olması gerektiğinde kullanarak genel bir kayıt hello nesne kapsayıcısı biçimi ile bellek arabelleği bakın <a href="#Scenario4">nesne kapsayıcısı kullanarak seri hale getirme Genel kayıt dosyalarıyla</a> örnek.

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a>Örnek 3: Serileştirme nesne kapsayıcısı dosyaları ve seri hale getirme yansıma ile kullanma
Bu örnekte hello benzer toohello senaryosunda, <a href="#Scenario1"> ilk örnek</a>burada hello şema yansıma ile örtük olarak belirtilir. Merhaba fark vardır hello şema, seri durumdan çıkarır toohello okuyucu bilinen toobe burada varsayılır değil. Merhaba **SensorData** serileştirilmiş nesneler toobe ve bunların örtük olarak belirtilen şema hello tarafından temsil edilen bir Avro nesne kapsayıcısı dosyasında depolanır [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) sınıf.

Bu örnekte ile Merhaba veri serileştirilmiş [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) ve seri durumdan çıkarılmış ile [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx). Merhaba sonuç sonra karşılaştırılan toohello ilk örnekleri tooensure kimliğidir.

Merhaba hello verilerde kapsayıcı dosya hello varsayılan sıkıştırılmış nesne [ **Deflate** ] [ deflate-100] sıkıştırma codec .NET Framework 4. Merhaba bkz <a href="#Scenario5"> beşinci örnek</a> bu konuda toolearn içinde nasıl toouse hello daha yeni ve üst bir sürümünü [ **Deflate** ] [ deflate-110] sıkıştırma codec .NET Framework 4. 5 ' kullanılabilir.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a>Örnek 4: nesne kapsayıcısı dosyaları ve seri hale getirme Genel kaydıyla kullanarak seri hale getirme
Bu örnekte hello benzer toohello senaryosunda, <a href="#Scenario2"> ikinci örnek</a>burada hello şema JSON ile açıkça belirtilir. Merhaba fark vardır hello şema, seri durumdan çıkarır toohello okuyucu bilinen toobe burada varsayılır değil.

Merhaba sınama veri kümesi bir liste halinde toplanan [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) nesneleri açıkça tanımlanmış bir JSON şeması ve hello tarafından temsil edilen bir nesne kapsayıcısı dosyasında depolanan [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) sınıfı. Bu kapsayıcı dosyayı sıkıştırılmamış, kullanılan tooserialize hello veri yazıcısı sonra tooa dosyasını kaydettiğiniz tooa bellek akışı oluşturur. Merhaba [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) hello okuyucusunu oluşturmak için kullanılan parametresi, bu verileri sıkıştırılmaz belirtir.

Merhaba veri sonra hello dosyadan okunan ve nesneleri koleksiyona seri. Bu koleksiyon karşılaştırılan toohello ilk bunların özdeş olduğunu Avro kayıtları tooconfirm listesidir.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a>Örnek 5: özel sıkıştırma codec ile nesne kapsayıcısı dosyaları kullanarak seri hale getirme
Merhaba beşinci örnekteki nasıl toouse Avro için özel sıkıştırma codec nesne kapsayıcısı dosyaları. Bu örnek hello indirilebilir hello kodu içeren bir örnek [Azure Kod örnekleri](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.

Merhaba [Avro belirtimi](http://avro.apache.org/docs/current/spec.html#Required+Codecs) bir isteğe bağlı sıkıştırma codec kullanımına izin verir (Ayrıca çok**Null** ve **Deflate** Varsayılanları). Bu örnekte yeni codec Snappy gibi uygulama değil (Merhaba desteklenen isteğe bağlı codec olarak belirtilen [Avro belirtimi](http://avro.apache.org/docs/current/spec.html#snappy)). Nasıl toouse hello hello .NET Framework 4.5 uygulaması gösterir [ **Deflate** ] [ deflate-110] helloüzerindegöredahaiyibirsıkıştırmaalgoritmasısağlayancodec[zlib](http://zlib.net/) hello varsayılan .NET Framework 4 sürümünden sıkıştırma kitaplığı.

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a>Örnek 6: Merhaba Microsoft Azure Hdınsight hizmeti Avro tooupload verileri kullanma
Bazı programlama tekniklerinin ilgili toointeracting hello Azure Hdınsight hizmeti ile Merhaba altıncı örneği gösterilmektedir. Bu örnek hello indirilebilir hello kodu içeren bir örnek [Azure Kod örnekleri](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.

Merhaba örnek görevleri hello:

* Tooan varolan Hdınsight hizmeti kümesine bağlanır.
* Birkaç CSV dosyaları serileştirir ve hello sonuç tooAzure Blob depolama alanına yükler. (Merhaba CSV dosyaları hello örnek ile birlikte dağıtılır ve AMEX stok geçmiş verileri tarafından dağıtılan bir ayıklama temsil [Infochimps](http://www.infochimps.com/) 1970'ten 2010 hello dönemin. Merhaba örnek CSV dosyası verilerini okur, dönüştürür hello Merhaba, kayıtları tooinstances **hisse senedi** sınıfı ve ardından yansıma kullanarak serileştirir. Stok tür tanımı JSON şeması hello Microsoft Avro Library kod oluşturma yardımcı programı aracılığıyla oluşturulur.
* Adlı yeni bir dış tablo oluşturur **istediğiniz hisse** , kovanında ve toohello veri bağlantıları hello önceki adımda karşıya.
* Merhaba Hive kullanarak bir sorguyu yürüten **istediğiniz hisse** tablo.

Ayrıca, hello örnek önce ve sonra ana işlemlerini gerçekleştirme temizleme yordamı gerçekleştirir. Merhaba temizleme sırasında tüm hello Azure Blob verileri ve klasörleri kaldırılır ve hello Hive tablosu bırakılan ilgili. Merhaba temizleme yordamı hello örnek komut satırından da çağırabilirsiniz.

Merhaba örnek hello aşağıdaki önkoşullar vardır:

* Etkin bir Microsoft Azure aboneliği ve abonelik kimliği
* Merhaba karşılık gelen özel anahtara sahip hello aboneliği için yönetim sertifikası. Merhaba sertifika hello geçerli kullanıcı özel depolama hello kullanılan makine toorun hello örnek üzerinde yüklü olmalıdır.
* Etkin bir Hdınsight kümesi.
* Bir Azure Storage hesabı toohello Hdınsight hello karşılık gelen birincil veya ikincil erişim anahtarı ile birlikte hello önceki önkoşul kümeden bağlı.

Merhaba örneği çalıştırmadan önce tüm hello bilgileri hello önkoşullardan girilen toohello örnek yapılandırma dosyası olmalıdır. İki olası yolları toodo vardır:

* Merhaba örnek kök dizininde Hello app.config dosyasını düzenleyin ve hello örnek oluşturma
* İlk hello örneği oluşturmak ve ardından AvroHDISample.exe.config hello yapı dizininde düzenleyin

Her iki durumda da, tüm düzenlemeleri hello yapılmalıdır  **<appSettings>**  ayarları bölümü. Merhaba dosya Hello açıklamaları izleyin.
Merhaba örnek hello komut satırından (burada hello .zip dosyası hello örnek ile ayıklanan toobe tooC:\AvroHDISample varsayılır; Aksi halde, kullanım ilgili hello varsa dosyasının yolu) komutu aşağıdaki hello yürüterek çalıştırılır:

    AvroHDISample run C:\AvroHDISample\Data

tooclean hello kümesi, hello aşağıdaki komutu çalıştırın:

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
