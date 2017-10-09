---
title: "Visual Studio ile özel Azure Bulutları aaaAccessing | Microsoft Docs"
description: "Nasıl tooaccess özel bulut kaynaklarına Visual Studio kullanarak öğrenin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="4c75c-103">Özel Azure bulut Visual Studio ile erişme</span><span class="sxs-lookup"><span data-stu-id="4c75c-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="4c75c-104">Varsayılan olarak, Visual Studio genel Azure bulut REST uç noktalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="4c75c-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="4c75c-105">Bu konuda, nasıl toouse, özel bulut bilgi sertifika tooaccess - kullanıcının ve etkileşim - hello Visual Studio'dan özel bulut.</span><span class="sxs-lookup"><span data-stu-id="4c75c-105">In this topic, you learn how toouse your private cloud's certificate tooaccess - and interact with - hello private cloud from Visual Studio.</span></span>

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="4c75c-106">Visual Studio'da tooaccess özel bir Azure bulut</span><span class="sxs-lookup"><span data-stu-id="4c75c-106">tooaccess a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="4c75c-107">Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885) hello özel bulut için yayımlama ayarları dosyanız indirin veya yayımlama ayarları dosyası için yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="4c75c-107">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for hello private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="4c75c-108">Merhaba ortak sürümünde Azure, bu bağlantı toodownload hello [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="4c75c-108">On hello public version of Azure, hello link toodownload this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="4c75c-109">(Merhaba indirilen dosya uzantısına sahip olmalıdır `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="4c75c-109">(hello downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="4c75c-110">Açık Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4c75c-110">Open Visual Studio</span></span>

1. <span data-ttu-id="4c75c-111">İçinde **Sunucu Gezgini**, sağ hello **Azure** düğümü ve hello bağlam menüsünden seçin **yönetin ve filtre abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="4c75c-111">In **Server Explorer**, right-click hello **Azure** node and, from hello context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Abonelikleri komutu yönetme](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="4c75c-113">Merhaba, **Microsoft Azure Aboneliklerini Yönet** iletişim, select hello **sertifikaları** sekmesini tıklatın ve ardından **alma**.</span><span class="sxs-lookup"><span data-stu-id="4c75c-113">In hello **Manage Microsoft Azure Subscriptions** dialog, select hello **Certificates** tab, and then select **Import**.</span></span>
   
    ![Azure sertifikaları alma](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="4c75c-115">Merhaba, **alma Microsoft Azure abonelikleri** iletişim kutusunda **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="4c75c-115">In hello **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Gözat düğmesi hello alma Microsoft Azure abonelikleri iletişim](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="4c75c-117">Merhaba, **açık** iletişim kutusunda, Gözat toohello, kaydedilen hello yayımlama ayarları dosyası, select hello burada dosya dizin ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="4c75c-117">In hello **Open** dialog, browse toohello directory where you saved hello publish-settings file, select hello file, and then select **Open**.</span></span>

    ![Merhaba yayımlama ayarları dosyasını seçin](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="4c75c-119">Zaman toohello döndürülen **alma Microsoft Azure abonelikleri** iletişim kutusunda **alma**.</span><span class="sxs-lookup"><span data-stu-id="4c75c-119">When returned toohello **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Merhaba yayımlama ayarları dosyasını içeri aktarma](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="4c75c-121">Merhaba sertifikaları hello yayımlama ayarları dosyası Visual Studio'ya aktarılır ve şimdi, özel bulut kaynakları ile etkileşim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c75c-121">hello certificates are imported from hello publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="4c75c-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c75c-122">Next steps</span></span>
- [<span data-ttu-id="4c75c-123">Yayımlama tooan Visual Studio'dan Azure bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="4c75c-123">Publishing tooan Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="4c75c-124">[Nasıl yapılır: indirme ve içeri aktarma yayımlama ayarları ve abonelik bilgileri](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="4c75c-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
