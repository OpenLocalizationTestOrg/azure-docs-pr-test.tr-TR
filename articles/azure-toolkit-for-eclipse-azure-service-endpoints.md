---
title: "aaaAzure hizmet uç noktaları"
description: "Merhaba Eclipse için Azure Araç Seti Hello Azure hizmet uç noktası ayarlarını açıklar."
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
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="26c43-103">Azure hizmet uç noktaları</span><span class="sxs-lookup"><span data-stu-id="26c43-103">Azure Service Endpoints</span></span>
<span data-ttu-id="26c43-104">Azure hizmet uç noktaları Azure platformu, uygulamanızın hello genel Azure platformu tarafından yönetilen dağıtılan tooand olup Çin ya da özel bir 21Vianet tarafından Azure işletilen belirler.</span><span class="sxs-lookup"><span data-stu-id="26c43-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="26c43-105">Merhaba **hizmet uç noktaları** iletişim kutusu, uç noktaları toouse istediğiniz hizmet toospecify sağlar.</span><span class="sxs-lookup"><span data-stu-id="26c43-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="26c43-106">tooopen hello **hizmet uç noktaları** Eclipse içinde iletişim tıklatın **penceresi**, tıklatın **Tercihler**, genişletin **Azure**ve ardından **Hizmet uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="26c43-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="26c43-107">Ayar hello **etkin olarak** alanı, hangi Azure hizmet uç noktaları hello için kullanılacak Azure geçerli çalışma alanınızda projeleri belirler.</span><span class="sxs-lookup"><span data-stu-id="26c43-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="26c43-108">Merhaba aşağıdaki gösterir hello **hizmet uç noktaları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="26c43-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="26c43-109">tooset hello hizmet uç noktaları</span><span class="sxs-lookup"><span data-stu-id="26c43-109">tooset hello service endpoints</span></span>
<span data-ttu-id="26c43-110">Merhaba, **hizmet uç noktaları** iletişim, Eylemler aşağıdaki hello birini gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26c43-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="26c43-111">Toouse hello genel Azure platformundan, hello isteyip istemediğinizi **etkin olarak** açılır listesinden, **windowsazure.com** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="26c43-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="26c43-112">Azure hello gelen Çin'de, 21Vianet tarafından işletilen toouse isteyip istemediğinizi **etkin olarak** açılır listesinden, **windowsazure.cn (Çin)** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="26c43-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="26c43-113">Toouse özel Azure platformu istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="26c43-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="26c43-114">**Düzenle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26c43-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="26c43-115">Bu hello bildiren bir iletişim kutusu açılır **hizmet uç noktaları** iletişim kapatılacak ve hello tercih ayarlar dosyasını açılabilir.</span><span class="sxs-lookup"><span data-stu-id="26c43-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="26c43-116">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26c43-116">Click **OK**.</span></span>

  3. <span data-ttu-id="26c43-117">Merhaba preferencesets.xml dosyasında, yeni bir oluşturma `preferenceset` öğesi.</span><span class="sxs-lookup"><span data-stu-id="26c43-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="26c43-118">Bu yeni öğe için oluşturma `name`, `blob`, `management`, `portalURL` ve `publishsettings` özniteliklerini ve değerlerini tooyour özel Azure platformu karşılık gelen bunları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="26c43-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="26c43-119">Merhaba varolan için sağlanan hello değerleri kullanabilirsiniz `preferenceset` öğeleri şablonları olarak.</span><span class="sxs-lookup"><span data-stu-id="26c43-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="26c43-120">**Not**: Merhaba hello için kullanılan değer `blob` özniteliği hello metin "blob" Merhaba URL'de içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="26c43-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="26c43-121">Kaydedin ve preferencesets.xml kapatın.</span><span class="sxs-lookup"><span data-stu-id="26c43-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="26c43-122">Merhaba yeniden **hizmet uç noktaları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="26c43-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="26c43-123">Merhaba gelen **etkin olarak** açılır listesinde, select hello etkin ayarlanmış oluşturulur ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="26c43-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="26c43-124">Özel, Azure platformu oluşturduktan sonra `preferenceset` öğesi hello tıklayarak hello atanan değerlerin tooit değiştirebilirsiniz **Düzenle** hello düğmesini **Services bitiş** iletişim.</span><span class="sxs-lookup"><span data-stu-id="26c43-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="26c43-125">Birden çok özel Azure platformu da oluşturabilirsiniz `preferenceset` , üzerinde isterse öğeleri.</span><span class="sxs-lookup"><span data-stu-id="26c43-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="26c43-126">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="26c43-126">See Also</span></span>
<span data-ttu-id="26c43-127">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="26c43-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="26c43-128">[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="26c43-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="26c43-129">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="26c43-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="26c43-130">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="26c43-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
