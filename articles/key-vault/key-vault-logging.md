---
title: "aaaAzure anahtar kasası günlüğü | Microsoft Docs"
description: "Azure anahtar kasası kullanmaya başlama Öğreticisi bu toohelp kullanmak günlüğü."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Azure Anahtar Kasası Günlüğü
Azure Anahtar Kasası çoğu bölgede kullanılabilir. Daha fazla bilgi için bkz: Merhaba [anahtar kasası fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Giriş
Bir veya daha fazla anahtar kasası oluşturduktan sonra büyük olasılıkla erişilen ve kim tarafından ne zaman ve nasıl anahtarınızı kasaları toomonitor isteyeceksiniz. Anahtar Kasası için günlüğe kaydetmeyi etkinleştirerek bunu yapabilirsiniz; böylece sağladığınız Azure depolama hesabında bilgiler kaydedilir. Belirttiğiniz depolama hesabı için **insights-logs-auditevent** adlı yeni bir kapsayıcı oluşturulur ve birden çok anahtar kasasının günlüklerini toplamak için bu depolama hesabını kullanabilirsiniz.

En fazla günlük bilgilerinize erişebilir, 10 dakika sonra hello anahtar kasası işleminden. Çoğu durumda, bundan daha hızlı olacaktır.  Depolama hesabınızdaki günlüklerinizi tooyou toomanage öyledir:

* Standart Azure erişim denetimi yöntemlerini toosecure günlüklerinize erişebilecek kişileri kısıtlayarak kullanın.
* Artık depolama hesabınız tookeep, istediğiniz günlükleri silin.

Azure anahtar, kasası günlüğü ile toocreate Başlarken Bu öğretici toohelp kullanmak depolama hesabınızın günlüğe yazılmasını etkinleştirmek ve toplanan hello günlük bilgilerini yorumlamak.  

> [!NOTE]
> Bu öğretici toocreate nasıl anahtar kasalarının, anahtarların veya gizli için yönergeler içermez. Bu bilgi için bkz. [Azure Anahtar Kasası ile çalışmaya başlama](key-vault-get-started.md). Alternatif olarak, Platformlar Arası Komut Satırı Arabirimi yönergeleri için [bu eşdeğer öğreticiye](key-vault-manage-with-cli2.md) bakın.
>
> Şu anda hello Azure portalında Azure anahtar kasası yapılandıramazsınız. Bunun yerine, bu Azure PowerShell yönergelerini kullanın.
>
>

Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğreticiyi izleyerek hello olması gerekir:

* Kullanmakta olduğunuz var olan bir anahtar kasası.  
* Azure PowerShell'in, **en az 1.0.1 sürümü**. tooinstall Azure PowerShell ve Azure aboneliğinizle ilişkilendirmek için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). Azure PowerShell'i zaten yüklediyseniz ve hello sürüm hello Azure PowerShell konsolundan bilmiyorsanız, çalışamazsa `(Get-Module azure -ListAvailable).Version`.  
* Anahtar Kasası günlükleriniz için Azure'da yeterli depolama.

## <a id="connect"></a>Tooyour abonelikleri Bağlan
Bir Azure PowerShell oturumu Başlat ve tooyour Azure hesabı komutu aşağıdaki hello ile oturum açın:  

    Login-AzureRmAccount

Merhaba açılır tarayıcı penceresinde Azure hesabı kullanıcı adınızı ve parolanızı girin. Azure PowerShell varsayılan olarak bu hesap ile ilişkilendirilmiş tüm hello abonelikleri alır, birinci kullanır hello.

Birden çok aboneliğiniz varsa, kullanılan toocreate olan belirli bir toospecify olabilir, Azure anahtar kasası. Merhaba toosee hello abonelikleri hesabınız için aşağıdaki komutu yazın:

    Get-AzureRmSubscription

Günlüğünü tutacağınız, anahtar kasasıyla türü ilişkili ardından toospecify hello abonelik:

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> Bu önemli bir adımdır ve hesabınızla ilişkili birden çok abonelik varsa özellikle yararlıdır. Bu adım atlanır içeriyorsa bir hata tooregister Microsoft.ınsights alabilirsiniz.
>   
>

Azure PowerShell yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a id="storage"></a>Günlükleriniz için yeni bir depolama hesabı oluşturma
Günlükleriniz için var olan depolama hesabını kullanabilmenize karşın, ayrılmış tooKey kasası günlükleri olacak yeni bir depolama hesabı oluşturacağız. Ne zaman toospecify bu sahibiz kolaylık sağlamak için daha sonra biz adlı bir değişkende hello ayrıntıları depolayacağınız **sa**.

Ek yönetim kolaylığı için aynı zamanda kullanacağız anahtar kasamızı içeren bir hello gibi hello aynı kaynak grubu. Merhaba gelen [başlama Öğreticisi](key-vault-get-started.md), bu kaynak grubu adında **ContosoResourceGroup** ve toouse hello Doğu Asya konumunu devam edeceğiz. Bunları uygun şekilde kendi değerlerinizle değiştirin:

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> Toouse mevcut bir depolama hesabını karar verirseniz, kullanmanız gereken anahtar kasanızı ve hello Klasik dağıtım modeli yerine hello Resource Manager dağıtım modeli kullanmanız gerektiği gibi aynı abonelik hello.
>
>

## <a id="identify"></a>Merhaba anahtar kasası günlükleriniz için tanımlayın
Bizim alma başlatılan öğreticide öğreticimizde anahtar kasamızın adı olan **ContosoKeyVault**, ad ve hello ayrıntıları adlı bir değişkende depolamaya toouse devam edeceğiz **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>Günlüğe kaydetmeyi etkinleştirme
tooenable anahtar kasası için günlüğe kaydetme, hello Set-AzureRmDiagnosticSetting cmdlet'ini kullanacağız, hello değişkenleri ile birlikte yeni depolama hesabımız ve anahtar kasamız için oluşturduğumuz. Merhaba ayrıca yaparız **-etkin** çok bayrak**$true** ve hello kategori tooAuditEvent (Merhaba yalnızca kategori anahtar kasası günlüğü için) olarak ayarlayın:

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

Bunun için Hello çıkış şunları içerir:

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


Bu günlük kaydı bilgileri tooyour depolama hesabı kaydedilirken anahtar kasanız için şimdi etkin olduğunu doğrular.

İsteğe bağlı olarak günlükleriniz için eski günlüklerin otomatik olarak silinmesi gibi bir bekletme ilkesi de ayarlayabilirsiniz. Örneğin, bekletme ilkesi kullanılarak ayarlanan **- RetentionEnabled** çok bayrak**$true** ve **- RetentionInDays** parametresi çok**90** şekilde 90 günden daha eski günlükleri otomatik olarak silinir.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

Günlüğe kaydedilenler:

* Erişim izinleri, sistem hataları veya hatalı istekler sonucunda başarısız olan istekleri içeren tüm kimliği doğrulanmış REST API istekleri günlüğe kaydedilir.
* Operations hello anahtarı oluşturma, silme, ayarı anahtar kasası erişim ilkelerini içeren, kendi, kasa ve etiketler gibi anahtar kasası öznitelikler güncelleştiriliyor.
* Anahtarları ve gizli anahtarları oluşturma, değiştirme veya bu bir anahtar veya gizli anahtarları silme içerir hello anahtar kasasında işlemleri; oturum gibi işlemleri doğrulayın, şifrelemek, şifresini, sarmalama ve anahtarları kaydırma, gizli, anahtarları ve gizli anahtarları ve sürümlerine Al.
* Bir 401 yanıtına neden olan kimliği doğrulanmamış istekler. Örneğin, bir taşıyıcı belirtecine sahip olmayan veya hatalı biçimlendirilmiş ya da süresi dolmuş veya geçersiz bir belirtece sahip olan istekler.  

## <a id="access"></a>Günlüklerinize erişme
Anahtar kasası günlükleri hello depolanan **insights-logs-auditevent** hello depolama hesabı sağladığınız kapsayıcısında. toolist bu kapsayıcıdaki tüm hello BLOB'lar yazın:

İlk olarak hello kapsayıcı adı için bir değişken oluşturun. Merhaba ilerlemesi hello kalanı boyunca kullanılır.

    $container = 'insights-logs-auditevent'

toolist bu kapsayıcıdaki tüm hello BLOB'lar yazın:

    Get-AzureStorageBlob -Container $container -Context $sa.Context
Merhaba çıkış benzeri toothis görünür:

**Kapsayıcı Uri'si: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Ad**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

Bu Çıkışta gördüğünüz gibi hello bloblar bir adlandırma kuralını izler: **ResourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m = <minute> /dosya adı.JSON**

Merhaba tarih ve saat değerleri UTC'yi kullanır.

Merhaba aynı depolama hesabı birden fazla kaynak için kullanılan toocollect günlükleri olabileceğinden, hello hello blob adındaki tam kaynak kimliği çok kullanışlı tooaccess veya gereksinim duyduğunuz indirme yalnızca hello BLOB'lar değil. Ancak bunu yapmadan önce biz değineceğiz nasıl toodownload tüm BLOB'ları hello.

İlk olarak, bir klasör toodownload hello BLOB'lar oluşturun. Örneğin:

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

Ardından tüm blobların listesini alın:  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

Bu liste 'Get-AzureStorageBlobContent' toodownload hello BLOB'ları aracılığıyla bizim hedef klasöre kanal:

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

Bu ikinci komutu çalıştırdığınızda, hello  **/**  hello blob adlarındaki sınırlayıcı hello hedef klasörün altında tam klasör yapısı oluşturun ve bu yapı dosyaları olarak kullanılan toodownload ve deposu hello BLOB'lar olacaktır.

tooselectively blobları indirmek, joker karakter kullanın. Örneğin:

* Birden çok anahtar kasanız varsa ve yalnızca bir anahtar kasası için toodownload günlükleri istiyorsanız CONTOSOKEYVAULT3 adlı:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* Birden çok kaynak gruplarınız ve yalnızca bir kaynak grubu için toodownload günlükleri istiyorsanız kullanın `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* Merhaba Ocak 2016 ayı için tüm hello günlüklerini toodownload istiyorsanız, kullanmak `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

Hello neler olduğuna bakmaya hazır toostart oturum artık olduğunuz. Ancak, Get-AzureRmDiagnosticSetting tooknow gerekebilecek için iki parametre daha üzerine geçmeden önce:

* anahtar kasası kaynağınızın tanılama ayarlarının tooquery hello durumu:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* anahtar kasası kaynağınızın için toodisable günlüğü:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>Anahtar Kasası günlüklerinizi yorumlama
Tek tek bloblar JSON blobu olarak biçimlendirilip metin olarak depolanır. Bu `Get-AzureRmKeyVault -VaultName 'contosokeyvault'` çalıştırılarak oluşturulmuş bir günlük girişi örneğidir:

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


Merhaba aşağıdaki tabloda hello alan adları ve açıklamaları listelenmektedir.

| Alan adı | Açıklama |
| --- | --- |
| time |Tarih ve saat (UTC). |
| resourceId |Azure Resource Manager Kaynak Kimliği. Anahtar kasası günlükleri için bu her zaman hello anahtar kasası kaynak kimliğidir. |
| operationName |Merhaba sonraki tabloda belirtildiği gibi hello işlemin adı. |
| operationVersion |Bu hello istemci tarafından istenilen hello REST API'si sürümüdür. |
| category |Anahtar kasası günlükleri için AuditEvent hello tek ve kullanılabilir bir değerdir. |
| resultType |REST API'si isteğinin sonucu. |
| resultSignature |HTTP durumu. |
| resultDescription |Kullanılabilir olduğunda hello sonuç hakkında ek açıklama. |
| durationMs |Milisaniye cinsinden tooservice hello REST API isteği, geçen süre. Hello istemci tarafında ölçmek hello süre bu süreyle eşleşmeyebilir şekilde bu hello ağ gecikmesini içermez. |
| callerIpAddress |Merhaba isteği yapan hello istemci IP adresi. |
| correlationId |İstemci hello isteğe bağlı bir GUID toocorrelate istemci-tarafı günlüklerini Hizmet tarafı (anahtar kasası) günlükleriyle geçirebilirsiniz. |
| identity |Merhaba REST API'si isteği yapılırken sunulan hello belirteç kimlik. Bu genellikle bir "kullanıcı", "hizmet sorumlusu" veya bir Azure PowerShell cmdlet'inden kaynaklanan bir istekte olduğu gibi "kullanıcı+uygulama kimliği" birleşimidir. |
| properties |Bu alan hello işleme (operationName) bağlı olarak farklı bilgiler içerir. Çoğu durumda, istemci bilgilerini (Merhaba istemci tarafından geçirilen hello useragent dizesi) içeren REST API'SİNİN tam istek URI'sini ve HTTP durum kodu hello. Ayrıca, bir nesne bir istek (örneğin, KeyCreate veya VaultGet) nedeniyle döndürüldüğünde anahtar URI'sini ("id") olarak, kasa URI'sini veya gizli anahtar URI'sini hello içerecektir. |

Merhaba **operationName** alan değerleri ObjectVerb biçimindedir. Örneğin:

* Tüm anahtar kasası işlemleri hello sahip ' kasası`<action>`' gibi biçimde `VaultGet` ve `VaultCreate`.
* Tüm anahtar işlemleri hello sahip ' anahtar`<action>`' gibi biçimde `KeySign` ve `KeyList`.
* Tüm gizli anahtar işlemleri hello sahip ' gizli`<action>`' gibi biçimde `SecretGet` ve `SecretListVersions`.

Aşağıdaki tablonun hello hello operationName ve karşılık gelen REST API'si komutu listelenmektedir.

| operationName | REST API'si Komutu |
| --- | --- |
| Kimlik Doğrulaması |Azure Active Directory uç noktası aracılığıyla |
| VaultGet |[Bir anahtar kasası hakkında bilgi edinme](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[Anahtar kasası oluşturma veya güncelleştirme](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[Anahtar kasası silme](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[Bir anahtar kasasını güncelleştirme](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[Bir kaynak grubundaki tüm anahtar kasalarını listeleme](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[Anahtar oluşturma](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[Bir anahtar hakkında bilgi edinme](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[Bir kasaya anahtar aktarma](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[Bir anahtarı yedekleme](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx). |
| KeyDelete |[Anahtar silme](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[Bir anahtarı geri yükleme](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[Bir anahtar ile oturum açma](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[Bir anahtar ile doğrulama](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[Bir anahtarı sarmalama](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[Bir anahtarı kaydırma](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[Bir anahtar ile şifreleme](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[Bir anahtar ile şifre çözme](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[Bir anahtarı güncelleştirme](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[Bir kasadaki listesi hello anahtarları](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[Bir anahtar hello sürümlerini listeleme](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[Gizli anahtar oluşturma](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[Gizli anahtar alma](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[Gizli anahtarı güncelleştirme](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[Gizli anahtarı silme](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[Bir kasadaki gizli anahtarları listeleme](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[Bir gizli anahtarın sürümlerini listeleme](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Log Analytics'i kullanma

Azure anahtar kasası AuditEvent günlüklerini günlük analizi tooreview içinde hello Azure anahtar kasası çözüm kullanabilirsiniz. Daha fazla bilgi için bu, nasıl tooset bakın dahil olmak üzere [günlük analizi Azure anahtar kasası çözümde](../log-analytics/log-analytics-azure-key-vault.md). Çözümden burada ilk, günlükleri tooan Azure depolama hesabı yönlendirilir ve buradan günlük analizi tooread yapılandırılmış hello günlük analizi Önizleme sırasında sunulan hello eski anahtar kasası toomigrate gerekiyorsa bu makale yönergeleri de içerir.

## <a id="next"></a>Sonraki adımlar
Azure Anahtar Kasası'nın bir web uygulamasında kullanıldığı bir öğretici için bkz. [Azure Anahtar Kasası'nı bir Web Uygulamasından Kullanma](key-vault-use-from-web-application.md).

Programlama başvuruları için bkz: [Azure anahtar kasası Geliştirici Kılavuzu hello](key-vault-developers-guide.md).

Azure Anahtar Kasası'na yönelik Azure PowerShell 1.0 cmdlet'leri listesi için bkz. [Azure Anahtar Kasası Cmdlet'leri](/powershell/module/azurerm.keyvault/#key_vault).

Anahtar döndürme ve Azure anahtar kasası ile günlük denetim bir öğretici için bkz: [toosetup anahtar kasası son tooend ile nasıl anahtar döndürme ve Denetim](key-vault-key-rotation-log-monitoring.md).
