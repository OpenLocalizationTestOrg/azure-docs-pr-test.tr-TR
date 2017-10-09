---
title: "aaaAzure işlem - Linux tanılama uzantısını | Microsoft Docs"
description: "Nasıl tooconfigure Azure Linux tanılama uzantısını (LAD) toocollect ölçümleri hello ve Linux Azure'da çalışan Vm'lerden gelen olayları günlüğe kaydedin."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Linux tanılama uzantısını toomonitor ölçümleri ve günlükleri kullanın

Bu belgede sürüm 3.0 ve hello Linux tanılama uzantı, daha yeni açıklanmaktadır.

> [!IMPORTANT]
> 2.3 ve eski sürümü hakkında daha fazla bilgi için bkz: [bu belgeyi](./classic/diagnostic-extension-v2.md).

## <a name="introduction"></a>Giriş

Merhaba Linux tanılama uzantısını Microsoft Azure üzerinde çalışan bir Linux VM kullanıcı İzleyicisi Merhaba durumunu yardımcı olur. Hello aşağıdaki özellikleri içerir:

* VM hello sistem performans ölçümleri toplar ve bunları belirtilen depolama hesabı belirli bir tabloda depolar.
* Syslog günlüğü olaylarını alır ve bunları belirli bir depolama hesabı belirlenmiş hello tabloda depolar.
* Toplanan ve karşıya kullanıcılar toocustomize hello veri ölçümleri sağlar.
* Kullanıcıların toocustomize hello syslog tesis ve toplanan ve karşıya olayların önem düzeyleri sağlar.
* Kullanıcıların tooupload belirtilen günlük dosyaları tooa atanan depolama tablosu sağlar.
* Ölçümleri ve günlük olayları tooarbitrary EventHub uç noktaları ve JSON biçimli BLOB'lar hello göndermeyi destekler, depolama hesabı atanmış.

Bu uzantı, hem Azure dağıtım modelleri ile çalışır.

## <a name="installing-hello-extension-in-your-vm"></a>Merhaba uzantısı VM ile yükleme

Bu uzantı hello Azure PowerShell cmdlet'lerini, Azure CLI komut dosyaları veya Azure dağıtım şablonları kullanarak etkinleştirebilirsiniz. Daha fazla bilgi için bkz: [uzantıları özelliklerinin](./extensions-features.md).

Hello Azure portal kullanılan tooenable veya LAD 3.0 yapılandırma değiştirilemez. Bunun yerine, yükler ve sürüm 2.3 yapılandırır. Azure portal grafikleri ve uyarılar iki sürümünü de hello uzantısı verilerle çalışır.

Bu yükleme yönergeleri ve [indirilebilir örnek yapılandırma](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) LAD 3.0 yapılandırın:

* yakalama ve depolama ölçümler aynı LAD 2.3 tarafından sağlanan gibi hello;
* dosya sistemi ölçümler, yeni tooLAD 3.0 yararlı bir dizi yakalama;
* Yakalama LAD 2.3 ile etkin hello varsayılan syslog toplama;
* Merhaba grafik ve VM ölçümleri uyarmak için Azure portal deneyimi sağlar.

Merhaba indirilebilir yapılandırma yalnızca bir örnektir; toosuit değiştirmek, kendi gereksinimlerinizi.

### <a name="prerequisites"></a>Ön koşullar

