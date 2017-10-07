---
title: "bir bulut klasörü tooAzure uygulama hizmeti aaaSync içeriği"
description: "Nasıl toodeploy uygulama tooAzure uygulama hizmeti içerik aracılığıyla eşitleme bulut klasöründen öğrenin."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>Eşitleme içerikten bulut klasörü tooAzure uygulama hizmeti
Bu öğretici şunların nasıl yapıldığını gösterir toodeploy çok[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) içeriğinizi Dropbox ve OneDrive gibi popüler bulut depolama hizmetlerinden eşitleniyor tarafından. 

## <a name="overview"></a>İçerik eşitleme dağıtımına genel bakış
Merhaba isteğe bağlı içerik eşitleme dağıtım hello tarafından desteklenen [Kudu dağıtım altyapısı](https://github.com/projectkudu/kudu/wiki) App Service ile tümleşiktir. Merhaba, [Azure Portal](https://portal.azure.com), bulut depolama alanınızda bir klasör belirtmek, bu klasördeki içerik ve uygulama kodu ile çalışma ve eşitleme tooApp hizmeti ile Merhaba bir düğmesine tıklayın. İçerik eşitleme hello Kudu işlemi derleme ve dağıtım için kullanır. 

## <a name="contentsync"></a>Nasıl tooenable içerik eşitleme dağıtım
Merhaba içerik eşitlemenin tooenable [Azure Portal](https://portal.azure.com), şu adımları izleyin:

1. Hello Azure Portalı'nda, uygulamanızın dikey penceresinde tıklayın **ayarları** > **dağıtım kaynağı**. Tıklatın **Kaynağı Seç**seçeneğini belirleyip **OneDrive** veya **Dropbox** dağıtımı için hello kaynağı olarak. 
   
    ![İçerik eşitleme](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > Merhaba API'leri, temel farklılıkları nedeniyle **OneDrive iş** şu anda desteklenmiyor. 
   > 
   > 
2. Tam hello yetkilendirme iş akışı tooenable uygulama hizmeti tooaccess belirli bir belirtilen yoldaki OneDrive veya Dropbox tüm uygulama hizmeti içeriğinize depolanacağı için önceden tanımlanmış.  
    App Service platformu erişmenizi sağlayan yetkilendirme hello sonra içerik yolu veya toochoose bu belirtilen içerik yolu altında varolan bir içerik klasörü hello seçeneği toocreate hello altında içerik bir klasör atanmış. Uygulama hizmeti eşitleme için kullanılan bulut depolama hesaplarınızı altında belirtilen hello içerik yolları hello şunlardır:  
   
   * **OneDrive**:`Apps\Azure Web Apps` 
   * **Dropbox**:`Dropbox\Apps\Azure`
3. Merhaba sonra isteğe bağlı hello Azure Portalı'ndan ilk içerik eşitleme hello içerik eşitleme başlatılabilir. Dağıtım geçmişi ile Merhaba kullanılabilir **dağıtımları** dikey.
   
    ![Dağıtım geçmişi](./media/app-service-deploy-content-sync/onedrive_sync.png)

Daha fazla bilgi için Dropbox dağıtım altında kullanılabilir [Dropbox gelen dağıtma](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx). 

