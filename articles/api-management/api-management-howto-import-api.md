---
title: "aaaImport bir API uygulamasına Azure API Management | Microsoft Docs"
description: "Bilgi nasıl tooimport bir API ve Azure API Management içine işlemlerini."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>Nasıl tooimport hello Azure API Management işlemleri olan bir API tanımı
API Management, yeni API'leri oluşturulabilir ve hello işlemleri el ile eklenmiş veya hello API hello işlemlerini tek bir adımda birlikte içeri aktarılabilir.

API'ler ve bunların işlemler biçimleri aşağıdaki hello kullanılarak alınabilir.

* WADL
* Swagger

Bu kılavuz gösterir yeni bir API oluşturma ve işlemlerini tek bir adımda içeri aktarın. El ile bir API oluşturma ve işlemleri ekleme hakkında daha fazla bilgi için bkz: [nasıl toocreate API'leri] [ How toocreate APIs] ve [nasıl tooadd işlemleri tooan API] [ How tooadd operations tooan API].

## <a name="import-api"> </a>Bir API'yi içeri aktarma
API oluşturulur ve hello yayımcı portalında yapılandırılır. tooaccess hello yayımcı portalı, tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda. Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.

![Yayımcı portalı][api-management-management-console]

Tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **API'yi içeri aktarma**.

![İçeri aktarma API'si][api-management-import-apis]

Merhaba **içeri aktarma API'si** penceresinde toohello üç yolu tooprovide hello API Belirtimi karşılık gelen üç sekme bulunur.

* **Pano'dan** hello belirlenen metin kutusuna toopaste hello API belirtimine izin verir.
* **Dosyadan** hello API belirtimi içeren toobrowse tooand select hello dosyası sağlar.
* **URL'den** toosupply hello URL toohello belirtimi hello API sağlar.

![API'yi İçeri Aktar biçimi][api-management-import-api-clipboard]

Merhaba API Belirtimi sağladıktan sonra hello radyo düğmeleri hello sağ tooindicate hello belirtimi biçimi kullanın. biçimler aşağıdaki hello desteklenir.

* WADL
* Swagger

Ardından, girin bir **Web API'si URL soneki**. API management hizmetiniz için temel URL eklenmiş toohello budur. Her bir API Management hizmet örneği üzerinde barındırılan tüm API'leri Hello temel URL yaygındır. API Management API'leri kendi soneki ayırır ve bu nedenle hello soneki belirli bir API management hizmet örneğindeki her API için benzersiz olmalıdır.

Tüm değerleri girdikten sonra tıklayın **kaydetmek** toocreate hello API ve hello ilişkili işlemleri. 

> [!NOTE]
> Swagger biçiminde temel hesaplayıcı API'sini içeri aktarma bir öğretici için bkz: [ilk API'nizi Azure API Management'te yönetme](api-management-get-started.md).
> 
> 

## <a name="export-api"></a> Bir API dışarı aktarma
Ayrıca tooimporting, yeni API'leri, Apı'lerinizi hello tanımlarını hello yayımcı Portalı'ndan verebilirsiniz. Bu nedenle, toodo'ı tıklatın **verme API** hello gelen **Özet sekmesi** , **API**.

![API dışarı aktarma][api-management-export-api]

API WADL veya Swagger kullanılarak verilebilir. Merhaba istediğiniz biçimi seçin, **kaydetmek**ve hangi toosave hello dosyasında hello konumu seçin.

![Dışa aktarma API biçimi][api-management-export-api-format]

## <a name="next-steps"> </a>Sonraki adımlar
Bir API oluşturulur ve içe hello işlemleri, gözden geçirin ve yapılandırabilirsiniz sonra herhangi bir ek ayarı hello API tooa ürün ekleyin ve böylece geliştiriciler için kullanılabilir yayımlayın. Daha fazla bilgi için aşağıdaki kılavuzları hello bakın.

* [Nasıl tooconfigure API ayarları][How tooconfigure API settings]
* [Nasıl toocreate ürün ve yayımlama][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
