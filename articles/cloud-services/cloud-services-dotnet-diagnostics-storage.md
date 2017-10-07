---
title: "aaaStore ve görünüm tanılama verilerini Azure storage'da | Microsoft Docs"
description: "Azure Tanılama verileri Azure depolama alanına almak ve görüntüleme"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>Azure Storage deposu ve görünüm Tanılama verileri
Toohello Microsoft Azure storage öykünücüsü veya tooAzure depolama aktarım sürece Tanılama verileri kalıcı olarak depolanmaz. Bir kez depolama biriminde, onu birkaç kullanılabilen araçlar biriyle görüntülenebilir.

## <a name="specify-a-storage-account"></a>Bir depolama hesabı belirtin
Merhaba ServiceConfiguration.cscfg dosyasında toouse istediğiniz hello depolama hesabı belirtin. Merhaba hesap bilgileri, bir bağlantı dizesi bir yapılandırma ayarı olarak tanımlanır. Merhaba aşağıdaki örnek Visual Studio'da yeni bir bulut hizmeti projesi için oluşturulan hello varsayılan bağlantı dizesini gösterir:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

Bir Azure depolama hesabı için bu bağlantı dizesi tooprovide hesap bilgilerini değiştirebilirsiniz.

Toplanacak tanılama veri Hello türüne bağlı olarak, Azure tanılama hello Blob hizmeti veya hello tablo hizmeti kullanır. Merhaba aşağıdaki tabloda kalıcı hello veri kaynaklarını ve bunların biçimi gösterir.

| Veri kaynağı | Depolama biçimi |
| --- | --- |
| Azure günlükleri |Tablo |
| IIS 7.0 günlükleri |Blob |
| Azure tanılama altyapı günlükleri |Tablo |
| Başarısız istek izleme günlükleri |Blob |
| Windows olay günlükleri |Tablo |
| Performans sayaçları |Tablo |
| Kilitlenme bilgi dökümleri |Blob |
| Özel hata günlükleri |Blob |

## <a name="transfer-diagnostic-data"></a>Tanılama veri aktarımı girişi
SDK 2.5 ve sonrası hello istek tootransfer Tanılama verileri hello yapılandırma dosyası aracılığıyla ortaya çıkabilir. Merhaba yapılandırmasında belirtilen zamanlanan aralıklarla tanılama veri aktarın.

SDK 2.4 ve önceki tootransfer hello tanılama verilerini de hello yapılandırma dosyası aracılığıyla programlı olarak isteyebilir. Merhaba programlı yaklaşım da toodo isteğe bağlı aktarımları sağlar.

> [!IMPORTANT]
> Tanılama veri tooan Azure depolama hesabı aktardığınızda, tanılama verilerini kullanan hello depolama alanı kaynakları için ücrete neden.
> 
> 

## <a name="store-diagnostic-data"></a>Tanılama verileri depola
Günlük verileri adlarından hello ile Blob veya tablo depolama alanına depolanır:

**Tabloları**

* **WadLogsTable** - hello İzleme dinleyicisi kullanarak kod içinde yazılmış günlükleri.
* **WADDiagnosticInfrastructureLogsTable** -Tanılama izleme ve yapılandırma değişikliklerini.
* **WADDirectoriesTable** – izleme bu hello tanı İzleyicisi dizinleri.  Bu, IIS günlüklerini içerir, IIS istek günlüklerini ve özel dizinleri başarısız oldu.  Merhaba hello blob günlük dosyasının konumunu hello kapsayıcı alanında belirtilen ve hello hello blob hello RelativePath alanında adıdır.  hello Azure sanal makinesi üzerinde var gibi hello AbsolutePath alan hello konumunu ve hello dosya adını belirtir.
* **WADPerformanceCountersTable** – performans sayaçları.
* **WADWindowsEventLogsTable** – Windows olayı günlüğe kaydeder.

**Bloblar**

* **wad denetimi kapsayıcısı** – (yalnızca SDK 2.4 ve önceki) hello Azure tanılama denetimleri hello XML yapılandırma dosyalarını içerir.
* **wad IIS failedreqlogfiles** – IIS isteği başarısız oldu günlüklerdeki bilgiler içerir.
* **wad IIS logfiles** – IIS günlüklerini hakkında bilgiler içerir.
* **"özel"** – özel bir kapsayıcı dayalı hello tanı İzleyicisi tarafından izlenen dizinleri yapılandırma.  Bu blob kapsayıcısının Hello adı WADDirectoriesTable belirtilir.

## <a name="tools-tooview-diagnostic-data"></a>Araçlar tooview Tanılama verileri
Aktarılan toostorage tamamlandıktan sonra birkaç kullanılabilir tooview hello veri araçlardır. Örneğin:

* Visual Studio - server Explorer'da hello Azure Araçları için Microsoft Visual Studio, yüklü değilse, Azure depolama hesaplarından Sunucu Gezgini tooview salt okunur blob ve tablo verilerinizi hello Azure Storage düğümünü kullanabilirsiniz. Yerel depolama öykünücüsü hesabınızdan verileri görüntüleyebilir ve ayrıca depolama hesaplarından Azure için oluşturduğunuz. Daha fazla bilgi için bkz: [gözatma ve Sunucu Gezgini ile depolama kaynaklarını yönetme](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).
* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, OSX ve Linux Azure Storage verilerle tooeasily çalışma sağlayan bir tek başına uygulamadır.
* [Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) tooview, sağlayan Azure tanılama Manager içerir indirmek ve Azure üzerinde çalışan hello uygulamalar tarafından toplanan hello Tanılama verileri yönetmek.

## <a name="next-steps"></a>Sonraki Adımlar
[Bulut Hizmetleri uygulaması Azure Tanılama ile Merhaba akışı izleme](cloud-services-dotnet-diagnostics-trace-flow.md)

