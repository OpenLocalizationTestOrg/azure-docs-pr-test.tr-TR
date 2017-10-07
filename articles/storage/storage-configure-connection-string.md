---
title: "Azure depolama için bir bağlantı dizesi aaaConfigure | Microsoft Docs"
description: "Bir Azure depolama hesabı için bir bağlantı dizesi yapılandırın. Bir bağlantı dizesi tooauthenticate tooa depolama hesabı uygulamanızdan çalışma zamanında gereken erişim hello bilgiler içerir."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a>Azure Storage bağlantı dizelerini yapılandırma

Bir bağlantı dizesi uygulama tooaccess verilerinizi çalışma zamanında bir Azure depolama hesabı için gerekli hello kimlik doğrulama bilgilerini içerir. Bağlantı dizeleri için yapılandırabilirsiniz:

* Toohello Azure storage öykünücüsü bağlayın.
* Azure depolama hesabı erişim.
* Paylaşılan erişim imzası (SAS) aracılığıyla Azure içinde belirtilen kaynaklara erişir.

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>Bağlantı dizenizi depolanması
Uygulamanızı tooaccess hello bağlantı dizesi çalışma zamanı tooauthenticate yapılan istekleri tooAzure depolama konumunda gerekir. Bağlantı dizenizi depolamak için birkaç seçeneğiniz vardır:

* Çalışan hello Masaüstü veya bir aygıtta bir uygulama hello bağlantı dizesinde depolayabilir bir **app.config** veya **web.config** dosya. Merhaba bağlantı dizesi toohello ekleme **AppSettings** bu dosyaları bölümünde.
* Bir Azure bulut hizmetindeki çalışan bir uygulama hello bağlantı dizesi hello depolayabilir [Azure hizmet yapılandırma (.cscfg) şema dosyası](https://msdn.microsoft.com/library/ee758710.aspx). Merhaba bağlantı dizesi toohello ekleme **ConfigurationSettings** hello hizmet yapılandırma dosyasının.
* Bağlantı dizenizi doğrudan kodunuzda kullanabilirsiniz. Ancak, çoğu senaryoda yapılandırma dosyasında bağlantı dizenizi depolamanız önerilir.

Bağlantı dizenizi bir yapılandırma dosyasında depolanması, bu kolay tooupdate hello bağlantı dizesi tooswitch hello depolama öykünücüsü Azure storage hesabı arasındaki hello bulutta sağlar. Yalnızca tooedit hello bağlantı dizesi toopoint tooyour hedef ortam gerekir.

Merhaba kullanabilirsiniz [Microsoft Azure Yapılandırma Yöneticisi](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) , bağlantı dizesi, uygulamanızın nerede çalıştığına bakmaksızın çalışma zamanında tooaccess.

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>Merhaba depolama öykünücüsü için bağlantı dizesi oluştur
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Merhaba depolama öykünücüsü hakkında daha fazla bilgi için bkz: [geliştirme ve test amacıyla hello Azure storage öykünücüsünü kullanma](storage-use-emulator.md).

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>Bir Azure depolama hesabı için bir bağlantı dizesi oluşturma
Azure depolama hesabınız için bir bağlantı dizesi toocreate, kullanım hello aşağıdaki biçimi. (Önerilen) HTTPS üzerinden tooconnect toohello depolama hesabı isteyip istemediğiniz veya HTTP belirtmek, yerine `myAccountName` hello adlı depolama hesabı ve Değiştir `myAccountKey` hesabının erişim anahtarı ile:

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

Örneğin, bağlantı dizenizi benzer şekilde görünebilir:

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

Azure Storage HTTP ve HTTPS bağlantı dizesinde desteklemesine rağmen *HTTPS tavsiye*.

> [!TIP]
> Depolama hesabınızın bağlantı dizeleri hello bulabilirsiniz [Azure portal](https://portal.azure.com). Çok gidin**ayarları** > **erişim anahtarları** depolama hesabınızın menü dikey toosee bağlantı dizelerinde her iki birincil ve ikincil erişim anahtarı.
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>Paylaşılan erişim imzası kullanarak bir bağlantı dizesi oluşturma
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>Bir açık depolama uç nokta için bir bağlantı dizesi oluşturma
Merhaba varsayılan uç noktaları kullanmak yerine, bağlantı dizesinde açık hizmet uç noktaları belirtin. toocreate açık bir uç nokta belirten bir bağlantı dizesi biçimi aşağıdaki hello hello protokolü belirtimi (HTTPS (önerilen) veya HTTP) dahil olmak üzere her hizmet için hello tüm hizmet uç noktası belirtin:

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

Blob storage uç nokta tooa eşlenen nerede istediğiniz toospecify açık bir uç nokta bir senaryo olduğunda [özel etki alanı](storage-custom-domain-name.md). Bu durumda, bağlantı dizenizi Blob storage için özel uç noktanızı belirtebilirsiniz. Uygulamanız bunları kullanıyorsa diğer hizmetler hello için hello varsayılan uç noktalar isteğe bağlı olarak belirtebilirsiniz.

Burada, hello Blob hizmeti için açık bir uç nokta belirten bir bağlantı dizesi örneği verilmiştir:

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

Bu örnek hello Blob hizmeti için özel bir etki alanı dahil olmak üzere tüm hizmetleri için açık uç nokta belirtir:

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

Merhaba uç değerler bağlantı dizesinde kullanılan tooconstruct hello isteği URI'ler toohello depolama hizmetleri ve tooyour kodu döndürdü URI'ler hello biçiminde dikte.

Depolama uç nokta tooa özel bir etki alanı eşlenen ve bu uç bağlantı dizesinden mümkün toouse olmaz atlayın Bu bağlantı o hizmet kodunuzdan tooaccess verileri dize.

> [!IMPORTANT]
> Hizmet uç noktası değerleri bağlantı dizelerinizi doğru biçimlendirilmiş olmalıdır URI'ler dahil olmak üzere, `https://` (önerilen) veya `http://`. Azure Storage henüz HTTPS özel etki alanları için desteklemediğinden, *gerekir* belirtin `http://` için herhangi bir uç nokta tooa özel etki alanı gösteren URI.
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>Bir uç nokta soneki ile bir bağlantı dizesi oluşturma
toocreate bir bağlantı dizesi için bölgeler ve farklı uç nokta sonekleri örnekleriyle depolama hizmetinde gibi Azure Çin veya Azure kamu, bağlantı dizesi biçimi aşağıdaki kullanım hello için. (Önerilen) HTTPS üzerinden tooconnect toohello depolama hesabı isteyip istemediğiniz veya HTTP belirtmek, yerine `myAccountName` depolama hesabınız hello adıyla değiştirin `myAccountKey` hesap erişim tuşu ve Değiştir ile `mySuffix` hello URI ile soneki:

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

Bir örnek bağlantı dizesi Azure Çin'de depolama hizmetleri aşağıdadır:

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>Bir bağlantı dizesini ayrıştırma
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
* [Geliştirme ve test amacıyla Hello Azure storage öykünücüsünü kullanma](storage-use-emulator.md)
* [Azure depolama gezginleri](storage-explorers.md)
* [Paylaşılan erişim imzaları (SAS) kullanma](storage-dotnet-shared-access-signature-part-1.md)

