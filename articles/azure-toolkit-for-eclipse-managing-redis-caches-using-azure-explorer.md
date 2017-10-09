---
title: "Eclipse için Azure Explorer hello aaaManaging Redis önbellekleri kullanarak | Microsoft Docs"
description: "Nasıl toomanage Eclipse için hello Azure Gezgini kullanarak Azure redis önbellekleri öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: aa0c38862bda7919a3fc6c53c2fdaf555dd64bff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-eclipse"></a>Redis önbellekleri Eclipse için hello Azure Gezgini kullanarak yönetme

Merhaba hello Eclipse için Azure Araç Seti parçası olan, kullanımı kolay çözümünü Java geliştiricilere yönetme redis için kendi Azure hesabında içinde önbellekleri Eclipse IDE hello sağlar Azure Gezgini.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a>Eclipse kullanarak bir Redis önbelleği oluşturma

Aşağıdaki adımları hello hello Azure Gezgini kullanarak redis önbelleği hello adımları toocreate yol.

1. İçinde tooyour Azure hesabı hello adımları hello kullanarak oturum [hello Eclipse için Azure Araç Seti içinde oturum yönergeleri] makalesi.

1. Merhaba, **Azure Gezgini** araç penceresi, hello genişletin **Azure** düğümünü sağ tıklatın **Redis önbellekleri**ve ardından **Redis önbelleği oluşturma**.

   ![Redis önbelleği menü oluşturma][CR01]

1. Ne zaman hello **yeni Redis önbelleği** iletişim kutusu görüntülenirse, aşağıdaki seçenekleri şu hello belirtin:

   ![Yeni Redis önbelleği Oluştur iletişim kutusu][CR02]

   a. **DNS adı**: hello DNS alt çok $a hello yeni redis önbelleği için belirtir ". redis.cache.windows .net"; Örneğin: *wingtiptoys.redis.cache.windows.net*.

   b. **Abonelik**: hello hello yeni redis önbelleği için toouse istediğiniz Azure aboneliği belirtir.

   c. **Kaynak grubu**: hello kaynak grubu, redis önbelleği için belirtir; seçenekleri aşağıdaki Merhaba, toochoose gerekir:
      * **Yeni Oluştur**: toocreate yeni bir kaynak grubu istediğinizi belirtir.
      * **Varolan kullanmak**: Azure hesabınızla ilişkili kaynak gruplarının bir listeden seçer belirtir.

   d. **Konum**: Burada, redis önbelleği oluşturulur; hello konumu belirtir örneğin, *Batı ABD*.

   e. **Fiyatlandırma katmanı**: redis önbelleği kullanan hangi fiyatlandırma katmanı belirtir; bu ayarı, istemci bağlantılarının hello sayısını belirler. (Daha fazla bilgi için bkz: [Redis önbelleği fiyatlandırma].)

   f. **SSL olmayan bağlantı noktası**: belirtir mi, redis önbelleği sağlayan SSL olmayan bağlantıları; varsayılan olarak, yalnızca SSL bağlantılarına izin verilir.

1. Tüm redis önbelleği ayarları belirtildiğinde tıklatın **Tamam**.

Redis önbelleği oluşturulduktan sonra hello Azure Gezgini görüntülenir.

   ![Redis önbelleği Azure Explorer'da][CR03]

> [!NOTE]
>
> Redis önbelleği ayarları Azure yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooconfigure Azure Redis önbelleği].
>

## <a name="display-hello-properties-for-your-redis-cache-in-eclipse"></a>Eclipse'te, Redis önbelleği için Hello özelliklerini görüntüle

1. İçinde Azure Gezgini Merhaba, redis önbelleği sağ tıklatın ve **Göster özellikleri**.

   ![Azure Explorer bağlam menüsü toodisplay özellikleri redis önbelleği için][SP01]

1. Hello Azure Gezgini, redis önbelleği için hello özelliklerini görüntüler.

   ![Redis önbelleği özellikleri][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a>Redis önbelleği Eclipse kullanarak silme

1. İçinde Azure Gezgini Merhaba, redis önbelleği sağ tıklatın ve **silmek**.

   ![Azure Explorer bağlam menüsü toodelete redis önbelleği][DE01]

1. Tıklatın **Tamam** olduğunda, redis önbelleği toodelete istenir.

   ![Redis önbelleği istemi Sil][DE02]

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Azure redis önbellekleri, yapılandırma ayarlarını ve fiyatlandırma hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:

* [Azure Redis Önbelleği]
* [Redis önbelleği belgeleri]
* [Redis önbelleği fiyatlandırma]
* [nasıl tooconfigure Azure Redis önbelleği]

<!-- URL List -->

[Redis önbelleği fiyatlandırma]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Önbelleği]: https://azure.microsoft.com/services/cache/
[Redis önbelleği belgeleri]: ./redis-cache/index.md
[nasıl tooconfigure Azure Redis önbelleği]: ./redis-cache/cache-configure.md
[hello Eclipse için Azure Araç Seti içinde oturum yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
