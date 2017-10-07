---
title: "Windows mağazası uygulamalarında Azure depolama aaaUse | Microsoft Docs"
description: "Nasıl toocreate bir Windows mağazası öğrenin Azure Blob, kuyruk, tablo veya dosya depolama kullanan uygulama."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>Nasıl Windows mağazası uygulamalarında toouse Azure depolama
## <a name="overview"></a>Genel Bakış
Bu kılavuz Azure Storage kullanır bir Windows mağazası uygulaması geliştirme ile tooget nasıl başlatılacağını gösterir.

## <a name="download-required-tools"></a>Gerekli araçları yükleyin
* [Visual Studio](https://www.visualstudio.com/downloads/) kolay toobuild kolaylaştırır hata ayıklama, yerelleştirme, paketini ve Windows mağazası uygulamaları dağıtın. Visual Studio 2012 veya üzeri gereklidir.
* Merhaba [Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage) Azure Storage ile çalışmak için bir Windows çalışma zamanı sınıf kitaplığı sağlar.
* [Windows mağazası uygulamaları için WCF Veri Hizmetleri Araçları](http://www.microsoft.com/download/details.aspx?id=30714) hello hizmet Başvurusu Ekle deneyimi Visual Studio'daki Windows mağazası uygulamaları için istemci tarafı OData desteği ile genişletir.

## <a name="develop-apps"></a>Uygulamaları geliştirme
### <a name="getting-ready"></a>Hazırlanma
Yeni bir Windows mağazası uygulama projesi Visual Studio 2012 veya sonraki sürümlerde oluşturun:

![Depolama-apps-depolama-vs-proje][store-apps-storage-vs-project]

Ardından sağ tıklayarak bir başvuru toohello Azure Storage istemci kitaplığı ekleyin **başvuruları**a **Başvuru Ekle**ve Windows Runtime için depolama istemci kitaplığı toohello göz atma, yüklenen:

![Depolama-uygulamalar-storage--kitaplığını seçin][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>Merhaba Blob ile Merhaba kitaplığını ve kuyruk Hizmetleri kullanma
Bu noktada, uygulamanız hazır toocall hello Azure Blob ve kuyruk Hizmetleri ' dir. Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri böylece Azure depolama türlerini doğrudan başvurulabilir:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Ardından, bir düğme tooyour sayfa ekleyin. Kod tooits aşağıdaki hello eklemek **tıklatın** olay ve hello kullanarak, olay işleyicisi yöntemi değiştirme [async anahtar sözcüğü](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

Bu kod iki dize değişkenleri olduğunu varsayar *accountName* ve *accountKey*. Bunlar, bu hesapla ilişkili depolama hesabı ve hello hesap anahtarınızı hello adını temsil eder.

Derleme ve hello uygulamayı çalıştırın. Merhaba düğmesi tıklatıldığında, bir kapsayıcı adlı olup olmadığını denetleyin *container1* hesabınızda var ve ardından değilse oluşturun.

### <a name="using-hello-library-with-hello-table-service"></a>Merhaba tablo hizmeti ile Merhaba kitaplığı kullanma
WCF Veri Hizmetleri hello Windows mağazası uygulama kitaplığı için kullanılan toocommunicate hello Azure Table hizmetiyle olan türlerini bağlıdır. Ardından, Paket Yöneticisi konsolu kullanılarak WCF kitaplıkları hello başvuru toohello gerekli ekleyin:

![Mağaza-apps-depolama-Paket-Yöneticisi][store-apps-storage-package-manager]

Komut toopoint Paket Yöneticisi toohello konumu makinenizde aşağıdaki hello kullan:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

Bu komut tüm gerekli başvuruları tooyour proje otomatik olarak ekler. Toouse istemiyorsanız, Paket Yöneticisi konsolu Merhaba, paket kaynaklarını, LocalMachine toohello listenizde hello WCF Veri Hizmetleri NuGet klasör ekleyin ve ardından açıklandığı gibi hello kullanıcı Arabirimi aracılığıyla hello başvurusu ekleyin [yönetme NuGet paketlerini kullanma Merhaba iletişim](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

Merhaba WCF Veri Hizmetleri NuGet paketi başvurduğunda, düğmenin hello kodda değişiklik **tıklatın** olay:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Bu kod adlı bir tablo olup olmadığını denetler *tablo1* hesabınızda var ve yoksa oluşturur.

Aynı yüklediğiniz paketini hello kullanılabilir olduğu bir başvuru tooMicrosoft.WindowsAzure.Storage.Table.dll de ekleyebilirsiniz. Bu kitaplık yansıma tabanlı seri hale getirme ve genel sorgular gibi ek işlevler içerir. Bu kitaplık JavaScript'i desteklemiyor unutmayın.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
