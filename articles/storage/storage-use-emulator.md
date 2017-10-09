---
title: "geliştirme ve test için aaaUse hello Azure depolama öykünücüsü | Microsoft Docs"
description: "Hello Azure storage öykünücüsü geliştirmek ve Azure Storage uygulamalarınızı test etme için boş yerel geliştirme ortamı sağlar. İstekler, nasıl kimlik doğrulamalarının nasıl yapılacağını öğrenin tooconnect toohello öykünücüsünden uygulamanız ve nasıl toouse hello komut satırı aracı."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: f480b059-df8a-4a63-b05a-7f2f5d1f5c2a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: marsma
ms.openlocfilehash: 42637dcd9f476069e6ecd19ed04e7ed93fe38ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-storage-emulator-for-development-and-testing"></a>Geliştirme ve test amacıyla Hello Azure storage öykünücüsünü kullanma

Merhaba Microsoft Azure storage öykünücüsü hello Azure Blob, kuyruk ve Tablo Hizmetleri Geliştirme amaçlı öykünen yerel bir ortam sağlar. Merhaba storage öykünücüsü kullanarak, bir Azure aboneliği oluşturmak veya herhangi bir maliyet olmadan uygulamanızı yerel olarak hello depolama hizmetleri karşı sınayabilirsiniz. Uygulamanızı hello öykünücüsünde nasıl çalıştığını ile memnun kaldığınızda, toousing hello buluttaki bir Azure depolama hesabını geçiş yapabilirsiniz.