* **Azure Linux Aracısı sürüm 2.2.0 veya daha sonra**. Çoğu Azure VM Linux galeri görüntüleri sürüm 2.2.7 dahil etmek veya daha sonra. Çalıştırma `/usr/sbin/waagent -version` tooconfirm hello sürüm hello VM üzerinde yüklü. Merhaba VM hello Konuk aracısının daha eski bir sürümünü çalıştırıyorsa, izleyin [bu yönergeleri](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate onu.
* **Azure CLI**. [Azure CLI 2.0 Hello ayarlamak](https://docs.microsoft.com/cli/azure/install-azure-cli) makinenizde ortamı.
* zaten yoksa wget komutu Hello: çalıştırmak `sudo apt-get install wget`.
* Var olan bir Azure aboneliği ve mevcut bir depolama hesabı içinde toostore hello veri.

### <a name="sample-installation"></a>Örnek yükleme

Merhaba doğru parametreleri hello üzerinde ilk üç satırını doldurun, sonra da kök olarak bu betiği yürütün:

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

Merhaba örnek yapılandırma Hello URL'sini ve içeriğini, konu toochange var. Merhaba portal ayarları JSON dosyasının bir kopyasını indirin ve gereksinimlerinize göre özelleştirin. Tüm Şablonları ya da Otomasyon, oluşturmak, her zaman bu URL'yi indirmek yerine kendi kopyanızı kullanmanız gerekir.

### <a name="updating-hello-extension-settings"></a>Merhaba uzantısı ayarları güncelleştiriliyor

Korumalı veya genel ayarları değiştirdikten sonra bunları toohello VM çalıştırarak dağıtma hello aynı komutu. Herhangi bir şey hello ayarlarını değiştirdiyseniz, güncelleştirilmiş hello ayarları toohello uzantısı gönderilir. LAD hello yapılandırma yeniden yükler ve kendisini yeniden başlatır.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Merhaba uzantısı eski sürümlerinden geçiş

Merhaba uzantısı'nın en son sürüm Hello **3.0**. **Eski sürümlerini (2.x) kullanım dışıdır ve ve 31 Temmuz 2018 sonrasında yayımdan**.

> [!IMPORTANT]
> Bu uzantı hello uzantısı'nın en son değişiklikleri toohello yapılandırma tanıtır. Bu tür bir değişiklik tooimprove hello güvenlik hello uzantısının bulunuldu; Sonuç olarak, geriye dönük uyumluluk 2.x ile korunmasını değil. Ayrıca, bu uzantı için uzantı yayımcı hello hello yayımcı hello 2.x sürümleri için farklıdır.
>
> toomigrate sürümünden 2.x toothis yeni hello uzantısı hello eski uzantısı (altında hello eski Yayımcı adı) ve ardından hello uzantısı 3 sürümünü yükleyin kaldırmanız gerekir.

Öneriler:

* Merhaba uzantı etkin otomatik alt sürüm yükseltme işlemine yükleyin.
  * Merhaba uzantısı Azure XPLAT CLI veya Powershell aracılığıyla yüklüyorsanız, Klasik dağıtım modeli VM'ler, '3.*' hello sürüm olarak belirtin.
  * Sanal makineleri üzerinde Azure Resource Manager dağıtım modeli, dahil ' "olan": true' hello VM Dağıtım şablonu olarak.
* Yeni/farklı bir depolama hesabı LAD 3.0 için kullanın. Bir hesap sorunlu paylaşımı olun birkaç küçük uyumsuzlukları LAD 2.3 LAD 3.0 arasındaki vardır:
  * LAD 3.0 syslog olayları farklı bir ada sahip bir tablo olarak depolar.
  * Merhaba counterSpecifier dizeleri için `builtin` ölçümleri farklı LAD 3. 0 '.

## <a name="protected-settings"></a>Korumalı ayarları

Bu yapılandırma bilgileri kümesi genel görünümünde, örneğin, depolama kimlik korunması gereken hassas bilgiler içerir. Bu ayarları şifreli biçimde hello uzantısı tarafından depolanan iletilen tooand verilmiştir.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

Ad | Değer
---- | -----
storageAccountName | Veri hello uzantısı tarafından yazılmış hello depolama hesabı Hello adı.
storageAccountEndPoint | (isteğe bağlı) hello uç noktası hangi hello depolama hesabı zaten hello bulut tanımlama. Bu ayar olmazsa LAD toohello Azure genel bulutunda, varsayılan olarak `https://core.windows.net`. toouse bir depolama hesabı Azure Almanya, Azure kamu ya da Azure Çin'de, bu değeri uygun şekilde ayarlayın.
storageAccountSasToken | Bir [hesap SAS belirteci](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) Blob ve tablo hizmeti (`ss='bt'`), geçerli toocontainers ve nesneler (`srt='co'`), hangi verir ekleyin, oluşturmak, liste, güncelleştirme ve yazma izinleri (`sp='acluw'`). Yapmak *değil* hello başında soru işareti (?) içerir.
mdsdHttpProxy | (isteğe bağlı) HTTP proxy gerekli bilgileri tooenable hello uzantısı tooconnect toohello belirtilen depolama hesabı ve uç nokta.
sinksConfig | (isteğe bağlı) Alternatif hedefleri toowhich ölçümleri ve olayları ayrıntılarını alınabilir. Merhaba uzantısı tarafından desteklenen her veri havuzu belirli ayrıntılarını Hello izleyen hello bölümlerde açıklanmıştır.

Gerekli hello SAS belirteci hello Azure portal aracılığıyla kolayca oluşturabilirsiniz.

1. Merhaba uzantısı toowrite istediğiniz hello genel amaçlı depolama hesabı toowhich seçin
1. "Hello ayarları bölümünden hello soldaki menüden erişim imzası paylaşılan" seçin
1. Daha önce açıklandığı gibi hello uygun bölümleri olun
1. Merhaba "SAS oluştur" düğmesine tıklayın.

![Görüntü](./media/diagnostic-extension/make_sas.png)

Kopya hello SAS hello storageAccountSasToken alanına oluşturulan; Merhaba başında soru işareti kaldırın ("?").

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

Bu isteğe bağlı bir bölüm toowhich hello uzantısı topladığı hello bilgileri gönderir ek hedefleri tanımlar. Merhaba "havuz" dizi her ek veri havuzu için bir nesne içeriyor. Merhaba diğer öznitelikleri hello nesnesindeki hello "tür" özniteliği belirler.

Öğesi | Değer
------- | -----
ad | Bir dize toorefer toothis havuz hello uzantı yapılandırmasındaki başka bir yerde kullanılır.
type | Havuz tanımlanmakta Hello türü. Diğer değerleri (varsa) hello bu tür durumlarda belirler.

Merhaba Linux tanılama uzantısını 3.0 sürümünü iki havuz türlerini destekler: EventHub ve JsonBlob.

#### <a name="hello-eventhub-sink"></a>Merhaba EventHub havuz

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

Merhaba "sasURL" giriş hello olay hub'ı toowhich veri için SAS belirteci dahil tam URL'yi yayınlanmalıdır hello içeriyor. LAD hello gönderme talep sağlayan bir ilke adlandırma SAS gerektirir. Örnek:

* Adlı bir olay hub'ları ad alanı oluşturma`contosohub`
* Adlı hello ad alanında bir olay hub'ı oluşturma`syslogmsgs`
* Olay Hub'ın adlandırılmış hello üzerinde bir paylaşılan erişim ilkesi oluşturun `writer` etkinleştirir gönderme talep hello

Bir SAS iyi 1 Ocak 2018 gece yarısı UTC kadar oluşturduysanız hello sasURL değeri olabilir:

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Olay hub'ları için SAS belirteci oluşturma hakkında daha fazla bilgi için bkz: [bu web sayfası](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).

#### <a name="hello-jsonblob-sink"></a>Merhaba JsonBlob havuz

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

Veri yönergelerine uygun tooa JsonBlob havuz BLOB'ları Azure depolama alanında depolanır. Her örneği LAD blob her saat için her bir havuz adı oluşturur. Her bir blob her zaman nesne sözdizimsel olarak geçerli bir JSON dizisi içerir. Yeni girişler toohello dizi otomatik olarak eklenir. BLOB'ları bir kapsayıcıda hello hello havuzu olarak aynı ad ile depolanır. BLOB kapsayıcı adları JsonBlob havuzlarını toohello adlarını uygulamak için Azure depolama kuralları hello: küçük harf alfasayısal ASCII karakterler veya tire 3 ile 63 arasında.

## <a name="public-settings"></a>Genel ayarları

Bu yapı çeşitli bloklarını hello uzantısı tarafından toplanan hello bilgiler denetleyen ayarları içerir. Her ayar isteğe bağlıdır. Belirtirseniz `ladCfg`, de belirtmeniz gerekir `StorageAccount`.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

Öğesi | Değer
------- | -----
StorageAccount | Veri hello uzantısı tarafından yazılmış hello depolama hesabı Hello adı. Olmalıdır hello belirtildiği gibi aynı adı hello [ayarların korumalı](#protected-settings).
mdsdHttpProxy | (isteğe bağlı) Merhaba olduğu gibi aynı [ayarların korumalı](#protected-settings). Merhaba ortak değer varsa hello özel değer tarafından geçersiz ayarlayın. Yerleştirin bir Parolada hello gibi bir gizlilik içeren proxy ayarlarını [ayarların korumalı](#protected-settings).

Aşağıdaki bölümlerde hello ayrıntılı Hello kalan öğeleri açıklanmaktadır.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

Bu isteğe bağlı yapısı denetimleri hello toplama ölçümleri ve teslimat toohello Azure ölçümleri hizmeti ve tooother veri günlüklerini iç havuzlar. Ya da belirtmeniz gerekir `performanceCounters` veya `syslogEvents` veya her ikisini de. Merhaba belirtmelisiniz `metrics` yapısı.

Öğesi | Değer
------- | -----
eventVolume | (isteğe bağlı) Denetimleri hello depolama tablo içinde oluşturulan bölüm sayısı hello. Biri olmalıdır `"Large"`, `"Medium"`, veya `"Small"`. Belirtilmezse, hello varsayılan değerdir `"Medium"`.
sampleRateInSeconds | Ham (unaggregated) ölçümleri topluluğu arasındaki (isteğe bağlı) hello varsayılan zaman aralığı. desteklenen hello en küçük örnek hızı 15 saniyedir. Belirtilmezse, hello varsayılan değerdir `15`.

#### <a name="metrics"></a>metrics

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

Öğesi | Değer
------- | -----
resourceId | Hello Azure Resource Manager kaynak kimliği hello VM veya hello sanal makine ölçek VM ait toowhich hello ayarlayın. Bu ayar olmalıdır herhangi JsonBlob havuz hello yapılandırmada kullanılıp kullanılmayacağını da belirtilmiş.
scheduledTransferPeriod | Birleşik ölçümleri toobe olduğu hello sıklığı hesaplanan ve 8601 olduğu zaman aralığı ifade edilen tooAzure ölçümleri, aktarılır. Merhaba en küçük aktarım süresi 60, diğer bir deyişle, PT1M saniyedir. En az bir scheduledTransferPeriod belirtmeniz gerekir.

Merhaba performans sayaçları bölümünde belirtilen ölçümleri 15 dakikada toplanır hello veya hello sayaç için açıkça tanımlanmış hello örnek hızı örnekleri. Birden çok scheduledTransferPeriod sıklıklarını (Merhaba örnekte olduğu gibi) görünüyorsa, her bir toplama bağımsız olarak hesaplanır.

#### <a name="performancecounters"></a>performans sayaçları

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

Bu isteğe bağlı bir bölüm ölçümleri hello koleksiyonunu denetler. Ham örnekleri her biri için toplanmış [scheduledTransferPeriod](#metrics) tooproduce bu değerler:

* Ortalama
* en az
* Maksimum
* Son toplanan değeri
* kullanılan toocompute hello toplam ham örnekleri sayısı

Öğesi | Değer
------- | -----
İç havuzlar | (isteğe bağlı) Adlarının virgülle ayrılmış bir liste iç havuzlar toowhich LAD toplanmış ölçüm sonuçlarını gönderir. Tüm toplanan ölçümler listelenen yayımlanan tooeach havuz ' dir. Bkz: [sinksConfig](#sinksconfig). Örnek: `"EHsink1, myjsonsink"`.
type | Merhaba ölçüsünün Hello gerçek sağlayıcısını tanımlar.
sınıfı | "Sayacı birlikte" Merhaba belirli ölçüm hello sağlayıcının ad alanı içindeki tanımlar.
Sayaç | "Sınıf ile birlikte" Merhaba belirli ölçüm hello sağlayıcının ad alanı içindeki tanımlar.
counterSpecifier | Merhaba belirli ölçüm hello Azure ölçümleri ad alanı içindeki tanımlar.
Koşul | (isteğe bağlı) Bu nesnenin tüm örneklerde toplama seçer hello veya seçer hello nesne toowhich hello ölçüm belirli bir örneği uygular. Daha fazla bilgi için bkz: Merhaba [ `builtin` ölçüm tanımlarını](#metrics-supported-by-builtin).
sampleRate | Bu ölçüm için ham örnek toplanan hello oranı ayarlar 8601 aralığı BELİRTİR. Ayarlanmadı, hello toplama aralığı başlangıç değeri olarak ayarlanmış olup olmadığını [sampleRateInSeconds](#ladcfg). Merhaba kısa desteklenen örnek hızı 15 saniye (PT15S) kullanılır.
Birim | Bu dizeler biri olmalıdır: "Count", "Bayt sayısı", "Saniye", "Yüzde", "CountPerSecond", "BytesPerSecond", "Milisaniyelik". Merhaba ölçüm için Hello birimi tanımlar. Merhaba, bu birim veri değerleri toomatch toplanan hello toplanan veri tüketicileri bekler. Bu alan LAD yoksayar.
Görünen adı | Merhaba etiketinde (Merhaba ilişkili yerel ayarı tarafından belirtilen hello dili) toobe Azure ölçümleri toothis verilerde bağlı. Bu alan LAD yoksayar.

Merhaba counterSpecifier rasgele bir tanımlayıcıdır. Azure portal grafik ve özelliği, uyarı hello gibi ölçümleri tüketicilerinin counterSpecifier "bir ölçüm veya bir ölçüm örneğini tanımlayan anahtarı" Merhaba kullanın. İçin `builtin` ölçümleri, öneririz ile başlayan counterSpecifier değerleri kullandığınız `/builtin/`. Ölçüm belirli bir örneği topluyorsanız hello örneği toohello counterSpecifier değerini hello tanıtıcısı ekleme öneririz. Bazı örnekler:

* `/builtin/Processor/PercentIdleTime`-Tüm çekirdek arasında ortalaması boşta kalma süresi
* `/builtin/Disk/FreeSpace(/mnt)`-Merhaba /mnt filesystem boş alan
* `/builtin/Disk/FreeSpace`-Boş alan tüm takılı bağlanan dosya sistemlerinin ortalaması

LAD ne hello Azure portal hello counterSpecifier değeri toomatch herhangi düzeni bekliyor. CounterSpecifier değerleri nasıl oluşturmak tutarlı olması.

Belirttiğinizde `performanceCounters`, LAD her zaman Azure depolama alanında veri tooa tablosu yazar. Siz sahip hello aynı tooJSON blobları ve/veya olay hub'ları yazılan veriler, ancak depolama veri tooa tablosu devre dışı bırakılamıyor. Merhaba tanılama uzantı yapılandırılmamış toouse tüm örnekleri aynı depolama hesabı adı ve uç nokta Ekle kendi ölçümleri ve günlükleri toohello hello aynı tablo. Çok fazla sayıda sanal makineleri yazıyorsanız aynı tablo bölümleme, Azure daraltabilir toohello toothat bölüm yazar. Merhaba eventVolume nedenler girişleri toobe ayarı 1 (küçük), 10 (Orta) ya da 100 (büyük) farklı bölümleri arasında yayılır. Genellikle, "Orta" yeterli tooensure trafiğinin azaltılacağı değil. hello Azure portal Hello Azure ölçümleri özelliği bu tablo tooproduce grafikleri veya tootrigger uyarıları hello verileri kullanır. Bu dizeler hello birleşimini Hello tablo adıdır:

* `WADMetrics`
* Merhaba tablosunda depolanan değerleri Hello "scheduledTransferPeriod" Merhaba için bir araya getirilir
* `P10DV2S`
* 10 günde değişiklikleri "YYYYAAGG" Merhaba formunda bir tarih

Örnekler `WADMetricsPT1HP10DV2S20170410` ve `WADMetricsPT1MP10DV2S20170609`.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

Bu isteğe bağlı bir bölüm syslog günlük olayları hello koleksiyonunu denetler. Merhaba bölüm atlanırsa, syslog olayları hiç yakalanmaz.

Merhaba syslogEventConfiguration koleksiyonun her syslog özelliğini ilgi için bir girişi yok. MinSeverity belirli olanağı için "hiçbiri", veya bu tesis hello öğesinde hiç görünmüyorsa, bu tesis hiçbir olaylarından yakalanır.

Öğesi | Değer
------- | -----
İç havuzlar | Adlarının virgülle ayrılmış bir liste iç havuzlar toowhich ayrı günlük olayları yayımlanır. SyslogEventConfiguration Hello kısıtlamaları eşleşen tüm günlük listelenen yayımlanan tooeach havuz olaylardır. Örnek: "EHforsyslog"
facilityName | Bir syslog tesis adı (gibi "günlük\_kullanıcı" veya "günlük\_LOCAL0"). Merhaba Hello "özelliği" bölümüne bakın [syslog adam sayfa](http://man7.org/linux/man-pages/man3/syslog.3.html) hello tam listesi için.
minSeverity | Bir syslog önem düzeyi (gibi "günlük\_hata" veya "günlük\_bilgileri"). Merhaba Hello "düzeyi" bölümüne bakın [syslog adam sayfa](http://man7.org/linux/man-pages/man3/syslog.3.html) hello tam listesi için. Merhaba uzantısı gönderilen olaylar toohello olanağı yakalar veya düzeyi hello belirtilen.

Belirttiğinizde `syslogEvents`, LAD her zaman Azure depolama alanında veri tooa tablosu yazar. Siz sahip hello aynı tooJSON blobları ve/veya olay hub'ları yazılan veriler, ancak depolama veri tooa tablosu devre dışı bırakılamıyor. Bu tablo için davranış bölümleme hello aynı için açıklandığı gibi hello olduğu `performanceCounters`. Bu dizeler hello birleşimini Hello tablo adıdır:

* `LinuxSyslog`
* 10 günde değişiklikleri "YYYYAAGG" Merhaba formunda bir tarih

Örnekler `LinuxSyslog20170410` ve `LinuxSyslog20170609`.

### <a name="perfcfg"></a>perfCfg

Bu isteğe bağlı bir bölüm rasgele yürütülmesi denetimleri [OMI](https://github.com/Microsoft/omi) sorgular.

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

Öğesi | Değer
------- | -----
Namespace | (isteğe bağlı) hello OMI ad alanı içinde hangi hello sorgu yürütülmelidir. Belirtilmezse, "kök/hello tarafından uygulanan scx", hello varsayılan değer olan [System Center platformlar arası sağlayıcıları](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).
sorgu | Merhaba OMI sorgu toobe yürütülür.
Tablo | Depolama hesabı belirlenmiş hello de (isteğe bağlı) hello Azure depolama tablosunda (bkz [ayarların korumalı](#protected-settings)).
frequency | (isteğe bağlı) hello hello sorgunun yürütülmesi, arasındaki saniye sayısı. 300 (5 dakika); varsayılan değer: en düşük değer 15 saniyedir.
İç havuzlar | (isteğe bağlı) Ek havuzlarını toowhich ham örnek ölçüm sonuçlarını adlarının virgülle ayrılmış bir liste yayımlanması gerekir. Bu ham örnekleri toplama yok veya Azure ölçümleri hello uzantısı tarafından hesaplanır.

"Tablo" veya "İç havuzlar" ya da her ikisini de belirtilmesi gerekir.

### <a name="filelogs"></a>fileLogs

Denetimleri hello günlük dosyalarının yakalayın. LAD toohello dosyası yazılırken yeni metin satırlarını yakalar ve tootable satırları ve/veya belirtilen tüm havuzlarını (JsonBlob veya EventHub) yazar.

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

Öğesi | Değer
------- | -----
Dosya | Merhaba günlük dosyası toobe tam yol adı Hello izlenen ve yakalanan. Merhaba pathname tek bir dosya adı olmalıdır; bir dizin adı veya joker karakterler içeriyor.
Tablo | (isteğe bağlı) hello Azure depolama tablosunda belirtilen hello depolama hesabı (belirtildiği şekilde korumalı hello yapılandırmasında), hangi yeni satırlarına hello "Merhaba dosyasının kuyruk" yazılır.
İç havuzlar | (isteğe bağlı) Ek havuzlarını toowhich günlük satırları adlarının virgülle ayrılmış bir liste gönderdi.

"Tablo" veya "İç havuzlar" ya da her ikisini de belirtilmesi gerekir.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Merhaba yerleşik sağlayıcı tarafından desteklenen ölçümleri

Merhaba yerleşik ölçüm ölçümleri en ilginç tooa geniş kullanıcı kümesi için kaynak sağlayıcıdır. Bu ölçümler beş geniş sınıflara ayrılır:

* İşlemci
* Bellek
* Ağ
* Dosya sistemi
* Disk

### <a name="builtin-metrics-for-hello-processor-class"></a>Merhaba işlemci sınıfı için yerleşik ölçümleri

Merhaba ölçümleri işlemci sınıfının hello VM işlemci kullanımı hakkında bilgi sağlar. Yüzdeleri toplanırken hello hello ortalama tüm CPU'lar arasında sonucudur. Bir iki çekirdek VM, bir çekirdek % 100 meşgul ve % 100 boşta hello diğer şeklindeydi hello PercentIdleTime 50 olur bildirilen. Her çekirdek % 50 meşgul ise aynı hello dönem sonuç 50 de olacaktır hello bildirdi. Bir dört çekirdek VM, bir çekirdek % 100 meşgul ve hello boşta, diğerleri hello PercentIdleTime 75 olacaktır bildirdi.

Sayaç | Anlamı
------- | -------
PercentIdleTime | İşlemci hello çekirdek boşta döngü yürütülmekte hello toplama penceresi sırasında zamanı yüzdesi
percentProcessorTime | Boş olmayan bir iş parçacığı yürütme zamanı yüzdesi
PercentIOWaitTime | G/ç işlemleri toocomplete için beklerken zaman yüzdesi
PercentInterruptTime | Donanım/yazılım kesmeler ve DPC'ler (ertelenmiş yordam çağrılarını) yürütme zamanı yüzdesi
PercentUserTime | Boş olmayan süresini hello toplama penceresi sırasında hello zamanın normal öncelik en fazla kullanıcı yüzdesi
PercentNiceTime | Boş olmayan süresini alçaltılmış (iyi) öncelikli harcanan yüzdeyle hello
PercentPrivilegedTime | Boş olmayan süresini ayrıcalıklı (çekirdek) modda harcanan yüzdeyle hello

Merhaba bir too100% en ilk dört sayaçları sum. Merhaba son üç ayrıca toplam too100% sayaçları; Bunlar PercentProcessorTime, PercentIOWaitTime ve PercentInterruptTime hello toplamını ayırabilir.

tek bir ölçüm toplanan tüm işlemciler arasında tooobtain ayarlamak `"condition": "IsAggregate=TRUE"`. İkinci mantıksal işlemciye bir dört hello çekirdek VM olarak tooobtain belirli bir işlemci için bir ölçüm ayarlamak `"condition": "Name=\\"1\\""`. Mantıksal işlemci numaralarıdır hello aralığında `[0..n-1]`.

### <a name="builtin-metrics-for-hello-memory-class"></a>Merhaba bellek sınıfı için yerleşik ölçümleri

Merhaba ölçümleri sınıfının bellek disk belleği ve değiştirmeyi bellek kullanımı hakkında bilgi sağlar.

Sayaç | Anlamı
------- | -------
AvailableMemory | MIB kullanılabilir fiziksel bellek
PercentAvailableMemory | Kullanılabilir fiziksel belleğin toplam bellek yüzdesi
UsedMemory | Kullanımda fiziksel bellek (MIB)
PercentUsedMemory | Kullanımdaki fiziksel belleğin toplam bellek yüzdesi
PagesPerSec | Toplam disk belleği (okuma/yazma)
PagesReadPerSec | Depolama (takas dosyası, program dosyası, eşlenmiş dosya, vb.) yedekleme sayfaları oku
PagesWrittenPerSec | Toobacking yazılan sayfa depolamak (takas dosyası, eşlenmiş dosya, vb.)
AvailableSwap | Kullanılmayan takas alanı (MIB)
PercentAvailableSwap | Kullanılmayan değiştirme alanının toplam değiştirme yüzdesi
UsedSwap | Kullanımda takas alanı (MIB)
PercentUsedSwap | Değiştirme alanının toplam değiştirme yüzdesi olarak kullanımda

Bu sınıf ölçümleri yalnızca tek bir örneği vardır. Merhaba "koşul" özniteliği yok yararlı ayarlara sahip ve alınmamalıdır.

### <a name="builtin-metrics-for-hello-network-class"></a>Merhaba ağ sınıfı için yerleşik ölçümleri

Hello ölçümleri ağ sınıfı önyüklemeden tek tek ağ arabirimleri üzerinde ağ etkinliği hakkında bilgi sağlar. LAD ana ölçümleri alınabilir bant genişliği ölçümleri kullanıma sunmuyor.

Sayaç | Anlamı
------- | -------
BytesTransmitted | Önyüklemeden gönderilen toplam bayt sayısı
BytesReceived | Önyüklemeden alınan toplam bayt sayısı
BytesTotal | Gönderilen veya alınan önyüklemeden toplam bayt sayısı
PacketsTransmitted | Önyüklemeden gönderilen toplam paket sayısı
PacketsReceived | Önyüklemeden alınan toplam paket sayısı
TotalRxErrors | Sayısı önyüklemeden hataları alırsınız
TotalTxErrors | Sayısı önyüklemeden iletme işlemi hataları
TotalCollisions | Çakışmaları önyüklemeden hello ağ bağlantı noktaları tarafından bildirilen sayısı

 Bu sınıf instanced rağmen LAD tüm ağ aygıtlarını toplanan yakalama ağ ölçümleri desteklemez. eth0 gibi belirli bir arabirim için tooobtain hello ölçümleri ayarlamak `"condition": "InstanceID=\\"eth0\\""`.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>Merhaba Filesystem sınıfı için yerleşik ölçümleri

Merhaba ölçümleri Filesystem sınıfının filesystem kullanımı hakkında bilgi sağlar. Mutlak ve yüzde değerleri, görüntülenen tooan normal kullanıcı (kök değil) olduğu raporlanır.

Sayaç | Anlamı
------- | -------
FreeSpace | Bayt cinsinden kullanılabilir disk alanı
UsedSpace | Kullanılan disk alanı bayt
PercentFreeSpace | Boş alan yüzdesi
PercentUsedSpace | Kullanılan yüzde alanı
PercentFreeInodes | Kullanılmayan inode yüzdesi
PercentUsedInodes | Tüm bağlanan dosya sistemlerinin arasında toplamı (kullanımda) ayrılmış inode yüzdesi
BytesReadPerSecond | Saniye başına okunan bayt
BytesWrittenPerSecond | Saniye başına yazılan bayt
BytesPerSecond | Okunan veya saniye başına yazılan bayt sayısı
ReadsPerSecond | Saniye başına okuma işlemleri
WritesPerSecond | Saniye başına işlem yazma
TransfersPerSecond | Saniye başına okuma veya yazma işlemi

Tüm dosya sistemleri arasında toplanmış değerler elde edilebilir ayarlayarak `"condition": "IsAggregate=True"`. Belirli bağlı dosya sistemi için aşağıdaki gibi değerler "/ mnt", ayarlayarak elde `"condition": 'Name="/mnt"'`.

### <a name="builtin-metrics-for-hello-disk-class"></a>Merhaba Disk sınıfı için yerleşik ölçümleri

Merhaba ölçümleri Disk sınıfının disk Aygıt kullanımı hakkında bilgi sağlar. Bu istatistikler sürücünün tamamını toohello uygulayın. Bir cihazda birden çok dosya sistemleri varsa, bu aygıt için hello sayaçları, etkili bir şekilde, bunların tümünün toplanan var.

Sayaç | Anlamı
------- | -------
ReadsPerSecond | Saniye başına okuma işlemleri
WritesPerSecond | Saniye başına işlem yazma
TransfersPerSecond | Saniye başına toplam işlem
AverageReadTime | Okuma işlemi başına ortalama saniye
AverageWriteTime | Yazma işlemi başına ortalama saniye
AverageTransferTime | İşlem başına ortalama saniye
AverageDiskQueueLength | Sıraya alınan disk işlemleri ortalama sayısı
ReadBytesPerSecond | Saniye başına okunan bayt sayısı
WriteBytesPerSecond | Saniye başına yazılan bayt sayısı
BytesPerSecond | Okunan veya saniye başına yazılan bayt sayısı

Tüm diskler boyunca toplanan değerler elde edilebilir ayarlayarak `"condition": "IsAggregate=True"`. tooget bilgilerini (örneğin, / dev/sdf1), belirli bir aygıt için `"condition": "Name=\\"/dev/sdf1\\""`.

## <a name="installing-and-configuring-lad-30-via-cli"></a>Yükleme ve LAD 3.0 CLI üzerinden yapılandırma

Korumalı ayarlarınızı PrivateConfig.json hello dosyasında ve genel yapılandırma bilgilerinizi PublicConfig.json varsayılarak, şu komutu çalıştırın:

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

Merhaba komutu hello Azure CLI hello Azure kaynak yönetimi modu (arm) kullandığınızı varsayar. Klasik dağıtım için tooconfigure LAD (ASM) VM'ler model, çok geçiş "asm" modu (`azure config mode asm`) ve hello kaynak grubu adı hello komutta atlayın. Daha fazla bilgi için bkz: Merhaba [platformlar arası CLI belgelerine](https://docs.microsoft.com/azure/xplat-cli-connect).

## <a name="an-example-lad-30-configuration"></a>Bir örnek LAD 3.0 yapılandırma

Tanımları, burada ait bir örnek LAD 3.0 uzantısı yapılandırması bazı açıklama ile önceki hello temel. tooapply Bu örnek tooyour durumda, kendi depolama hesabı adı kullanın, hesap SAS belirteci ve EventHubs SAS belirteçleri.

### <a name="privateconfigjson"></a>PrivateConfig.json

Bu özel ayarları yapılandırın:

* bir depolama hesabı
* eşleşen hesap SAS belirteci
* birkaç havuzlarını (JsonBlob veya EventHubs SAS belirteci ile)

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

Bu genel ayarları için LAD neden:

* Yüzde işlemci zamanı ve kullanılan disk alanı ölçümleri toohello karşıya `WADMetrics*` tablosu
* Syslog tesis "kullanıcı" ve önem derecesi "bilgi" toohello iletilerden karşıya `LinuxSyslog*` tablosu
* Adlı ham OMI sorgu sonuçları (PercentProcessorTime ve PercentIdleTime) toohello karşıya `LinuxCPU` tablosu
* Dosyasına eklenen satır karşıya `/var/log/myladtestlog` toohello `MyLadTestLog` tablo

Her durumda için veri yüklenir:

* Azure Blob storage (kapsayıcı adı: Merhaba JsonBlob havuzunda tanımlandığı gibi)
* EventHubs uç noktası (Merhaba EventHubs havuzunda belirtildiği şekilde)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

Merhaba `resourceId` hello hello VM veya hello sanal makine ölçek kümesi yapılandırma eşleşmelidir.

* Grafik ve uyarı azure platformu ölçümleri hello ResourceId hello üzerinde çalıştığınız VM, bilir. Toofind hello veri hello ResourceId hello arama anahtarı kullanarak, VM için bekler.
* Azure otomatik ölçeklendirme kullanırsanız, hello ResourceId hello otomatik ölçeklendirme yapılandırmasında LAD tarafından kullanılan hello ResourceId eşleşmesi gerekir.
* Merhaba ResourceId LAD tarafından yazılan JsonBlobs hello adlarını içinde yerleşik olarak bulunur.

## <a name="view-your-data"></a>Verilerinizi görüntüleme

Hello Azure portal tooview performans verileri kullanma veya Uyarıları ayarlayın:

![Görüntü](./media/diagnostic-extension/graph_metrics.png)

Merhaba `performanceCounters` verileri her zaman bir Azure Storage tablosunda depolanır. Azure depolama API'leri, birçok diller ve platformlar için kullanılabilir.

TooJsonBlob havuzlarını gönderilen veriler hello adlı hello depolama hesabındaki BLOB depolanır [ayarların korumalı](#protected-settings). Tüm Azure Blob Depolama API'leri kullanılarak hello blob verileri kullanabilir.

Ayrıca, bu kullanıcı Arabirimi araçlarını tooaccess hello verileri Azure depolama alanında kullanabilirsiniz:

* Visual Studio Sunucu Gezgini.
* [Microsoft Azure Storage Gezgini](https://azurestorageexplorer.codeplex.com/ "Azure Storage Gezgini").

Bu oturumunun anlık görüntüsü, bir Microsoft Azure Storage Gezgini hello Azure Storage tablolarının ve kapsayıcıları test VM üzerinde doğru şekilde yapılandırılmış bir LAD 3.0 uzantısı üretilen gösterir. Merhaba görüntü hello ile tam olarak eşleşmiyor [örnek LAD 3.0 yapılandırma](#an-example-lad-30-configuration).

![Görüntü](./media/diagnostic-extension/stg_explorer.png)

Hello ilgili bkz [EventHubs belgelerine](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn nasıl tooconsume iletileri tooan EventHubs endpoint yayımlandı.

## <a name="next-steps"></a>Sonraki adımlar

* Ölçüm uyarıları oluşturma [Azure İzleyici](../../monitoring-and-diagnostics/insights-alerts-portal.md) topladığınız hello ölçümünün.
* Oluşturma [izleme grafikleri](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) ölçümlerinizi için.
* Nasıl çok öğrenin[bir sanal makine ölçek kümesi oluşturma](/azure/virtual-machines/linux/tutorial-create-vmss) , ölçümleri toocontrol otomatik ölçeklendirmeyi kullanma.
