---
title: "Visual Studio ile Azure özel Bulutlar erişme | Microsoft Docs"
description: "Visual Studio kullanarak özel bulut kaynaklarına erişmek öğrenin."
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
ms.openlocfilehash: b2578c837732ab05d538e9b896ed3a3035075a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="bef4e-103">Özel Azure bulut Visual Studio ile erişme</span><span class="sxs-lookup"><span data-stu-id="bef4e-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="bef4e-104">Varsayılan olarak, Visual Studio genel Azure bulut REST uç noktalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="bef4e-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="bef4e-105">Bu konuda, erişim - ve - ile etkileşim kurmak için özel bulutunuzun sertifika kullanmayı öğrenin Visual Studio'dan özel bulut.</span><span class="sxs-lookup"><span data-stu-id="bef4e-105">In this topic, you learn how to use your private cloud's certificate to access - and interact with - the private cloud from Visual Studio.</span></span>

## <a name="to-access-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="bef4e-106">Özel bir Azure erişmek için Visual Studio bulut</span><span class="sxs-lookup"><span data-stu-id="bef4e-106">To access a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="bef4e-107">İçinde [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885) özel bulut için yayımlama ayarları dosyanız indirin veya yayımlama ayarları dosyası için yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="bef4e-107">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for the private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="bef4e-108">Azure ortak sürümünde bu indirmek için bağlantıdır [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="bef4e-108">On the public version of Azure, the link to download this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="bef4e-109">(İndirilen dosya uzantısına sahip olmalıdır `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="bef4e-109">(The downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="bef4e-110">Açık Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bef4e-110">Open Visual Studio</span></span>

1. <span data-ttu-id="bef4e-111">İçinde **Sunucu Gezgini**, sağ **Azure** düğümü ve bağlam menüsünden seçin **yönetin ve filtre abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="bef4e-111">In **Server Explorer**, right-click the **Azure** node and, from the context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Abonelikleri komutu yönetme](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="bef4e-113">İçinde **Microsoft Azure Aboneliklerini Yönet** iletişim kutusunda **sertifikaları** sekmesini tıklatın ve ardından **alma**.</span><span class="sxs-lookup"><span data-stu-id="bef4e-113">In the **Manage Microsoft Azure Subscriptions** dialog, select the **Certificates** tab, and then select **Import**.</span></span>
   
    ![Azure sertifikaları alma](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="bef4e-115">İçinde **alma Microsoft Azure abonelikleri** iletişim kutusunda **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="bef4e-115">In the **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Gözat düğmesi alma Microsoft Azure abonelikleri iletişim](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="bef4e-117">İçinde **açık** Seç iletişim kutusu, yayımlama ayarları dosyasını kaydettiğiniz dizine gidin dosya ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="bef4e-117">In the **Open** dialog, browse to the directory where you saved the publish-settings file, select the file, and then select **Open**.</span></span>

    ![Yayımlama ayarları dosyasını seçin](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="bef4e-119">Döndürülen zaman **alma Microsoft Azure abonelikleri** iletişim kutusunda **alma**.</span><span class="sxs-lookup"><span data-stu-id="bef4e-119">When returned to the **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Yayımlama ayarları dosyasını içeri aktar](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="bef4e-121">Sertifikaları yayımlama ayarları dosyasını Visual Studio'ya aktarılır ve şimdi, özel bulut kaynakları ile etkileşim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bef4e-121">The certificates are imported from the publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="bef4e-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bef4e-122">Next steps</span></span>
- [<span data-ttu-id="bef4e-123">Bir Azure bulut hizmeti Visual Studio'dan yayımlama</span><span class="sxs-lookup"><span data-stu-id="bef4e-123">Publishing to an Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="bef4e-124">[Nasıl yapılır: indirme ve içeri aktarma yayımlama ayarları ve abonelik bilgileri](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="bef4e-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
