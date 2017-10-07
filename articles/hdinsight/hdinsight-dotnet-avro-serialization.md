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
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a><span data-ttu-id="b1673-104">Merhaba Microsoft Avro Library hadoop'ta verilerle serileştirme</span><span class="sxs-lookup"><span data-stu-id="b1673-104">Serialize data in Hadoop with hello Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="b1673-105">Merhaba Avro SDK artık Microsoft tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b1673-105">hello Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="b1673-106">Merhaba, açık kaynak topluluğu desteklenen kitaplığıdır.</span><span class="sxs-lookup"><span data-stu-id="b1673-106">hello library is open source community supported.</span></span> <span data-ttu-id="b1673-107">Merhaba kaynakları hello kitaplığı içinde bulunur [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="b1673-107">hello sources for hello library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="b1673-108">Bu konuda gösterilmektedir nasıl toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize nesneleri ve diğer veri yapıları akışları toopersist bunları toomemory, bir veritabanı veya dosya.</span><span class="sxs-lookup"><span data-stu-id="b1673-108">This topic shows how toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objects and other data structures into streams toopersist them toomemory, a database, or a file.</span></span> <span data-ttu-id="b1673-109">Ayrıca gösterir nasıl toodeserialize bunları toorecover hello orijinal nesneler.</span><span class="sxs-lookup"><span data-stu-id="b1673-109">It also shows how toodeserialize them toorecover hello original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="b1673-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="b1673-110">Apache Avro</span></span>
<span data-ttu-id="b1673-111">Merhaba <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> uygulayan hello hello Microsoft.NET ortamı için Apache Avro verileri seri hale getirme sistem.</span><span class="sxs-lookup"><span data-stu-id="b1673-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements hello Apache Avro data serialization system for hello Microsoft.NET environment.</span></span> <span data-ttu-id="b1673-112">Apache Avro sıkıştırılmış ikili veri değişim biçimi serileştirme için sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1673-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="b1673-113">Kullandığı <a href="http://www.json.org" target="_blank">JSON</a> toodefine dil birlikte çalışabilirliğini sağlayan bir dilden bağımsız şemasını.</span><span class="sxs-lookup"><span data-stu-id="b1673-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> toodefine a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="b1673-114">Tek bir dilde seri verilerini başka bir programda okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="b1673-115">Şu anda C, C++, C#, Java, PHP, Python ve Ruby desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b1673-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="b1673-116">Merhaba biçim hakkında ayrıntılı bilgi hello bulunabilir <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro belirtimi</a>.</span><span class="sxs-lookup"><span data-stu-id="b1673-116">Detailed information on hello format can be found in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="b1673-117">Merhaba Microsoft Avro Library hello uzaktan yordam çağrılarını (RPC) bu belirtiminin bir parçası desteklemez.</span><span class="sxs-lookup"><span data-stu-id="b1673-117">hello Microsoft Avro Library does not support hello remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="b1673-118">Merhaba Avro sistem bir nesneyi seri hale getirilmiş hello gösterimini iki bölümden oluşur: şema ve gerçek değer.</span><span class="sxs-lookup"><span data-stu-id="b1673-118">hello serialized representation of an object in hello Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="b1673-119">Merhaba Avro şemasının JSON ile seri hale getirilmiş hello veri hello dilden bağımsız veri modeli açıklar.</span><span class="sxs-lookup"><span data-stu-id="b1673-119">hello Avro schema describes hello language-independent data model of hello serialized data with JSON.</span></span> <span data-ttu-id="b1673-120">Veri ikili gösterimidir yan yana sunulur.</span><span class="sxs-lookup"><span data-stu-id="b1673-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="b1673-121">Merhaba ikili gösterimden ayrı Hello şemasına sahip seri hale getirme hızlı ve hello gösterimi küçük yapma hiçbir değer başına ek yüklerine karşılık ile yazılan her nesne toobe izin verir.</span><span class="sxs-lookup"><span data-stu-id="b1673-121">Having hello schema separate from hello binary representation permits each object toobe written with no per-value overheads, making serialization fast, and hello representation small.</span></span>

