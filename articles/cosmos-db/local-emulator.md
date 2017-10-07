---
title: "hello Azure Cosmos DB öykünücü ile yerel olarak aaaDevelop | Microsoft Docs"
description: "Hello Azure Cosmos DB öykünücüsü kullanarak, geliştirmek ve uygulamanızı yerel olarak ücretsiz, Azure aboneliği oluşturmadan test edin."
services: cosmos-db
documentationcenter: 
keywords: "Azure Cosmos DB öykünücüsü"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Hello Azure Cosmos DB öykünücüsü yerel geliştirme ve test amacıyla kullanın

<table>
<tr>
  <td><strong>İkili dosyalar</strong></td>
  <td>[MSI indirin](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Docker hub'a](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Docker kaynak</strong></td>
  <td>[Github](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
Hello Azure Cosmos DB öykünücüsü hello Azure Cosmos DB hizmeti Geliştirme amaçlı öykünen yerel bir ortam sağlar. Hello Azure Cosmos DB öykünücüsü kullanarak, geliştirmek ve bir Azure aboneliği oluşturmak veya herhangi bir maliyet olmadan uygulamanızı yerel olarak test etmek. Uygulamanızı hello Azure Cosmos DB öykünücüsü nasıl çalıştığını ile memnun kaldığınızda, toousing hello buluttaki bir Azure Cosmos DB hesabını geçiş yapabilirsiniz.

Bu makalede görevleri aşağıdaki hello yer almaktadır: 

> [!div class="checklist"]
> * Merhaba öykünücüsü yükleme
> * Merhaba öykünücüsü için Docker Windows üzerinde çalışan
> * Kimlik doğrulama istekleri
> * Merhaba öykünücüsü Hello Veri Gezgini kullanma
> * SSL sertifikaları verme
> * Merhaba öykünücüsü hello komut satırından çağırma
> * İzleme dosyaları toplama

Burada tooget hello Azure Cosmos DB öykünücü ile çalışmaya nasıl Kirill Gavrylyuk gösterir video, aşağıdaki hello izleyerek çalışmaya başlamanızı öneririz. Merhaba video toohello öykünücüsü DocumentDB öykünücüsü hello başvuruyor, ancak hello aracı kendisini yeniden adlandırıldı Not hello Azure Cosmos DB öykünücüsü hello video basmaya itibaren. Merhaba video tüm bilgileri hello Azure Cosmos DB öykünücüsü hala doğru olur. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>Merhaba öykünücüsü nasıl çalışır?
Hello Azure Cosmos DB öykünücüsü hello Azure Cosmos DB hizmeti, yüksek doğruluk öykünme sağlar. Azure Cosmos JSON belgelerini sorgulamak için destek dahil olmak üzere sağlama DB olarak aynı işlevselliği destekler ve koleksiyonları ölçekleme ve yürütme yordamları ve Tetikleyicileri depolanır. Geliştirme ve hello Azure Cosmos DB öykünücüsü kullanarak uygulamaları test etme ve bunları yalnızca tek bir yapılandırma için Azure Cosmos DB toohello bağlantı uç noktasının değişikliği yaparak küresel ölçekli tooAzure dağıtabilirsiniz.

Yüksek kaliteli yerel öykünme hello gerçek Azure Cosmos DB hizmetinin oluşturduğumuz olsa da, hello hello Azure Cosmos DB öykünücüsü hello hizmeti farklı uygulamasıdır. Örneğin, hello Azure Cosmos DB öykünücüsü hello yerel dosya sistemi gibi standart işletim sistemi bileşenlerini kalıcılığını ve HTTPS protokol yığını bağlantısı için kullanır. Bu genel çoğaltma, okuma/yazma ve ince ayarlanabilir tutarlılık düzeyleri için tek basamaklı milisaniyelik gecikme süresi yok gibi hello Azure Cosmos DB öykünücüsü kullanılabilir Azure altyapı dayanan bazı işlevler anlamına gelir.

> [!NOTE]
> Merhaba bu zaman hello Veri Gezgini adresindeki öykünücüsü yalnızca DocumentDB API koleksiyonları ve MongoDB koleksiyonları hello oluşturmayı destekler. Merhaba öykünücüsü Hello Veri Gezgini hello oluşturulmasını tablolar ve grafikler şu anda desteklemiyor. 

## <a name="system-requirements"></a>Sistem gereksinimleri
Hello Azure Cosmos DB öykünücüsü hello donanım ve yazılım gereksinimlerine sahiptir:

* Yazılım gereksinimleri
  * Windows Server 2012 R2, Windows Server 2016 veya Windows 10
*   En düşük donanım gereksinimleri
  * 2 GB RAM
  * 10 GB kullanılabilir sabit disk alanı

## <a name="installation"></a>Yükleme
İndirip hello Azure Cosmos DB öykünücüsü hello yükleyin [Microsoft Download Center](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> tooinstall, yapılandırma ve hello Azure Cosmos DB öykünücüsü çalıştırma, hello bilgisayar üzerinde yönetici ayrıcalıklarına sahip olmalıdır.

## <a name="running-on-docker-for-windows"></a>Windows için Docker çalışan

Windows için Docker Hello Azure Cosmos DB öykünücüsü çalıştırabilirsiniz. Merhaba öykünücüsü, Oracle Linux için Docker üzerinde çalışmaz.

Bulduktan sonra [Windows için Docker](https://www.docker.com/docker-windows) yüklü, hello öykünücü görüntünüzün Docker hub'dan sık kullanılan kabuğundan komutu aşağıdaki hello çalıştırarak çekebilir (cmd.exe, PowerShell, vs.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
toostart hello resim, hello aşağıdaki komutları çalıştırın.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

Merhaba yanıt benzer toohello aşağıdaki gibidir:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Öykünücü başlatıldı hello sonra kapatma hello öykünücüsü'nın kapsayıcı hello etkileşimli Kabuk kapatılıyor.

Hello uç noktası ve ana anahtarından içinde hello yanıt, istemci kullanın ve ana bilgisayara hello SSL sertifikasını içeri aktarın. tooimport hello SSL sertifikası hello bir yönetici komut isteminden aşağıdaki:

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>Başlangıç hello öykünücüsü

toostart hello Azure Cosmos DB öykünücüsü hello Başlat düğmesine basın veya hello Windows tuşuna basın. Yazmaya başlayın **Azure Cosmos DB öykünücüsü**ve uygulamaları hello listesinden seçim hello öykünücüsü. 

![Hello Başlat düğmesine veya tuşuna hello Windows anahtarını seçin, yazmaya başlayın ** Azure Cosmos DB öykünücüsü ** ve uygulamaları hello listesinden seçim hello öykünücüsü](./media/local-emulator/database-local-emulator-start.png)

Merhaba öykünücüsü çalıştırırken hello Windows görev çubuğundaki bildirim alanında bir simge görürsünüz. ![Azure Cosmos DB yerel öykünücüsü görev çubuğu bildirim](./media/local-emulator/database-local-emulator-taskbar.png)

Varsayılan olarak Azure Cosmos DB öykünücüsü Hello 8081 numaralı bağlantı noktasını dinlemeye hello yerel makine ("localhost") çalışır.

Hello Azure Cosmos DB öykünücüsü tarafından varsayılan toohello yüklü `C:\Program Files\Azure Cosmos DB Emulator` dizin. Ayrıca, başlatma ve durdurma hello komut satırı hello öykünücüsünden. Bkz: [komut satırı aracını referans](#command-line) daha fazla bilgi için.

## <a name="start-data-explorer"></a>Veri Gezgini'ni başlatın

Hello Azure Cosmos DB öykünücüsü başlattığında, hello Azure Cosmos DB Data Explorer tarayıcınızda otomatik olarak açılır. Başlangıç adresi olarak görünür [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Hello explorer kapatıp toore açık ister misiniz varsa, daha sonra hello URL tarayıcınızda açın ya da aşağıda gösterildiği gibi hello Windows Tepsi simgesi hello Azure Cosmos DB öykünücüsü'nden başlatın.

![Azure Cosmos DB yerel öykünücüsü Veri Gezgini Başlatıcısı](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Güncelleştirmeleri denetleme
Veri Gezgini indirme için kullanılabilir yeni bir güncelleştirme olup olmadığını gösterir. 

> [!NOTE]
> Hello Azure Cosmos DB öykünücüsü bir sürümünde oluşturulan veri toobe erişilebilir farklı bir sürümünü kullanırken garanti edilmez. Hello uzun süreli verilerinizi toopersist gerekiyorsa, bu verileri Azure Cosmos DB hesabı yerine hello Azure Cosmos DB öykünücüsü depolamanız önerilir. 

## <a name="authenticating-requests"></a>Kimlik doğrulama istekleri
Gibi hello bulutta Azure Cosmos DB ile Azure Cosmos DB öykünücüsü hello karşı yaptığınız her isteğin kimliğinin doğrulanması gerekir. Hello Azure Cosmos DB öykünücüsü ana anahtar kimlik doğrulaması için tek bir sabit hesap ve bilinen bir kimlik doğrulama anahtarı destekler. Bu hesabı ve anahtarı hello Azure Cosmos DB öykünücü ile kullanmak için izin verilen hello yalnızca kimlik bilgileridir. Bunlar:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> Merhaba ana hello Azure Cosmos DB öykünücüsü tarafından desteklenen anahtar yalnızca hello öykünücü ile kullanılmak üzere tasarlanmıştır. Üretim Azure Cosmos DB hesabı ve anahtarı hello Azure Cosmos DB öykünücü ile kullanamazsınız. 

> [!NOTE] 
> Merhaba /Key seçeneği ile Merhaba öykünücüsü başlattıysanız yerine hello oluşturulan anahtarı kullanın "C2y6yDjf5/R, ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="

Ayrıca, yalnızca hello Azure Cosmos DB hizmeti, hello Azure Cosmos DB öykünücüsü yalnızca desteklediği SSL üzerinden iletişimi güvenli hale getirin.

## <a name="running-hello-emulator-on-a-local-network"></a>Yerel bir ağda Hello öykünücüsünün çalışır

Yerel bir ağda hello öykünücüsü çalıştırabilirsiniz. tooenable ağ erişimi, hello /AllowNetworkAccess hello tasarrufunda belirtin [komut satırı](#command-line-syntax), gerektiren /Key belirttiğiniz = key_string veya/keyfile dosya_adı =. /GenKeyFile kullanabileceğiniz dosya_adı toogenerate bir dosya önceden rastgele bir anahtar ile =.  Bu çok/KeyFile geçirebilirsiniz sonra dosya_adı veya /Key = contents_of_file =.

tooenable ağ erişimi hello ilk hello kullanıcı için kapatma hello öykünücüsü gerekir ve hello öykünücüsü'nın veri dizini (C:\Users\user_name\AppData\Local\CosmosDBEmulator) silin.

## <a name="developing-with-hello-emulator"></a>Merhaba öykünücü ile geliştirme
Masaüstünde çalışan Azure Cosmos DB öykünücüsü sahip hello sonra herhangi bir desteklenen kullanabilirsiniz [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) veya hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract hello öykünücü ile. Hello Azure Cosmos DB öykünücüsü de hello DocumentDB ve MongoDB API'ları ve görünüm için koleksiyonları oluşturun ve herhangi bir kod yazmak zorunda kalmadan belgeleri düzenlemesine olanak sağlayan yerleşik bir Veri Gezgini içerir.   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Kullanıyorsanız, [MongoDB için protokol desteği Azure Cosmos DB](mongodb-introduction.md), Lütfen bağlantı dizesini izleyen hello kullanın:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

Var olan araçlarla kullanabilirsiniz [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB öykünücüsü. Ayrıca hello Azure Cosmos DB öykünücüsü ve hello kullanarak hello Azure Cosmos DB hizmeti arasında verileri geçirebilirsiniz [Azure Cosmos DB veri geçiş aracı](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Merhaba /Key seçeneği ile Merhaba öykünücüsü başlattıysanız yerine hello oluşturulan anahtarı kullanın "C2y6yDjf5/R, ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="

Hello Azure Cosmos DB öykünücüsü, varsayılan olarak kullanarak, too25 tek bölüm koleksiyonları veya 1 bölümlenmiş koleksiyon oluşturabilirsiniz. Bu değer değiştirme hakkında daha fazla bilgi için bkz: [ayar hello PartitionCount değeri](#set-partitioncount).

## <a name="export-hello-ssl-certificate"></a>Merhaba SSL sertifikasını dışarı aktarma

.NET dilleri ile çalışma zamanı kullanmak hello Windows sertifika deposunda toosecurely toohello Azure Cosmos DB yerel öykünücüsü bağlayın. Diğer diller yönetme ve sertifikaları kullanarak kendi yöntemi vardır. Java kullanan kendi [sertifika deposu](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) Python kullanırken [yuva sarmalayıcıları](https://docs.python.org/2/library/ssl.html).

Sipariş tooobtain sertifika toouse diller ve Windows sertifika deposunda hello ile entegre değil çalışma zamanları ile Merhaba Windows Sertifika Yöneticisi'ni kullanarak tooexport gerekir. Başlatılsın certlm.msc çalıştırarak ya da hello adım adım yönergeleri izleyin [hello Azure Cosmos DB öykünücüsü sertifikaları verin](./local-emulator-export-ssl-certificates.md). Merhaba Sertifika Yöneticisi'ni çalışır duruma geldiğinde BASE-64 kodlanmış X.509 (.cer) dosyası olarak açık hello kişisel aşağıda gösterildiği gibi sertifikaları ve dışarı aktarma hello kolay adı "DocumentDBEmulatorCertificate" sertifikasıyla hello.

![Azure Cosmos DB yerel öykünücüsü SSL sertifikası](./media/local-emulator/database-local-emulator-ssl_certificate.png)

Merhaba X.509 sertifikası alınabilir hello Java sertifika deposuna hello yönergeleri takip ederek [sertifika toohello Java CA deposuna sertifika ekleme](https://docs.microsoft.com/azure/java-add-certificate-ca-store). Merhaba sertifika hello sertifika deposuna içeri aktarıldığında, Java ve MongoDB uygulamalar mümkün tooconnect toohello Azure Cosmos DB öykünücüsü olur.

Toohello öykünücüsü Python ve Node.js SDK'ları bağlanırken SSL doğrulama devre dışı bırakılır.

## <a id="command-line"></a>Komut satırı aracı başvurusu
Hello yükleme konumundan hello komut satırı toostart kullanın ve hello öykünücüsü durdurmak, seçeneklerini yapılandırmak ve diğer işlemleri gerçekleştirebilir.

### <a name="command-line-syntax"></a>Komut satırı sözdizimi

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

Seçenekler, türü tooview hello listesinde `CosmosDB.Emulator.exe /?` hello komut isteminde.

<table>
<tr>
  <td><strong>Seçeneği</strong></td>
  <td><strong>Açıklama</strong></td>
  <td><strong>Komutu</strong></td>
  <td><strong>Bağımsız değişkenler</strong></td>
</tr>
<tr>
  <td>[Bağımsız değişkenler]</td>
  <td>Hello Azure Cosmos DB öykünücüsü varsayılan ayarlarla başlatır.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Help]</td>
  <td>Merhaba listesini görüntüler komut satırı bağımsız değişkenleri desteklenir.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>kapatma</td>
  <td>Hello Azure Cosmos DB öykünücüsü kapatır.</td>
  <td>CosmosDB.Emulator.exe Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>DataPath</td>
  <td>Hangi toostore veri dosyalarında Hello yolunu belirtir. % LocalAppdata%\CosmosDBEmulator varsayılandır.</td>
  <td>CosmosDB.Emulator.exe /DataPath =&lt;datapath&gt;</td>
  <td>&lt;DataPath&gt;: erişilebilir yolu</td>
</tr>
<tr>
  <td>Bağlantı noktası</td>
  <td>Başlangıç bağlantı noktası numarası toouse hello öykünücüsü belirtir.  8081 varsayılandır.</td>
  <td>CosmosDB.Emulator.exe Port =&lt;bağlantı noktası&gt;</td>
  <td>&lt;bağlantı noktası&gt;: tek bir bağlantı noktası numarası</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>API MongoDB uyumluluk için başlangıç bağlantı noktası numarası toouse belirtir. Varsayılandır 10255 değerini bulur.</td>
  <td>CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;: tek bir bağlantı noktası numarası</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Doğrudan bağlantı için bağlantı noktalarını toouse Hello belirtir. Varsayılan 10251,10252,10253,10254 olur.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: 4 bağlantı noktalarının virgülle ayrılmış listesi</td>
</tr>
<tr>
  <td>Anahtar</td>
  <td>Merhaba öykünücüsü için yetkilendirme anahtar. Anahtar hello bir 64 baytlık vektör 64 tabanlı kodlama olmalıdır.</td>
  <td>CosmosDB.Emulator.exe /Key:&lt;anahtarı&gt;</td>
  <td>&lt;anahtar&gt;: anahtarı bir 64 baytlık vektör base-64 hello kodlaması olması gerekir</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>Davranış sınırlama istek hızı etkinleştirilip etkinleştirilmeyeceğini belirtir.</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>Davranış sınırlama istek hızı devre dışı belirtir.</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>Nouı</td>
  <td>Merhaba öykünücüsü kullanıcı arabirimi gösterme.</td>
  <td>CosmosDB.Emulator.exe/nouı</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>Belge Gezgini başlatma sırasında gösterme.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>bölüm sayısı</td>
  <td>Bölümlenmiş koleksiyonlar Hello sayısını belirtir. Bkz: [değiştirme koleksiyonları hello sayısı](#set-partitioncount) daha fazla bilgi için.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount =&lt;bölüm sayısı&gt;</td>
  <td>&lt;bölüm sayısı&gt;: maksimum sayısı, izin verilen tek bölüm koleksiyonları. Varsayılan 25'tir. İzin verilen en fazla 250'dir.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Merhaba varsayılan bölümlendirilmiş bir koleksiyon için bölüm sayısını belirtir.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; 25 varsayılandır.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Etkinleştirir toohello öykünücüsü bir ağ üzerinden erişir. /Key geçmesi gereken =&lt;key_string&gt; veya/keyfile =&lt;dosya_adı&gt; tooenable ağ erişimi.</td>
  <td>CosmosDB.Emulator.exe AllowNetworkAccess /Key =&lt;key_string&gt;<br><br>or<br><br>CosmosDB.Emulator.exe /AllowNetworkAccess/keyfile =&lt;dosya_adı&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>/AllowNetworkAccess kullanıldığında, güvenlik duvarı kurallarını ayarlama.</td>
  <td>CosmosDB.Emulator.exe /NoFirewall</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>Yeni bir yetkilendirme anahtar oluşturmak ve toohello belirtilen dosyayı kaydedin. oluşturulan başlangıç anahtarı hello /Key veya/keyfile seçenekleriyle kullanılabilir.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;yol tookey dosyası&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Tutarlılık</td>
  <td>Merhaba varsayılan tutarlılık düzeyi hello hesabı ayarlayın.</td>
  <td>CosmosDB.Emulator.exe /Consistency =&lt;tutarlılık&gt;</td>
  <td>&lt;Tutarlılık&gt;: değer hello aşağıdakilerden biri olması gerekir [tutarlılık düzeylerini](consistency-levels.md): oturum, güçlü, Eventual veya BoundedStaleness.  Oturum Hello varsayılan değerdir.</td>
</tr>
<tr>
  <td>?</td>
  <td>Merhaba Yardım iletisi göster.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Hello Azure Cosmos DB öykünücüsü ve Azure Cosmos DB arasındaki farklar 
Hello Azure Cosmos DB öykünücüsü yerel geliştirici istasyonunda çalıştıran benzetilmiş bir ortam sağladığından, bazı arasındaki işlevsel farklılıklar hello öykünücüsü ve bir Azure Cosmos DB hesap hello bulutta vardır:

* yalnızca tek bir sabit hesap ve bilinen bir ana anahtar Hello Azure Cosmos DB öykünücüsü destekler.  Anahtarını yeniden üretme hello Azure Cosmos DB öykünücüsü mümkün değildir.
* Hello Azure Cosmos DB öykünücüsü ölçeklenebilir hizmet değil ve çok sayıda koleksiyonları desteklemez.
* Hello Azure Cosmos DB öykünücüsü farklı benzetimini değil [Azure Cosmos DB tutarlılık düzeylerini](consistency-levels.md).
* Hello Azure Cosmos DB öykünücüsü benzetimi yapılamadı [bölgeli çoğaltma](distribute-data-globally.md).
* Hello Azure Cosmos DB öykünücüsü hello Azure Cosmos DB hizmetinde (örneğin belge boyutu sınırları, artan bölümlenmiş koleksiyonu depolama alanı) bulunan hello hizmeti kota geçersiz kılmaları desteklemez.
* Hello Azure Cosmos DB öykünücüsü kopyanızı hello Azure Cosmos DB hizmeti ile Merhaba en son değişikliklerle toodate yukarı olmayabilir gibi lütfen [Azure Cosmos DB kapasite Planlayıcısı](https://www.documentdb.com/capacityplanner) tooaccurately tahmin üretim verimlilik (RUs) uygulamanız gerekir.

## <a id="set-partitioncount"></a>Koleksiyonları Hello sayısını değiştirme

Varsayılan olarak, too25 tek bölüm koleksiyonları veya hello Azure Cosmos DB öykünücüsü kullanarak 1 bölümlenmiş koleksiyonunu oluşturabilirsiniz. Merhaba değiştirerek **PartitionCount** değeri too250 tek bölüm koleksiyonları veya 10 bölümlenmiş koleksiyonlar oluşturabilir ya da herhangi bir bileşimini hello 250 tek aşmayan iki bölümleri (burada 1 bölümlenmiş Koleksiyon 25 tek bölümlü bir koleksiyon =).

Merhaba geçerli bölüm sayısı aşıldı sonra toocreate koleksiyonu çalışırsanız hello öykünücüsü iletiden hello ile bir ServiceUnavailable özel durum oluşturur.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

koleksiyonları kullanılabilir toohello Azure Cosmos DB öykünücüsü toochange hello sayısı hello aşağıdaki:

1. Merhaba sağ tıklayarak tüm yerel Azure Cosmos DB öykünücüsü verilerini silmek **Azure Cosmos DB öykünücüsü** hello sistem tepsisi ve ardından simgesine **veri Sıfırla...** .
2. Bu klasörde C:\Users\user_name\AppData\Local\CosmosDBEmulator tüm öykünücüsü verileri silin.
3. Tüm açık örnekleri hello sağ tıklayarak çıkmak **Azure Cosmos DB öykünücüsü** hello sistem tepsisi ve ardından simgesine **çıkış**. Tüm örnekleri tooexit bir dakika sürebilir.
4. Merhaba Hello en son sürümünü yüklemek [Azure Cosmos DB öykünücüsü](https://aka.ms/cosmosdb-emulator).
5. Bir değer ayarlanarak Hello öykünücü hello PartitionCount bayrağı ile başlatın < 250 =. Örneğin: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Sorun giderme

Toohelp hello Azure Cosmos DB öykünücü ile karşılaştığınız sorunları sorun giderme ipuçları aşağıdaki hello kullan:

- Merhaba öykünücüsü yeni bir sürümünü yüklediyseniz ve hataları yaşıyor verilerinizi sıfırlama emin olun. Verilerinizi hello sistem tepsisi hello Azure Cosmos DB öykünücü simgesine sağ tıklayıp sıfırlama verileri tıklatarak sıfırlayabilirsiniz... Merhaba hataları çözmezse kaldırın ve hello uygulamayı yeniden yükleyin. Bkz: [hello yerel öykünücüsü kaldırma](#uninstall) yönergeler için.

- Hello Azure Cosmos DB öykünücüsü çökerse c:\Users\user_name\AppData\Local\CrashDumps klasöründen döküm dosyaları toplamak, sıkıştırmak ve bunları tooan e-postaya çok eklemek[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Kilitlenme karşılaşırsanız, komutu bir yönetici komut isteminden aşağıdaki hello CosmosDB.StartupEntryPoint.exe içinde çalıştırın:`lodctr /R` 

- Bir bağlantı sorunu yaşarsanız [toplamak izleme dosyaları](#trace-files)sıkıştırmak ve bunları tooan e-postaya çok eklemek[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Alırsanız, bir **Hizmet kullanılamıyor** iletisi, hello öykünücüsü tooinitialize hello ağ yığınını başarısız olabilir. Ağ filtre sürücülerini hello sorunu neden olabileceğinden hello Pulse güvenli istemci veya Juniper ağları istemcisi yüklü varsa toosee denetleyin. Kaldırma işlemi üçüncü taraf ağ filtre sürücüleri genellikle hello sorunu giderir.

### <a id="trace-files"></a>İzleme dosyaları Topla

toocollect hata ayıklama izlemeleri, komutları bir yönetici komut isteminden aşağıdaki hello çalıştırın:

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Gözcü hello sistem tepsisi toomake emin hello program kapatıldı, bir dakika sürebilir. Aynı zamanda yalnızca tıklatabilirsiniz **çıkış** hello Azure Cosmos DB öykünücüsü kullanıcı arabiriminde.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Merhaba sorunu yeniden oluşturun. Veri Gezgini çalışmıyorsa, yalnızca toowait hello tarayıcı tooopen birkaç saniye toocatch hello hata için gerekir.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Çok gidin`%ProgramFiles%\Azure Cosmos DB Emulator` ve hello docdbemulator_000001.etl dosyasını bulun.
7. Merhaba .etl dosyası yeniden oluşturma adımları birlikte çok gönderme[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) hata ayıklama için.

### <a id="uninstall"></a>Kaldırma yerel öykünücüsü hello

1. Tüm açık örnekleri hello çıkmak hello sistem tepsisi hello Azure Cosmos DB öykünücü simgesine sağ tıklayarak ve sonra da çıkış'ı tıklatarak yerel öykünücüsü. Tüm örnekleri tooexit bir dakika sürebilir.
2. Merhaba Windows Arama kutusuna yazın **uygulamalar ve Özellikler** üzerinde hello tıklatıp **uygulamalar ve Özellikler (sistem ayarlarını)** sonucu.
3. Uygulamaları Hello listesinde çok kaydırma**Azure Cosmos DB öykünücüsü**, onu seçin, **kaldırma**, ardından onaylayın ve tıklatın **kaldırma** yeniden.
4. Merhaba uygulama kaldırıldığında tooC:\Users gidin\<kullanıcı > \AppData\Local\CosmosDBEmulator ve delete hello klasör. 

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Yüklü yerel öykünücüsü hello
> * Rand öykünücüsü Docker için Windows hello
> * Kimliği doğrulanmış istekler
> * Merhaba öykünücüsü Hello Veri Gezgini kullanılan
> * Dışarı aktarılan SSL sertifikaları
> * Merhaba öykünücüsü hello komut satırından çağrılan
> * Toplanan izleme dosyaları

Bu öğreticide, nasıl toouse hello boş yerel geliştirme için yerel öykünücüsü öğrendiniz. Şimdi toohello sonraki öğretici devam ve öğrenin nasıl tooexport öykünücüsü SSL sertifikaları. 

> [!div class="nextstepaction"]
> [Hello Azure Cosmos DB öykünücüsü sertifikaları verme](local-emulator-export-ssl-certificates.md)
