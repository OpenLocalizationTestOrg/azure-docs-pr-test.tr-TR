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
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="c888a-103">Eşitleme içerikten bulut klasörü tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="c888a-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="c888a-104">Bu öğretici şunların nasıl yapıldığını gösterir toodeploy çok[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) içeriğinizi Dropbox ve OneDrive gibi popüler bulut depolama hizmetlerinden eşitleniyor tarafından.</span><span class="sxs-lookup"><span data-stu-id="c888a-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="c888a-105"><a name="overview"></a>İçerik eşitleme dağıtımına genel bakış</span><span class="sxs-lookup"><span data-stu-id="c888a-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="c888a-106">Merhaba isteğe bağlı içerik eşitleme dağıtım hello tarafından desteklenen [Kudu dağıtım altyapısı](https://github.com/projectkudu/kudu/wiki) App Service ile tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="c888a-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="c888a-107">Merhaba, [Azure Portal](https://portal.azure.com), bulut depolama alanınızda bir klasör belirtmek, bu klasördeki içerik ve uygulama kodu ile çalışma ve eşitleme tooApp hizmeti ile Merhaba bir düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c888a-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="c888a-108">İçerik eşitleme hello Kudu işlemi derleme ve dağıtım için kullanır.</span><span class="sxs-lookup"><span data-stu-id="c888a-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="c888a-109"><a name="contentsync"></a>Nasıl tooenable içerik eşitleme dağıtım</span><span class="sxs-lookup"><span data-stu-id="c888a-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="c888a-110">Merhaba içerik eşitlemenin tooenable [Azure Portal](https://portal.azure.com), şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c888a-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="c888a-111">Hello Azure Portalı'nda, uygulamanızın dikey penceresinde tıklayın **ayarları** > **dağıtım kaynağı**.</span><span class="sxs-lookup"><span data-stu-id="c888a-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="c888a-112">Tıklatın **Kaynağı Seç**seçeneğini belirleyip **OneDrive** veya **Dropbox** dağıtımı için hello kaynağı olarak.</span><span class="sxs-lookup"><span data-stu-id="c888a-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![İçerik eşitleme](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="c888a-114">Merhaba API'leri, temel farklılıkları nedeniyle **OneDrive iş** şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c888a-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="c888a-115">Tam hello yetkilendirme iş akışı tooenable uygulama hizmeti tooaccess belirli bir belirtilen yoldaki OneDrive veya Dropbox tüm uygulama hizmeti içeriğinize depolanacağı için önceden tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="c888a-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="c888a-116">App Service platformu erişmenizi sağlayan yetkilendirme hello sonra içerik yolu veya toochoose bu belirtilen içerik yolu altında varolan bir içerik klasörü hello seçeneği toocreate hello altında içerik bir klasör atanmış.</span><span class="sxs-lookup"><span data-stu-id="c888a-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="c888a-117">Uygulama hizmeti eşitleme için kullanılan bulut depolama hesaplarınızı altında belirtilen hello içerik yolları hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c888a-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="c888a-118">**OneDrive**:`Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="c888a-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="c888a-119">**Dropbox**:`Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="c888a-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="c888a-120">Merhaba sonra isteğe bağlı hello Azure Portalı'ndan ilk içerik eşitleme hello içerik eşitleme başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="c888a-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="c888a-121">Dağıtım geçmişi ile Merhaba kullanılabilir **dağıtımları** dikey.</span><span class="sxs-lookup"><span data-stu-id="c888a-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![Dağıtım geçmişi](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="c888a-123">Daha fazla bilgi için Dropbox dağıtım altında kullanılabilir [Dropbox gelen dağıtma](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="c888a-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