## <a name="get-hello-storage-emulator"></a>Merhaba depolama öykünücüsü Al
Merhaba depolama öykünücüsü kullanılabilir hello bir parçası olarak [Microsoft Azure SDK'sı](https://azure.microsoft.com/downloads/). Merhaba depolama öykünücüsü hello kullanarak da yükleyebilirsiniz [tek başına yükleyici](https://go.microsoft.com/fwlink/?linkid=717179&clcid=0x409) (doğrudan indirme). tooinstall hello depolama öykünücüsü, bilgisayarınızda yönetici ayrıcalıklarına sahip olmalıdır.

Merhaba depolama öykünücüsü şu anda yalnızca Windows üzerinde çalışır. Olanlar için Linux için depolama öykünücüsü dikkate alarak, bir seçenek tutulan, açık kaynaklı depolama öykünücüsü hello topluluktur [Azurite](https://github.com/arafato/azurite).

> [!NOTE]
> Merhaba depolama öykünücüsü bir sürümünde oluşturulan veri toobe erişilebilir farklı bir sürümünü kullanırken garanti edilmez. Merhaba uzun süreli verilerinizi toopersist gerekiyorsa, bu verileri Azure depolama hesabı yerine hello depolama öykünücüsü depolamak önerilir.
> <p/>
> Merhaba depolama öykünücüsü hello OData kitaplıklarının belirli sürümlerini bağlıdır. Merhaba OData diğer sürümleriyle hello depolama öykünücüsü tarafından kullanılan DLL'leri değiştirme desteklenmez ve beklenmeyen davranışlara neden olabilir. Ancak, OData hello depolama hizmeti tarafından desteklenen herhangi bir sürümünü kullanılan toosend istekleri toohello öykünücüsü olabilir.
>

## <a name="how-hello-storage-emulator-works"></a>Merhaba depolama öykünücüsü nasıl çalışır?
yerel bir Microsoft SQL Server örneğini ve hello yerel dosya sistemi tooemulate Azure storage Hizmetleri Hello depolama öykünücüsü kullanır. Varsayılan olarak, Microsoft SQL Server 2012 Express LocalDB içinde bir veritabanı hello depolama öykünücüsü kullanır. Yerel bir SQL Server örneğini hello LocalDB örnek yerine tooconfigure hello depolama öykünücüsü tooaccess seçebilirsiniz. Merhaba daha fazla bilgi için bkz [başlangıç ve başlatma hello depolama öykünücüsü](#start-and-initialize-the-storage-emulator) bu makalenin sonraki bölümlerinde bölümü.

Merhaba depolama öykünücüsü tooSQL sunucu veya yerel veritabanı Windows kimlik doğrulamasını kullanarak bağlanır.

Bazı işlev hello depolama öykünücüsü ve Azure storage Hizmetleri farklar. Hello bu farklar hakkında daha fazla bilgi için bkz: [hello depolama öykünücüsü Azure Storage arasındaki farklar](#differences-between-the-storage-emulator-and-azure-storage) bu makalenin sonraki bölümlerinde bölümü.

## <a name="start-and-initialize-hello-storage-emulator"></a>Başlangıç ve hello depolama öykünücüsü başlatma
toostart hello Azure storage öykünücüsü:
1. Select hello **Başlat** düğmesini veya tuşuna hello **Windows** anahtarı.
1. Yazmaya başlayın `Azure Storage Emulator`.
1. Merhaba öykünücüsü hello görüntülenen uygulamalar listesinden seçin.

Merhaba depolama öykünücüsü başladığında, bir komut istemi penceresi görüntülenir. Bu konsol penceresi toostart ve durdurma hello storage öykünücüsünü kullanma, verileri temizlemek, durumunu Al ve hello öykünücü başlatma. Merhaba daha fazla bilgi için bkz [depolama öykünücüsü komut satırı aracını referans](#storage-emulator-command-line-tool-reference) bu makalenin sonraki bölümlerinde bölümü.

Merhaba öykünücüsü çalıştırırken hello Windows görev çubuğundaki bildirim alanında bir simge görürsünüz.

Merhaba depolama öykünücüsü komut istemi penceresini kapattığınızda hello depolama öykünücüsü toorun devam eder. Merhaba depolama öykünücüsü konsol penceresini toobring yeniden adımları hello depolama öykünücüsü başlıyorsanız gibi önceki hello izleyin.

Merhaba hello depolama öykünücüsü, ilk çalıştırdığınızda hello yerel depolama ortamı sizin için başlatılır. Hello başlatma işlemi yerel veritabanı bir veritabanı oluşturur ve her yerel depolama hizmet için HTTP bağlantı noktası ayırır.

Merhaba depolama öykünücüsü varsayılan olarak yüklenir çok`C:\Program Files (x86)\Microsoft SDKs\Azure\Storage Emulator`.

> [!TIP]
> Merhaba kullanabilirsiniz [Microsoft Azure Storage Gezgini](http://storageexplorer.com) toowork yerel depolama öykünücüsü kaynaklarını ile. Yüklü ve hello depolama öykünücüsü başlatılan sonra "(Geliştirme)" için "Depolama hesapları altında" Merhaba Depolama Gezgini kaynakları ağacında arayın.
>

### <a name="initialize-hello-storage-emulator-toouse-a-different-sql-database"></a>Merhaba depolama öykünücüsü toouse farklı bir SQL veritabanını başlatılamadı
Merhaba depolama öykünücüsü komut satırı aracı tooinitialize hello depolama öykünücüsü toopoint tooa SQL veritabanı örneği hello varsayılan yerel veritabanı örneği dışında kullanabilirsiniz:

1. Hello açıklandığı gibi açık hello depolama öykünücüsü konsol penceresi [başlangıç ve başlatma hello depolama öykünücüsü](#start-and-initialize-the-storage-emulator) bölümü.
1. Merhaba konsol penceresinde hello komutu, aşağıdaki yazın burada `<SQLServerInstance>` hello hello SQL Server örneğinin adıdır. toouse LocalDB, belirtin `(localdb)\MSSQLLocalDb` hello SQL Server örneği olarak.

  `AzureStorageEmulator.exe init /server <SQLServerInstance>`

  Merhaba öykünücüsü toouse hello varsayılan SQL Server örneği yönlendiren komut aşağıdaki hello de kullanabilirsiniz:

  `AzureStorageEmulator.exe init /server .\\`

  Veya hello veritabanı toohello varsayılan yerel veritabanı örneğini yeniden başlatır komutu aşağıdaki hello kullanabilirsiniz:

  `AzureStorageEmulator.exe init /forceCreate`

Bu komutlar hakkında daha fazla bilgi için bkz: [depolama öykünücüsü komut satırı aracını referans](#storage-emulator-command-line-tool-reference).

> [!TIP]
> Merhaba kullanabilirsiniz [Microsoft SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) , SQL Server örnekleri, hello LocalDB yükleme de dahil olmak üzere (SSMS) toomanage. Merhaba SMSS içinde **tooServer bağlanmak** iletişim kutusunda, belirtin `(localdb)\MSSQLLocalDb` hello içinde **sunucu adı:** alan tooconnect toohello yerel veritabanı örneği.

## <a name="authenticating-requests-against-hello-storage-emulator"></a>Merhaba storage öykünücüsüne karşı kimlik doğrulama istekleri
Yüklü ve hello depolama öykünücüsü başlatılan sonra kodunuzu onu karşı test edebilirsiniz. Anonim İstek olmadığı sürece hello bulutta Azure Storage gibi ile Merhaba storage öykünücüsüne karşı yaptığınız her istek, kimliğinizin doğrulanması gerekiyor. İstekleri paylaşılan anahtar kimlik doğrulaması kullanarak hello depolama öykünücüsü karşı veya bir paylaşılan erişim imzası (SAS) ile kimlik doğrulaması yapabilir.

### <a name="authenticate-with-shared-key-credentials"></a>Paylaşılan anahtar kimlik bilgileriyle kimlik doğrulaması
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Bağlantı dizeleri hakkında daha fazla bilgi için bkz: [yapılandırma Azure Storage bağlantı dizelerini](storage-configure-connection-string.md).

### <a name="authenticate-with-a-shared-access-signature"></a>İle paylaşılan erişim imzası kimlik doğrulaması
Merhaba Xamarin kitaplığı gibi bazı Azure storage istemcisi kitaplıklarını yalnızca bir paylaşılan erişim imzası (SAS) belirteci ile kimlik doğrulamasını destekler. Merhaba SAS belirteci hello gibi bir araç kullanarak oluşturabileceğiniz [Depolama Gezgini](http://storageexplorer.com/) veya paylaşılan anahtar kimlik doğrulamasını destekleyen başka bir uygulama.

Azure PowerShell kullanarak bir SAS belirteci de oluşturabilirsiniz. Merhaba aşağıdaki örnekte tam izinleri tooa blob kapsayıcısı bir SAS belirteci oluşturur:

1. Henüz yapmadıysanız Azure PowerShell'i yükleyin (Merhaba en son sürümünü hello Azure PowerShell cmdlet'lerini kullanarak önerilir). Yükleme yönergeleri için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/install-azurerm-ps).
2. Azure PowerShell'i açın ve aşağıdaki komutları, değiştirme hello çalıştırın `ACCOUNT_NAME` ve `ACCOUNT_KEY==` kendi kimlik bilgileriyle ve `CONTAINER_NAME` seçtiğiniz bir ada sahip:

```powershell
$context = New-AzureStorageContext -StorageAccountName "ACCOUNT_NAME" -StorageAccountKey "ACCOUNT_KEY=="

New-AzureStorageContainer CONTAINER_NAME -Permission Off -Context $context

$now = Get-Date

New-AzureStorageContainerSASToken -Name CONTAINER_NAME -Permission rwdl -ExpiryTime $now.AddDays(1.0) -Context $context -FullUri
```

Merhaba elde edilen hello yeni kapsayıcı için paylaşılan erişim imzası URI benzer olmalıdır:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2015-07-08T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3Dsss
```

Bu örnek ile oluşturulmuş hello paylaşılan erişim imzası bir gün için geçerli değil. Merhaba imza hello kapsayıcı içindeki tam erişim (okuma, yazma, silme, liste) tooblobs verir.

Paylaşılan erişim imzaları ile ilgili daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları (SAS) Azure storage'da](storage-dotnet-shared-access-signature-part-1.md).

## <a name="addressing-resources-in-hello-storage-emulator"></a>Merhaba depolama öykünücüsü kaynaklarında adresleme
Merhaba hizmet uç noktaları hello depolama öykünücüsü Azure storage hesabı olanlardan farklı. Merhaba yerel bilgisayarın etki alanı adı çözümlemesi, hello depolama öykünücüsü uç noktaları toobe yerel adresler gerektiren gerçekleştirmez çünkü hello farktır.

Bir Azure depolama hesabı kaynak adres için düzeni aşağıdaki hello kullanın. Merhaba hesap adı hello URI ana bilgisayar adı bir parçasıdır ve ele alınan hello kaynak hello URI yolu bir parçasıdır:

`<http|https>://<account-name>.<service-name>.core.windows.net/<resource-path>`

Örneğin, hello aşağıdaki URI bir Azure depolama hesabındaki bir blob için geçerli bir adresi şöyledir:

`https://myaccount.blob.core.windows.net/mycontainer/myblob.txt`

Ancak, depolama öykünücüsü Merhaba, hello yerel bilgisayarın etki alanı adı çözümlemesine gerçekleştirmez çünkü hello hesap adı hello URI yolu hello ana bilgisayar adı yerine bir parçasıdır. Merhaba depolama öykünücüsü bir kaynak için URI biçimi aşağıdaki hello kullan:

`http://<local-machine-address>:<port>/<account-name>/<resource-path>`

Örneğin, hello aşağıdaki adresi hello depolama öykünücüsü bir blob'a erişmek için kullanılabilir:

`http://127.0.0.1:10000/myaccount/mycontainer/myblob.txt`

Merhaba depolama öykünücüsü Hello hizmet uç noktalar şunlardır:

* BLOB hizmeti:`http://127.0.0.1:10000/<account-name>/<resource-path>`
* Kuyruk hizmeti:`http://127.0.0.1:10001/<account-name>/<resource-path>`
* Tablo hizmeti:`http://127.0.0.1:10002/<account-name>/<resource-path>`

### <a name="addressing-hello-account-secondary-with-ra-grs"></a>Merhaba hesap RA-GRS ile ikincil adresleme
Sürüm 3.1 ile başlayarak, hello depolama öykünücüsü okuma erişimli coğrafi olarak yedekli çoğaltma (RA-GRS) destekler. Depolama kaynaklarını hello bulut hem de hello yerel öykünücüsü için hello ikincil konum erişebilirsiniz göre ekleme - ikincil toohello hesap adı. Örneğin, adres aşağıdaki hello hello salt okunur ikincil hello depolama öykünücüsünde kullanarak blob erişmek için kullanılabilir:

`http://127.0.0.1:10000/myaccount-secondary/mycontainer/myblob.txt`

> [!NOTE]
> Merhaba depolama öykünücü ile ikincil programlı erişim toohello için hello depolama istemci kitaplığı için .NET 3.2 veya sonraki bir sürümü kullanın. Merhaba bkz [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx) Ayrıntılar için.
>
>

## <a name="storage-emulator-command-line-tool-reference"></a>Depolama öykünücüsü komut satırı aracı başvurusu
Merhaba depolama öykünücüsü başlattığınızda sürüm 3. 0'dan başlayarak, bir konsol penceresi görüntülenir. Ve diğer işlemleri gerçekleştirmek için durum Hello komut satırında sorgu yanı sıra hello konsol penceresi toostart ve durdurma hello öykünücüsü kullanın.

> [!NOTE]
> Microsoft Azure işlem öykünücüsü yüklü hello varsa hello depolama öykünücüsü başlattığında sistem tepsisi simgesi görüntülenir. Merhaba simgesi tooreveal üzerinde grafiksel toostart sağlayan bir menüsünü sağ tıklatın ve hello depolama öykünücüsü durdurun.
>
>

### <a name="command-line-syntax"></a>Komut satırı sözdizimi
`AzureStorageEmulator.exe [start] [stop] [status] [clear] [init] [help]`

### <a name="options"></a>Seçenekler
Seçenekler, türü tooview hello listesinde `/help` hello komut isteminde.

| Seçenek | Açıklama | Komut | Bağımsız Değişkenler |
| --- | --- | --- | --- |
| **Start** |Merhaba depolama öykünücüsü başlatır. |`AzureStorageEmulator.exe start [-inprocess]` |*-InProcess*: yeni bir işlem oluşturmak yerine geçerli işlem hello hello öykünücü başlatma. |
| **Durdur** |Merhaba depolama öykünücüsü durdurur. |`AzureStorageEmulator.exe stop` | |
| **Durumu** |Baskı siparişi hello depolama öykünücüsü durumunu hello. |`AzureStorageEmulator.exe status` | |
| **Temizle** |Merhaba komut satırında belirtilen tüm hizmetleri Hello verileri temizler. |`AzureStorageEmulator.exe clear [blob] [table] [queue] [all]                                                    ` |*BLOB*: blob verileri temizler. <br/>*sıra*: sırası verileri temizler. <br/>*Tablo*: Tablo verileri temizler. <br/>*tüm*: tüm hizmetlerin tüm verileri temizler. |
| **Init** |Tek seferlik başlatma tooset hello öykünücüsü yukarı gerçekleştirir. |<code>AzureStorageEmulator.exe init [-server serverName] [-sqlinstance instanceName] [-forcecreate&#124;-skipcreate] [-reserveports&#124;-unreserveports] [-inprocess]</code> |*-Sunucu Sunucuadı\örnekadı*: hello SQL örneğini barındıran hello sunucusunu belirtir. <br/>*-sqlınstance InstanceName*: hello varsayılan sunucu örneğinde kullanılan hello SQL örneği toobe hello adını belirtir. <br/>*-forcecreate*: zaten mevcut olsa bile hello SQL veritabanını oluşturmayı zorlar. <br/>*-skipcreate*: hello SQL veritabanını oluşturmayı atlar. Bu - forcecreate önceliklidir.<br/>*-reserveports*: tooreserve hello HTTP bağlantı noktaları hello servisleri ile ilişkili çalışır.<br/>*-unreserveports*: hello servisleri ile ilişkili hello HTTP bağlantı noktaları için tooremove ayırmaları çalışır. Bu - reserveports önceliklidir.<br/>*-InProcess*: yeni bir işlem örnekten oluşturmak yerine hello geçerli işlem başlatma gerçekleştirir. Merhaba geçerli işlem yükseltilmiş izinleri olan bağlantı noktası ayırmaları değiştiriliyorsa başlatılması gerekir. |

## <a name="differences-between-hello-storage-emulator-and-azure-storage"></a>Merhaba depolama öykünücüsü Azure Storage arasındaki farklar
Merhaba depolama öykünücüsü yerel bir SQL örneğinde çalışan benzetilmiş bir ortam olduğundan, arasındaki işlevsel farklılıklar hello öykünücüsü ve Azure storage hesabı hello bulutta vardır:

* yalnızca tek bir sabit hesap ve bilinen bir kimlik doğrulama anahtarı Hello depolama öykünücüsünü destekler.
* Merhaba depolama öykünücüsü ölçeklenebilir depolama hizmeti ve çok sayıda eşzamanlı istemci desteklemiyor.
* Bölümünde açıklandığı gibi [hello depolama öykünücüsü kaynaklarında adresleme](#addressing-resources-in-the-storage-emulator), kaynakları ele farklı hello depolama öykünücüsü Azure storage hesabı karşı içinde. Etki alanı adı çözümlemesine hello bulut ancak değil hello yerel bilgisayarda kullanılabilir olduğu için bu farktır.
* Sürüm 3.1 ile başlayarak, hello depolama öykünücüsü hesabı okuma erişimli coğrafi olarak yedekli çoğaltma (RA-GRS) destekler. Hello öykünücüsü, RA-GRS etkinleştirilmiş tüm hesapları sahip ve hello birincil ve ikincil çoğaltmalar arasında hiçbir zaman bir gecikme yoktur. Merhaba Blob hizmeti istatistikleri almak, kuyruk hizmeti istatistikleri almak ve tablo hizmeti istatistikleri almak işlemler hello hesabında ikincil desteklenir ve her zaman hello hello değerini döndürür `LastSyncTime` geçerli saati according toohello temel hello gibi yanıt öğesi SQL veritabanı.
* Dosya hizmeti hello ve SMB protokolü hizmet uç noktaları şu anda hello depolama öykünücüsünde desteklenmez.
* Merhaba öykünücüsü tarafından henüz desteklenmeyen bir hello Depolama Hizmetleri sürümünü kullanıyorsanız, hello depolama öykünücüsü VersionNotSupportedByEmulator hata (HTTP durum kodu 400 - Hatalı istek) döndürür.

### <a name="differences-for-blob-storage"></a>Blob storage için farklar
farkları aşağıdaki hello hello öykünücüsü tooBlob depolama Uygula:

* Merhaba depolama öykünücüsü yalnızca too2 GB blob boyutlarını destekler.
* Artımlı kopya kopyalanır, hello hizmetinde bir hata döndürür üzerine BLOB'lar toobe alınan anlık sağlar.
* Get sayfa aralıklarını fark artımlı kopya Blob kullanarak kopyalanan anlık görüntüler arasında çalışmaz.
* Merhaba kira kimliği hello istekte belirtilmemiş olsa bile bir Blob Put işlemi hello depolama öykünücü ile etkin bir kira var. bir blob karşı başarılı olabilir.
* İşlemleri hello öykünücüsü tarafından desteklenmez Blob ekleyin. Bir ek blobu üzerinde bir işlemi çalışırken FeatureNotSupportedByEmulator hata (HTTP durum kodu 400 - Hatalı istek) döndürür.

### <a name="differences-for-table-storage"></a>Table storage farkları
farkları aşağıdaki hello hello öykünücüsü tooTable depolama Uygula:

* Merhaba hello depolama öykünücüsü tablo hizmetinde tarih özelliklerinde yalnızca SQL Server 2005'in (gerekli toobe 1 Ocak 1753'den sonraki oldukları) tarafından desteklenen hello aralığını destekler. Tüm tarih 1 Ocak 1753 önce değiştirilen toothis değeri. Merhaba tarihleri kesinliğini olduğu tarihleri kesin too1 olduğu anlamına gelir, SQL Server 2005'in sınırlı toohello duyarlık/saniyede 300th.
* Merhaba depolama öykünücüsü değerinden 512 bayt her bölüm anahtarını ve satır anahtar özellik değerlerini destekler. Ayrıca, hello hesap adı, tablo adını ve anahtar özellik adlarının toplam boyutu hello birlikte 900 baytı aşamaz.
* Merhaba toplam hello depolama öykünücüsü tablosunda bir satırı 1 MB'tan sınırlı tooless boyutudur.
* Merhaba depolama öykünücüsünde türü özellikleri veri `Edm.Guid` veya `Edm.Binary` desteği yalnızca hello `Equal (eq)` ve `NotEqual (ne)` Karşılaştırma işleçleri sorgu dizeleri filtre.

### <a name="differences-for-queue-storage"></a>Kuyruk depolama farkları
Merhaba öykünücüsünde farklar belirli tooQueue depolama vardır.

## <a name="storage-emulator-release-notes"></a>Depolama öykünücüsü sürüm notları
### <a name="version-52"></a>5.2 sürümü
* Hello depolama öykünücüsü artık Blob, kuyruk ve tablo Hizmeti uç noktalarda hello depolama hizmetleri 2017-04-17 sürümünü destekler.
* Bir hata olduğu tablo özellik değerlerini düzgün şekilde kodlanmamış sabit.

### <a name="version-51"></a>Sürüm 5.1
* Merhaba depolama öykünücüsü hello burada döndürdü hatanın düzeltildiğini `DataServiceVersion` burada hello hizmet değildi bazı yanıtları üstbilgisinde.

### <a name="version-50"></a>Sürüm 5.0
* Merhaba depolama öykünücüsü yükleyici artık için varolan MSSQL denetler ve .NET Framework yükler.
* Merhaba depolama öykünücüsü yükleyici artık hello veritabanı yükleme bir parçası olarak oluşturur. Veritabanı hala başlangıç bir parçası olarak gerekirse oluşturulacak.
* Veritabanı oluşturma artık yükseltme gerektirir.
* Bağlantı noktası ayırmaları başlatma için artık gerekli değildir.
* Aşağıdaki seçenekleri çok şu hello ekler`init`: `-reserveports` (yükseltme gerekir), `-unreserveports` (yükseltme gerekir), `-skipcreate`.
* Merhaba hello sistem tepsisi simgesi depolama öykünücüsü UI seçeneği artık hello komut satırı arabirimi başlatır. Merhaba eski GUI artık kullanılamıyor.
* Bazı DLL'lerin kaldırılmış veya yeniden adlandırılamaz.

### <a name="version-46"></a>Sürüm 4.6
* Hello depolama öykünücüsü şimdi Blob, kuyruk ve tablo Hizmeti uç noktalarda hello depolama hizmetleri 2016-05-31 sürümünü destekler.

### <a name="version-45"></a>Sürüm 4.5
* Veritabanı yedekleme hello adlandırıldığında hello depolama öykünücüsü toofail yüklenmesini ve başlatma neden olan bir hata sabit.

### <a name="version-44"></a>Sürüm 4.4
* Merhaba depolama öykünücüsü şimdi sürümü 2015-12-11, hello depolama hizmetleri Blob, kuyruk ve tablo Hizmeti uç noktalarda destekler.
* Merhaba depolama öykünücüsü'nın çöp toplama blob verisi artık çok sayıda BLOB ilgilenirken daha verimli olur.
* Kapsayıcı hello depolama hizmeti bunu nasıl yapar biraz daha farklı doğrulanmış ACL XML toobe neden olan bir hata sabit.
* Bazen max neden hatanın düzeltildiğini ve hello yanlış saat diliminde min DateTime değerleri toobe bildirdi.

### <a name="version-43"></a>Sürümü 4.3
* Merhaba depolama öykünücüsü şimdi sürüm 2015-07-08 hello depolama hizmetleri Blob, kuyruk ve tablo Hizmeti uç noktalarda destekler.

### <a name="version-42"></a>4.2 sürümü
* Merhaba depolama öykünücüsü şimdi sürüm 2015-04-05 hello depolama hizmetleri Blob, kuyruk ve tablo Hizmeti uç noktalarda destekler.

### <a name="version-41"></a>Sürümü 4.1
* Merhaba depolama öykünücüsü sürümü 2015-02-21 hello depolama hizmetleri, Blob, kuyruk ve tablo Hizmeti uç noktalarda, hello yeni ekleme Blob özellikleri dışında şimdi destekler.
* Merhaba öykünücüsü tarafından henüz desteklenmeyen bir hello Depolama Hizmetleri sürümünü kullanıyorsanız, hello öykünücüsü anlamlı bir hata mesajı döndürür. Merhaba hello öykünücüsü en son sürümünü kullanmanızı öneririz. Lütfen bir VersionNotSupportedByEmulator hatası (HTTP durum kodu 400 - Hatalı istek) karşılaşırsanız hello hello depolama öykünücüsü en son sürümünü yükleyin.
* Bir hata; burada görüntülerle bir yarış durumu nedeniyle tablo varlık veri toobe eşzamanlı birleştirme işlemleri sırasında hatalı sabit.

### <a name="version-40"></a>Sürüm 4.0
* Merhaba depolama öykünücüsü yürütülebilir çok adlandırılmıştır*AzureStorageEmulator.exe*.

### <a name="version-32"></a>Sürüm 3.2
* Merhaba depolama öykünücüsü şimdi Blob, kuyruk ve tablo Hizmeti uç noktalarda hello depolama hizmetleri 2014-02-14 sürümünü destekler. Dosya Hizmeti uç noktalarını hello depolama öykünücüsünde şu anda desteklenmemektedir. Bkz: [hello Azure Storage Hizmetleri için sürüm oluşturma](/rest/api/storageservices/Versioning-for-the-Azure-Storage-Services) sürümü 2014-02-14 hakkında ayrıntılı bilgi için.

### <a name="version-31"></a>Sürüm 3.1
* Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) hello depolama öykünücüsünde artık desteklenmektedir. Merhaba alma Blob hizmeti istatistikleri, kuyruk hizmeti istatistikleri almak ve tablo hizmeti istatistikleri API'leri almak ikincil hello hesabı için desteklenir ve her zaman geçerli zaman according toohello SQL temel hello gibi hello LastSyncTime yanıt öğesi hello değerini döndürür Veritabanı. Merhaba depolama öykünücü ile ikincil programlı erişim toohello için hello depolama istemci kitaplığı için .NET 3.2 veya sonraki bir sürümü kullanın. Merhaba Microsoft Azure Storage istemci kitaplığı .NET başvurusu için Ayrıntılar için bkz.

### <a name="version-30"></a>Sürüm 3.0
* Hello Azure storage öykünücüsü artık aynı hello işlem öykünücüsü paketini hello içinde geliyordu.
* Merhaba depolama öykünücüsü grafik kullanıcı arabirimi lehinde kodlanabilir bir komut satırı arabirimi kullanım dışıdır. Depolama öykünücüsü komut satırı aracını referans hello komut satırı arabirimi hakkında daha fazla bilgi için bkz. Merhaba grafik arabirim toobe sürüm 3.0 mevcut devam edecek ancak hello işlem öykünücüsü hello sistem tepsisi simgesi üzerinde sağ tıklatıp depolama öykünücüsü UI Göster'i seçerek yüklendiğinde yalnızca erişilebilir.
* Sürüm 2013-08-15'hello Azure depolama hizmetleri artık tam olarak desteklenmektedir. (Daha önce bu sürümü yalnızca sürüm 2.2.1 depolama öykünücüsü tarafından desteklenen Önizleme.)

## <a name="next-steps"></a>Sonraki adımlar

* Merhaba platformlar arası, topluluk tarafından tutulan açık kaynak depolama öykünücüsü değerlendirmek [Azurite](https://github.com/arafato/azurite). 
* [.NET kullanarak azure depolama örnekleri](storage-samples-dotnet.md) Uygulamanızı geliştirirken kullanabileceğiniz bağlantılar tooseveral kod örnekleri içerir.
* Merhaba kullanabilirsiniz [Microsoft Azure Storage Gezgini](http://storageexplorer.com) , bulut depolama hesabı ve hello depolama öykünücüsü kaynaklarla toowork.