## <a name="hello-hadoop-scenario"></a><span data-ttu-id="b1673-122">Merhaba Hadoop senaryosu</span><span class="sxs-lookup"><span data-stu-id="b1673-122">hello Hadoop scenario</span></span>
<span data-ttu-id="b1673-123">Merhaba Apache Avro seri hale getirme biçimi, Azure Hdınsight hem de diğer Apache Hadoop ortamlarında yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b1673-123">hello Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="b1673-124">Avro uygun şekilde toorepresent Hadoop MapReduce işi karmaşık veri yapılarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1673-124">Avro provides a convenient way toorepresent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="b1673-125">Avro dosyalarının (Avro nesne kapsayıcısı dosyası) Hello biçimi tasarlanmış toosupport hello dağıtılmış MapReduce programlama modelini olmuştur.</span><span class="sxs-lookup"><span data-stu-id="b1673-125">hello format of Avro files (Avro object container file) has been designed toosupport hello distributed MapReduce programming model.</span></span> <span data-ttu-id="b1673-126">Merhaba dağıtımına olanak sağlayan hello anahtar hello dosyaların "bölünebilir" olması bir dosyada herhangi bir noktaya arama ve böylelikle belirli bir bloktan itibaren okumaya başlamanız hello herkese açık olmasını özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="b1673-126">hello key feature that enables hello distribution is that hello files are “splittable” in hello sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="b1673-127">Avro Kitaplığı'nda seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="b1673-127">Serialization in Avro Library</span></span>
<span data-ttu-id="b1673-128">Merhaba Avro için .NET kitaplığı biçimlendiricisi nesnelerinin iki yolla destekler:</span><span class="sxs-lookup"><span data-stu-id="b1673-128">hello .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="b1673-129">**Yansıma** -hello JSON şeması hello türleri için serileştirilmiş hello .NET türleri toobe sözleşme özniteliklerini hello verilerinden otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b1673-129">**reflection** - hello JSON schema for hello types is automatically built from hello data contract attributes of hello .NET types toobe serialized.</span></span>
* <span data-ttu-id="b1673-130">**Genel kayıt** -A JSON şeması hello tarafından temsil edilen bir kayıttaki belirtilen açıkça [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) hiçbir .NET türleri hello veri toobe için mevcut toodescribe hello şema olduğunda sınıfı seri hale getirilmiş.</span><span class="sxs-lookup"><span data-stu-id="b1673-130">**generic record** - A JSON schema is explicitly specified in a record represented by hello [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present toodescribe hello schema for hello data toobe serialized.</span></span>

<span data-ttu-id="b1673-131">Merhaba veri şeması tooboth hello yazıcı ve okuyucu hello akışın bilindiğinde hello veri olmadan, şema gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-131">When hello data schema is known tooboth hello writer and reader of hello stream, hello data can be sent without its schema.</span></span> <span data-ttu-id="b1673-132">Avro nesne kapsayıcısı dosyası kullanıldığında durumlarda hello şema hello dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="b1673-132">In cases when an Avro object container file is used, hello schema is stored within hello file.</span></span> <span data-ttu-id="b1673-133">Veri sıkıştırma için kullanılan hello codec gibi diğer parametrelerle belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-133">Other parameters, such as hello codec used for data compression, can be specified.</span></span> <span data-ttu-id="b1673-134">Bu senaryolar daha ayrıntılı olarak özetlenen ve kod örnekleri aşağıdaki hello gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b1673-134">These scenarios are outlined in more detail and illustrated in hello following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="b1673-135">Avro kitaplığını yükle</span><span class="sxs-lookup"><span data-stu-id="b1673-135">Install Avro Library</span></span>
<span data-ttu-id="b1673-136">Merhaba kitaplığı yüklemeden önce hello gerekli şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b1673-136">hello following are required before you install hello library:</span></span>

* <span data-ttu-id="b1673-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="b1673-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="b1673-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="b1673-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="b1673-139">Bu hello Newtonsoft.Json.dll bağımlılık hello Microsoft Avro Library hello yüklemesiyle otomatik olarak karşıdan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b1673-139">Note that hello Newtonsoft.Json.dll dependency is downloaded automatically with hello installation of hello Microsoft Avro Library.</span></span> <span data-ttu-id="b1673-140">Merhaba yordamı bölümden hello sağlanır:</span><span class="sxs-lookup"><span data-stu-id="b1673-140">hello procedure is provided in hello following section:</span></span>

<span data-ttu-id="b1673-141">Merhaba Microsoft Avro Library Visual Studio'dan aşağıdaki yordamı hello yüklenebilir bir NuGet paketi olarak dağıtılır:</span><span class="sxs-lookup"><span data-stu-id="b1673-141">hello Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via hello following procedure:</span></span>

1. <span data-ttu-id="b1673-142">Select hello **proje** sekmesi -> **NuGet paketlerini Yönet...**</span><span class="sxs-lookup"><span data-stu-id="b1673-142">Select hello **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="b1673-143">Merhaba, "Microsoft.Hadoop.Avro" için arama **arama çevrimiçi** kutusu.</span><span class="sxs-lookup"><span data-stu-id="b1673-143">Search for "Microsoft.Hadoop.Avro" in hello **Search Online** box.</span></span>
3. <span data-ttu-id="b1673-144">Merhaba tıklatın **yükleme** sonraki çok düğmesini**Microsoft Azure Hdınsight Avro Kitaplığı**.</span><span class="sxs-lookup"><span data-stu-id="b1673-144">Click hello **Install** button next too**Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="b1673-145">Bu hello Newtonsoft.Json.dll unutmayın (> 6.0.4 =) bağımlılık da karşıdan otomatik olarak Microsoft Avro Library hello ile.</span><span class="sxs-lookup"><span data-stu-id="b1673-145">Note that hello Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with hello Microsoft Avro Library.</span></span>

<span data-ttu-id="b1673-146">Merhaba Microsoft Avro Library kaynak kodunu şu adreste [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="b1673-146">hello Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="b1673-147">Avro kitaplığını kullanarak şemaları derleme</span><span class="sxs-lookup"><span data-stu-id="b1673-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="b1673-148">Merhaba Microsoft Avro Library, otomatik olarak hello üzerinde temel C# türleri oluşturma sağlayan yardımcı JSON şeması önceden tanımlanmış bir kod oluşturma içerir.</span><span class="sxs-lookup"><span data-stu-id="b1673-148">hello Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on hello previously defined JSON schema.</span></span> <span data-ttu-id="b1673-149">Başlangıç kodu oluşturma yardımcı programı bir ikili yürütülebilir dağıtılmaz ancak aşağıdaki yordamı hello kolayca oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="b1673-149">hello code generation utility is not distributed as a binary executable, but can be easily built via hello following procedure:</span></span>

1. <span data-ttu-id="b1673-150">Hdınsight SDK kaynak kodundan hello en son sürümü ile Merhaba .zip dosyasını indirdikten <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">için Microsoft .NET SDK Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="b1673-150">Download hello .zip file with hello latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="b1673-151">(Tıklatın hello **indirin** simgesi, değil hello **indirir** sekmesini.)</span><span class="sxs-lookup"><span data-stu-id="b1673-151">(Click hello **Download** icon, not hello **Downloads** tab.)</span></span>
2. <span data-ttu-id="b1673-152">.NET Framework 4 ile Merhaba makinede Hdınsight SDK tooa dizine yüklü ve gerekli bağımlılık NuGet paketlerini indirmek için toohello Internet bağlı hello ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="b1673-152">Extract hello HDInsight SDK tooa directory on hello machine with .NET Framework 4 installed and connected toohello Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="b1673-153">Aşağıda, hello kaynak kodu ayıklanan tooC:\SDK olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="b1673-153">Below, we assume that hello source code is extracted tooC:\SDK.</span></span>
3. <span data-ttu-id="b1673-154">C:\SDK\src\Microsoft.Hadoop.Avro.Tools toohello klasörüne gidin ve build.bat çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b1673-154">Go toohello folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="b1673-155">(Merhaba dosya MSBuild gelen çağrıları hello .NET Framework hello 32-bit dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="b1673-155">(hello file calls MSBuild from hello 32-bit distribution of hello .NET Framework.</span></span> <span data-ttu-id="b1673-156">Toouse hello 64-bit sürümü, düzenleme build.bat isterseniz aşağıdaki içinde hello dosya yorumlar hello.) Merhaba yapı başarılı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b1673-156">If you would like toouse hello 64-bit version, edit build.bat, following hello comments inside hello file.) Ensure that hello build is successful.</span></span> <span data-ttu-id="b1673-157">(Bazı sistemlerinde MSBuild uyarılar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="b1673-158">Derleme hataları var olduğu sürece bu uyarılar hello yardımcı programı etkilemez.)</span><span class="sxs-lookup"><span data-stu-id="b1673-158">These warnings do not affect hello utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="b1673-159">derlenmiş hello yardımcı programı C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="b1673-159">hello compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="b1673-160">tooget hello komut satırı sözdizimi ile tanıdık komutu hello kod oluşturma yardımcı programı bulunduğu hello klasöründen aşağıdaki hello yürütün:`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="b1673-160">tooget familiar with hello command-line syntax, execute hello following command from hello folder where hello code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="b1673-161">tootest hello yardımcı programı, dosyadan hello kaynak kodu ile sağlanan hello örnek JSON şeması C# sınıfları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1673-161">tootest hello utility, you can generate C# classes from hello sample JSON schema file provided with hello source code.</span></span> <span data-ttu-id="b1673-162">Merhaba aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="b1673-162">Execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="b1673-163">Bu tooproduce iki C# dosyalarını hello geçerli dizinde olması: SensorData.cs ve Location.cs.</span><span class="sxs-lookup"><span data-stu-id="b1673-163">This is supposed tooproduce two C# files in hello current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="b1673-164">Merhaba JSON şeması tooC # türleri, dönüştürülürken hello kod oluşturma yardımcı programını kullanarak toounderstand hello mantığı GenerationVerification.feature C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc içinde bulunan hello dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="b1673-164">toounderstand hello logic that hello code generation utility is using while converting hello JSON schema tooC# types, see hello file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="b1673-165">Ad alanları hello JSON şemadan hello önceki paragrafta bahsedilen hello dosyasında açıklanan hello mantığı kullanarak ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="b1673-165">Namespaces are extracted from hello JSON schema, using hello logic described in hello file mentioned in hello previous paragraph.</span></span> <span data-ttu-id="b1673-166">Ad alanları Hello şemadan ayıklanan ne olursa olsun hello yardımcı programı komut satırında hello /n parametresiyle sağlanan üzerinden önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="b1673-166">Namespaces extracted from hello schema take precedence over whatever is provided with hello /n parameter in hello utility command line.</span></span> <span data-ttu-id="b1673-167">Merhaba şema içinde yer alan toooverride hello ad alanları istiyorsanız hello /nf parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1673-167">If you want toooverride hello namespaces contained within hello schema, use hello /nf parameter.</span></span> <span data-ttu-id="b1673-168">Örneğin, toochange hello SampleJSONSchema.avsc toomy.own.nspace, tüm ad alanlarını yürütme hello komutu:</span><span class="sxs-lookup"><span data-stu-id="b1673-168">For example, toochange all namespaces from hello SampleJSONSchema.avsc toomy.own.nspace, execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a><span data-ttu-id="b1673-169">Merhaba örnekleri hakkında</span><span class="sxs-lookup"><span data-stu-id="b1673-169">About hello samples</span></span>
<span data-ttu-id="b1673-170">Bu konuda sağlanan altı örnekleri Microsoft Avro Library hello tarafından desteklenen farklı senaryolar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b1673-170">Six examples provided in this topic illustrate different scenarios supported by hello Microsoft Avro Library.</span></span> <span data-ttu-id="b1673-171">Merhaba Microsoft Avro Library akış ile tasarlanmış toowork ' dir.</span><span class="sxs-lookup"><span data-stu-id="b1673-171">hello Microsoft Avro Library is designed toowork with any stream.</span></span> <span data-ttu-id="b1673-172">Bu örneklerde, veri veya bellek akışları yerine dosya akışları için veritabanları Basitlik ve tutarlılık aracılığıyla yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="b1673-173">bir üretim ortamında gerçekleştirilecek hello yaklaşım hello tam senaryo gereksinimleri, veri kaynağı ve birim, performans ile ilgili kısıtlamalar ve diğer etkenlere bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b1673-173">hello approach taken in a production environment depends on hello exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="b1673-174">ilk iki örneklerde nasıl hello tooserialize ve yansıma ve genel kayıtları kullanarak veri akışı arabelleklerini seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="b1673-174">hello first two examples show how tooserialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="b1673-175">Merhaba bu iki durumlarda şema hello okuyucuları ve yazıcıları arasında paylaşılan toobe varsayılır bant dışı.</span><span class="sxs-lookup"><span data-stu-id="b1673-175">hello schema in these two cases is assumed toobe shared between hello readers and writers out-of-band.</span></span>

<span data-ttu-id="b1673-176">Merhaba üçüncü ve dördüncü örneklerde nasıl tooserialize ve hello Avro nesne kapsayıcısı dosyaları kullanarak veri serisi.</span><span class="sxs-lookup"><span data-stu-id="b1673-176">hello third and fourth examples show how tooserialize and deserialize data by using hello Avro object container files.</span></span> <span data-ttu-id="b1673-177">Veriler bir Avro kapsayıcı dosyasında depolanır, hello şema çıkarma için paylaşılan gerekir çünkü şemasına her zaman ile depolanır.</span><span class="sxs-lookup"><span data-stu-id="b1673-177">When data is stored in an Avro container file, its schema is always stored with it because hello schema must be shared for deserialization.</span></span>

<span data-ttu-id="b1673-178">Merhaba örnek içeren hello ilk dört örnekler hello indirilebilir <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure Kod örnekleri</a> site.</span><span class="sxs-lookup"><span data-stu-id="b1673-178">hello sample containing hello first four examples can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="b1673-179">Merhaba beşinci örnekteki nasıl toouse Avro için özel sıkıştırma codec nesne kapsayıcısı dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b1673-179">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="b1673-180">Bu örnek hello indirilebilir hello kodu içeren bir örnek <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure Kod örnekleri</a> site.</span><span class="sxs-lookup"><span data-stu-id="b1673-180">A sample containing hello code for this example can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="b1673-181">Merhaba altıncı örnek nasıl toouse Avro serileştirme tooupload veri tooAzure Blob depolamaya ve Hdınsight (Hadoop) kümesi ile Hive kullanarak Analiz göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="b1673-181">hello sixth sample shows how toouse Avro serialization tooupload data tooAzure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="b1673-182">Merhaba indirilebilir <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure Kod örnekleri</a> site.</span><span class="sxs-lookup"><span data-stu-id="b1673-182">It can be downloaded from hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="b1673-183">Merhaba konuda tartışılan toohello altı örnekleri bağlantılar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b1673-183">Here are links toohello six samples discussed in hello topic:</span></span>

* <span data-ttu-id="b1673-184"><a href="#Scenario1">**Yansıma ile seri hale getirme** </a> -hello JSON şeması türleri toobe seri için sözleşme öznitelikleri hello verilerinden otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b1673-184"><a href="#Scenario1">**Serialization with reflection**</a> - hello JSON schema for types toobe serialized is automatically built from hello data contract attributes.</span></span>
* <span data-ttu-id="b1673-185"><a href="#Scenario2">**Seri hale getirme Genel kaydıyla** </a> -.NET türü yansıma için kullanılabilir duruma geldiğinde hello JSON şeması bir kayıtta açıkça belirtilen.</span><span class="sxs-lookup"><span data-stu-id="b1673-185"><a href="#Scenario2">**Serialization with generic record**</a> - hello JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="b1673-186"><a href="#Scenario3">**Yansıma ile nesne kapsayıcısı dosyaları kullanarak serileştirme** </a> -hello JSON şeması otomatik olarak oluşturulur ve bir Avro nesne kapsayıcısı dosyası aracılığıyla serileştirilmiş hello verilerine birlikte paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="b1673-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - hello JSON schema is automatically built and shared together with hello serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="b1673-187"><a href="#Scenario4">**Genel kaydıyla nesne kapsayıcısı dosyaları kullanarak serileştirme** </a> -hello JSON şeması açıkça hello seri hale getirme önce belirtilen ve Avro nesne kapsayıcısı dosyası aracılığıyla hello verilerine birlikte paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="b1673-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - hello JSON schema is explicitly specified before hello serialization and shared together with hello data via an Avro object container file.</span></span>
* <span data-ttu-id="b1673-188"><a href="#Scenario5">**Özel sıkıştırma codec ile nesne kapsayıcısı dosyaları kullanarak serileştirme** </a> -hello örnek, nasıl toocreate bir Avro nesne kapsayıcı dosya hello Deflate veri sıkıştırma codec, özelleştirilmiş bir .NET uygulama gösterir.</span><span class="sxs-lookup"><span data-stu-id="b1673-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - hello example shows how toocreate an Avro object container file with a customized .NET implementation of hello Deflate data compression codec.</span></span>
* <span data-ttu-id="b1673-189"><a href="#Scenario6">**Microsoft Azure Hdınsight hizmeti hello için avro tooupload verileri kullanarak** </a> -hello örnekte, Avro serileştirme hello Hdınsight hizmeti ile nasıl etkileşim kurduğu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b1673-189"><a href="#Scenario6">**Using Avro tooupload data for hello Microsoft Azure HDInsight service**</a> - hello example illustrates how Avro serialization interacts with hello HDInsight service.</span></span> <span data-ttu-id="b1673-190">Bir etkin Azure aboneliği ve erişim tooan Azure Hdınsight küme toorun Bu örnek gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b1673-190">An active Azure subscription and access tooan Azure HDInsight cluster are required toorun this example.</span></span>

## <span data-ttu-id="b1673-191"><a name="Scenario1"></a>Örnek 1: Yansıma seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="b1673-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="b1673-192">Merhaba JSON şeması hello türleri için otomatik olarak serileştirilmiş hello C# nesnelerini toobe sözleşme özniteliklerini hello Microsoft Avro Library hello verilerden yansıma yoluyla tarafından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-192">hello JSON schema for hello types can be automatically built by hello Microsoft Avro Library via reflection from hello data contract attributes of hello C# objects toobe serialized.</span></span> <span data-ttu-id="b1673-193">Merhaba Microsoft Avro Library oluşturur bir [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) serileştirilmiş tooidentify hello alanları toobe.</span><span class="sxs-lookup"><span data-stu-id="b1673-193">hello Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello fields toobe serialized.</span></span>

<span data-ttu-id="b1673-194">Bu örnekte, nesneleri (bir **SensorData** üyesi sınıfıyla **konumu** yapısı) serileştirilmiş tooa bellek akışı olan ve bu akış sırayla seri.</span><span class="sxs-lookup"><span data-stu-id="b1673-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized tooa memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="b1673-195">Bu hello tooconfirm ilk karşılaştırılan toohello örnek sonra hello sonucudur **SensorData** kurtarılan aynı toohello özgün nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="b1673-195">hello result is then compared toohello initial instance tooconfirm that hello **SensorData** object recovered is identical toohello original.</span></span>

<span data-ttu-id="b1673-196">Bu örnekte Hello şema hello Avro nesne kapsayıcısı biçimi gerekli olmamasını sağlayacak şekilde hello okuyucuları ve yazıcıları, arasında paylaşılan toobe varsayılır.</span><span class="sxs-lookup"><span data-stu-id="b1673-196">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="b1673-197">Bir örnek için nasıl tooserialize ve verileri seri durumdan hello şema hello verilerle paylaşılan gerekir kullanarak yansıma hello nesne kapsayıcısı biçimi ile bellek arabelleği bkz <a href="#Scenario3">yansımailenesnekapsayıcısıdosyalarıkullanarakserihalegetirme</a>.</span><span class="sxs-lookup"><span data-stu-id="b1673-197">For an example of how tooserialize and deserialize data into memory buffers by using reflection with hello object container format when hello schema must be shared with hello data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

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


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="b1673-198">Örnek 2: Genel bir kayıtla seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="b1673-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="b1673-199">Veri sözleşmesi ile .NET sınıfları aracılığıyla Hello veri gösterilemez yansıma kullanılamaz bir JSON şeması açıkça bir genel kayıtta belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because hello data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="b1673-200">Bu yöntem, yansıma kullanmaktan daha yavaştır.</span><span class="sxs-lookup"><span data-stu-id="b1673-200">This method is slower than using reflection.</span></span> <span data-ttu-id="b1673-201">Böyle durumlarda, hello şeması hello veriler için de başka bir deyişle, derleme zamanında bilinmiyor dinamik olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-201">In such cases, hello schema for hello data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="b1673-202">Veri dönüştürülmüş kadar şema toohello Avro biçimi çalışma zamanında dinamik senaryo bu tür bir örneğidir bilinmiyor (CSV) dosyaları virgülle ayrılmış değerler olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed toohello Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="b1673-203">Bu örnekte gösterilir nasıl toocreate ve bir [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly belirtin JSON şeması nasıl toopopulate hello veri ve ardından nasıl ile tooserialize ve bu seri.</span><span class="sxs-lookup"><span data-stu-id="b1673-203">This example shows how toocreate and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specify a JSON schema, how toopopulate it with hello data, and then how tooserialize and deserialize it.</span></span> <span data-ttu-id="b1673-204">Merhaba sonuç sonra karşılaştırıldığında kurtarılan kayıt hello toohello ilk örnek tooconfirm aynı toohello özgün olduğunu.</span><span class="sxs-lookup"><span data-stu-id="b1673-204">hello result is then compared toohello initial instance tooconfirm that hello record recovered is identical toohello original.</span></span>

<span data-ttu-id="b1673-205">Bu örnekte Hello şema hello Avro nesne kapsayıcısı biçimi gerekli olmamasını sağlayacak şekilde hello okuyucuları ve yazıcıları, arasında paylaşılan toobe varsayılır.</span><span class="sxs-lookup"><span data-stu-id="b1673-205">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="b1673-206">Bir örnek için nasıl tooserialize ve verileri seri durumdan hello hello şema hello serileştirilmiş verilerle birlikte olması gerektiğinde kullanarak genel bir kayıt hello nesne kapsayıcısı biçimi ile bellek arabelleği bakın <a href="#Scenario4">nesne kapsayıcısı kullanarak seri hale getirme Genel kayıt dosyalarıyla</a> örnek.</span><span class="sxs-lookup"><span data-stu-id="b1673-206">For an example of how tooserialize and deserialize data into memory buffers by using a generic record with hello object container format when hello schema must be included with hello serialized data, see hello <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

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


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="b1673-207">Örnek 3: Serileştirme nesne kapsayıcısı dosyaları ve seri hale getirme yansıma ile kullanma</span><span class="sxs-lookup"><span data-stu-id="b1673-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="b1673-208">Bu örnekte hello benzer toohello senaryosunda, <a href="#Scenario1"> ilk örnek</a>burada hello şema yansıma ile örtük olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-208">This example is similar toohello scenario in hello <a href="#Scenario1"> first example</a>, where hello schema is implicitly specified with reflection.</span></span> <span data-ttu-id="b1673-209">Merhaba fark vardır hello şema, seri durumdan çıkarır toohello okuyucu bilinen toobe burada varsayılır değil.</span><span class="sxs-lookup"><span data-stu-id="b1673-209">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span> <span data-ttu-id="b1673-210">Merhaba **SensorData** serileştirilmiş nesneler toobe ve bunların örtük olarak belirtilen şema hello tarafından temsil edilen bir Avro nesne kapsayıcısı dosyasında depolanır [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) sınıf.</span><span class="sxs-lookup"><span data-stu-id="b1673-210">hello **SensorData** objects toobe serialized and their implicitly specified schema are stored in an Avro object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="b1673-211">Bu örnekte ile Merhaba veri serileştirilmiş [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) ve seri durumdan çıkarılmış ile [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1673-211">hello data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="b1673-212">Merhaba sonuç sonra karşılaştırılan toohello ilk örnekleri tooensure kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="b1673-212">hello result then is compared toohello initial instances tooensure identity.</span></span>

<span data-ttu-id="b1673-213">Merhaba hello verilerde kapsayıcı dosya hello varsayılan sıkıştırılmış nesne [ **Deflate** ] [ deflate-100] sıkıştırma codec .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="b1673-213">hello data in hello object container file is compressed via hello default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="b1673-214">Merhaba bkz <a href="#Scenario5"> beşinci örnek</a> bu konuda toolearn içinde nasıl toouse hello daha yeni ve üst bir sürümünü [ **Deflate** ] [ deflate-110] sıkıştırma codec .NET Framework 4. 5 ' kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-214">See hello <a href="#Scenario5"> fifth example</a> in this topic toolearn how toouse a more recent and superior version of hello [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

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


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="b1673-215">Örnek 4: nesne kapsayıcısı dosyaları ve seri hale getirme Genel kaydıyla kullanarak seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="b1673-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="b1673-216">Bu örnekte hello benzer toohello senaryosunda, <a href="#Scenario2"> ikinci örnek</a>burada hello şema JSON ile açıkça belirtilir.</span><span class="sxs-lookup"><span data-stu-id="b1673-216">This example is similar toohello scenario in hello <a href="#Scenario2"> second example</a>, where hello schema is explicitly specified with JSON.</span></span> <span data-ttu-id="b1673-217">Merhaba fark vardır hello şema, seri durumdan çıkarır toohello okuyucu bilinen toobe burada varsayılır değil.</span><span class="sxs-lookup"><span data-stu-id="b1673-217">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span>

<span data-ttu-id="b1673-218">Merhaba sınama veri kümesi bir liste halinde toplanan [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) nesneleri açıkça tanımlanmış bir JSON şeması ve hello tarafından temsil edilen bir nesne kapsayıcısı dosyasında depolanan [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b1673-218">hello test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="b1673-219">Bu kapsayıcı dosyayı sıkıştırılmamış, kullanılan tooserialize hello veri yazıcısı sonra tooa dosyasını kaydettiğiniz tooa bellek akışı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1673-219">This container file creates a writer that is used tooserialize hello data, uncompressed, tooa memory stream that is then saved tooa file.</span></span> <span data-ttu-id="b1673-220">Merhaba [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) hello okuyucusunu oluşturmak için kullanılan parametresi, bu verileri sıkıştırılmaz belirtir.</span><span class="sxs-lookup"><span data-stu-id="b1673-220">hello [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating hello reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="b1673-221">Merhaba veri sonra hello dosyadan okunan ve nesneleri koleksiyona seri.</span><span class="sxs-lookup"><span data-stu-id="b1673-221">hello data is then read from hello file and deserialized into a collection of objects.</span></span> <span data-ttu-id="b1673-222">Bu koleksiyon karşılaştırılan toohello ilk bunların özdeş olduğunu Avro kayıtları tooconfirm listesidir.</span><span class="sxs-lookup"><span data-stu-id="b1673-222">This collection is compared toohello initial list of Avro records tooconfirm that they are identical.</span></span>

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




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="b1673-223">Örnek 5: özel sıkıştırma codec ile nesne kapsayıcısı dosyaları kullanarak seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="b1673-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="b1673-224">Merhaba beşinci örnekteki nasıl toouse Avro için özel sıkıştırma codec nesne kapsayıcısı dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b1673-224">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="b1673-225">Bu örnek hello indirilebilir hello kodu içeren bir örnek [Azure Kod örnekleri](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span><span class="sxs-lookup"><span data-stu-id="b1673-225">A sample containing hello code for this example can be downloaded from hello [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="b1673-226">Merhaba [Avro belirtimi](http://avro.apache.org/docs/current/spec.html#Required+Codecs) bir isteğe bağlı sıkıştırma codec kullanımına izin verir (Ayrıca çok**Null** ve **Deflate** Varsayılanları).</span><span class="sxs-lookup"><span data-stu-id="b1673-226">hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition too**Null** and **Deflate** defaults).</span></span> <span data-ttu-id="b1673-227">Bu örnekte yeni codec Snappy gibi uygulama değil (Merhaba desteklenen isteğe bağlı codec olarak belirtilen [Avro belirtimi](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="b1673-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="b1673-228">Nasıl toouse hello hello .NET Framework 4.5 uygulaması gösterir [ **Deflate** ] [ deflate-110] helloüzerindegöredahaiyibirsıkıştırmaalgoritmasısağlayancodec[zlib](http://zlib.net/) hello varsayılan .NET Framework 4 sürümünden sıkıştırma kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="b1673-228">It shows how toouse hello .NET Framework 4.5 implementation of hello [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on hello [zlib](http://zlib.net/) compression library than hello default .NET Framework 4 version.</span></span>

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

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a><span data-ttu-id="b1673-229">Örnek 6: Merhaba Microsoft Azure Hdınsight hizmeti Avro tooupload verileri kullanma</span><span class="sxs-lookup"><span data-stu-id="b1673-229">Sample 6: Using Avro tooupload data for hello Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="b1673-230">Bazı programlama tekniklerinin ilgili toointeracting hello Azure Hdınsight hizmeti ile Merhaba altıncı örneği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b1673-230">hello sixth example illustrates some programming techniques related toointeracting with hello Azure HDInsight service.</span></span> <span data-ttu-id="b1673-231">Bu örnek hello indirilebilir hello kodu içeren bir örnek [Azure Kod örnekleri](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span><span class="sxs-lookup"><span data-stu-id="b1673-231">A sample containing hello code for this example can be downloaded from hello [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="b1673-232">Merhaba örnek görevleri hello:</span><span class="sxs-lookup"><span data-stu-id="b1673-232">hello sample does hello following tasks:</span></span>

* <span data-ttu-id="b1673-233">Tooan varolan Hdınsight hizmeti kümesine bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b1673-233">Connects tooan existing HDInsight service cluster.</span></span>
* <span data-ttu-id="b1673-234">Birkaç CSV dosyaları serileştirir ve hello sonuç tooAzure Blob depolama alanına yükler.</span><span class="sxs-lookup"><span data-stu-id="b1673-234">Serializes several CSV files and uploads hello result tooAzure Blob storage.</span></span> <span data-ttu-id="b1673-235">(Merhaba CSV dosyaları hello örnek ile birlikte dağıtılır ve AMEX stok geçmiş verileri tarafından dağıtılan bir ayıklama temsil [Infochimps](http://www.infochimps.com/) 1970'ten 2010 hello dönemin.</span><span class="sxs-lookup"><span data-stu-id="b1673-235">(hello CSV files are distributed together with hello sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for hello period 1970-2010.</span></span> <span data-ttu-id="b1673-236">Merhaba örnek CSV dosyası verilerini okur, dönüştürür hello Merhaba, kayıtları tooinstances **hisse senedi** sınıfı ve ardından yansıma kullanarak serileştirir.</span><span class="sxs-lookup"><span data-stu-id="b1673-236">hello sample reads CSV file data, converts hello records tooinstances of hello **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="b1673-237">Stok tür tanımı JSON şeması hello Microsoft Avro Library kod oluşturma yardımcı programı aracılığıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b1673-237">Stock type definition is created from a JSON schema via hello Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="b1673-238">Adlı yeni bir dış tablo oluşturur **istediğiniz hisse** , kovanında ve toohello veri bağlantıları hello önceki adımda karşıya.</span><span class="sxs-lookup"><span data-stu-id="b1673-238">Creates a new external table called **Stocks** in Hive, and links it toohello data uploaded in hello previous step.</span></span>
* <span data-ttu-id="b1673-239">Merhaba Hive kullanarak bir sorguyu yürüten **istediğiniz hisse** tablo.</span><span class="sxs-lookup"><span data-stu-id="b1673-239">Executes a query by using Hive over hello **Stocks** table.</span></span>

<span data-ttu-id="b1673-240">Ayrıca, hello örnek önce ve sonra ana işlemlerini gerçekleştirme temizleme yordamı gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="b1673-240">In addition, hello sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="b1673-241">Merhaba temizleme sırasında tüm hello Azure Blob verileri ve klasörleri kaldırılır ve hello Hive tablosu bırakılan ilgili.</span><span class="sxs-lookup"><span data-stu-id="b1673-241">During hello clean-up, all of hello related Azure Blob data and folders are removed, and hello Hive table is dropped.</span></span> <span data-ttu-id="b1673-242">Merhaba temizleme yordamı hello örnek komut satırından da çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1673-242">You can also invoke hello clean-up procedure from hello sample command line.</span></span>

<span data-ttu-id="b1673-243">Merhaba örnek hello aşağıdaki önkoşullar vardır:</span><span class="sxs-lookup"><span data-stu-id="b1673-243">hello sample has hello following prerequisites:</span></span>

* <span data-ttu-id="b1673-244">Etkin bir Microsoft Azure aboneliği ve abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="b1673-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="b1673-245">Merhaba karşılık gelen özel anahtara sahip hello aboneliği için yönetim sertifikası.</span><span class="sxs-lookup"><span data-stu-id="b1673-245">A management certificate for hello subscription with hello corresponding private key.</span></span> <span data-ttu-id="b1673-246">Merhaba sertifika hello geçerli kullanıcı özel depolama hello kullanılan makine toorun hello örnek üzerinde yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b1673-246">hello certificate should be installed in hello current user private storage on hello machine used toorun hello sample.</span></span>
* <span data-ttu-id="b1673-247">Etkin bir Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="b1673-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="b1673-248">Bir Azure Storage hesabı toohello Hdınsight hello karşılık gelen birincil veya ikincil erişim anahtarı ile birlikte hello önceki önkoşul kümeden bağlı.</span><span class="sxs-lookup"><span data-stu-id="b1673-248">An Azure Storage account linked toohello HDInsight cluster from hello previous prerequisite, together with hello corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="b1673-249">Merhaba örneği çalıştırmadan önce tüm hello bilgileri hello önkoşullardan girilen toohello örnek yapılandırma dosyası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b1673-249">All of hello information from hello prerequisites should be entered toohello sample configuration file before hello sample is run.</span></span> <span data-ttu-id="b1673-250">İki olası yolları toodo vardır:</span><span class="sxs-lookup"><span data-stu-id="b1673-250">There are two possible ways toodo it:</span></span>

* <span data-ttu-id="b1673-251">Merhaba örnek kök dizininde Hello app.config dosyasını düzenleyin ve hello örnek oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1673-251">Edit hello app.config file in hello sample root directory and then build hello sample</span></span>
* <span data-ttu-id="b1673-252">İlk hello örneği oluşturmak ve ardından AvroHDISample.exe.config hello yapı dizininde düzenleyin</span><span class="sxs-lookup"><span data-stu-id="b1673-252">First build hello sample, and then edit AvroHDISample.exe.config in hello build directory</span></span>

<span data-ttu-id="b1673-253">Her iki durumda da, tüm düzenlemeleri hello yapılmalıdır  **<appSettings>**  ayarları bölümü.</span><span class="sxs-lookup"><span data-stu-id="b1673-253">In both cases, all edits should be done in hello **<appSettings>** settings section.</span></span> <span data-ttu-id="b1673-254">Merhaba dosya Hello açıklamaları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b1673-254">Follow hello comments in hello file.</span></span>
<span data-ttu-id="b1673-255">Merhaba örnek hello komut satırından (burada hello .zip dosyası hello örnek ile ayıklanan toobe tooC:\AvroHDISample varsayılır; Aksi halde, kullanım ilgili hello varsa dosyasının yolu) komutu aşağıdaki hello yürüterek çalıştırılır:</span><span class="sxs-lookup"><span data-stu-id="b1673-255">hello sample is run from hello command line by executing hello following command (where hello .zip file with hello sample was assumed toobe extracted tooC:\AvroHDISample; if otherwise, use hello relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="b1673-256">tooclean hello kümesi, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b1673-256">tooclean up hello cluster, run hello following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
