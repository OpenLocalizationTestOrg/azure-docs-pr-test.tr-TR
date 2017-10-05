---
title: "Azure hizmet uç noktaları"
description: "Azure araç setini Eclipse için Azure hizmet uç noktası ayarlarında açıklar."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="eb444-103">Azure hizmet uç noktaları</span><span class="sxs-lookup"><span data-stu-id="eb444-103">Azure Service Endpoints</span></span>
<span data-ttu-id="eb444-104">Azure hizmet uç noktaları Azure platformu uygulamanız için dağıtılan ve genel Azure platformu tarafından yönetilen olup olmadığını, Çin ya da özel bir 21Vianet tarafından Azure işletilen belirler.</span><span class="sxs-lookup"><span data-stu-id="eb444-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="eb444-105">**Hizmet uç noktaları** iletişim kutusu, kullanmak istediğiniz hangi hizmet uç noktaları belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb444-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="eb444-106">Açmak için **hizmet uç noktaları** Eclipse içinde iletişim tıklatın **penceresi**, tıklatın **Tercihler**, genişletin **Azure**ve ardından **hizmet uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="eb444-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="eb444-107">Ayarı **etkin olarak** alanı, hangi Azure hizmet uç noktaları geçerli çalışma alanınızı Azure projelerinde kullanılıp kullanılmayacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="eb444-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="eb444-108">Aşağıdaki gösterildiği **hizmet uç noktaları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb444-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="eb444-109">Hizmet uç noktalarına ayarlamak için</span><span class="sxs-lookup"><span data-stu-id="eb444-109">To set the service endpoints</span></span>
<span data-ttu-id="eb444-110">İçinde **hizmet uç noktaları** iletişim, aşağıdaki eylemlerden birini gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb444-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="eb444-111">Genel Azure platformu kullanmak isteyip istemediğinizi **etkin olarak** açılır listesinden, **windowsazure.com** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="eb444-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="eb444-112">Gelen Çin'de 21Vianet tarafından işletilen Azure kullanmak isteyip istemediğinizi **etkin olarak** açılır listesinden, **windowsazure.cn (Çin)** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="eb444-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="eb444-113">Özel bir Azure platformu kullanmak istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="eb444-113">If you want to use a private Azure platform:</span></span>

  1. <span data-ttu-id="eb444-114">**Düzenle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb444-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="eb444-115">Size bildiren bir iletişim kutusunu açar, **hizmet uç noktaları** iletişim kapatılacak ve tercih ayarlar dosyasını açılacak.</span><span class="sxs-lookup"><span data-stu-id="eb444-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="eb444-116">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb444-116">Click **OK**.</span></span>

  3. <span data-ttu-id="eb444-117">Preferencesets.xml dosyasında, yeni bir oluşturma `preferenceset` öğesi.</span><span class="sxs-lookup"><span data-stu-id="eb444-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="eb444-118">Bu yeni öğe için oluşturma `name`, `blob`, `management`, `portalURL` ve `publishsettings` özniteliklerini ve değerlerini karşılık gelen kendileri için özel Azure platformunuz için ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eb444-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="eb444-119">Varolan için sağlanan değerler kullanabilirsiniz `preferenceset` öğeleri şablonları olarak.</span><span class="sxs-lookup"><span data-stu-id="eb444-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="eb444-120">**Not**: için kullanılan değer `blob` özniteliği URL'deki "blob" metin içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb444-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>

  4. <span data-ttu-id="eb444-121">Kaydedin ve preferencesets.xml kapatın.</span><span class="sxs-lookup"><span data-stu-id="eb444-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="eb444-122">Yeniden **hizmet uç noktaları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb444-122">Reopen the **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="eb444-123">Gelen **etkin olarak** etkin ayarlanmış oluşturulur ve tıklatın açılır listesinden, **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="eb444-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="eb444-124">Özel, Azure platformu oluşturduktan sonra `preferenceset` öğesini tıklatarak atanmış değerleri değiştirebilir **Düzenle** düğmesini **Services bitiş** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb444-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="eb444-125">Birden çok özel Azure platformu da oluşturabilirsiniz `preferenceset` , üzerinde isterse öğeleri.</span><span class="sxs-lookup"><span data-stu-id="eb444-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="eb444-126">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="eb444-126">See Also</span></span>
<span data-ttu-id="eb444-127">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eb444-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="eb444-128">[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eb444-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="eb444-129">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eb444-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="eb444-130">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="eb444-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
