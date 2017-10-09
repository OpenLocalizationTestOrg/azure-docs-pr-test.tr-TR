---
title: "aaaUsing Emulator Express toorun ve hata ayıklama Azure bulut hizmeti yerel makinede | Microsoft Docs"
description: "Yerel makinede emulator Express toorun ve hata ayıklama bir bulut hizmeti kullanma"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="9e8fa-103">Öykünücü Express kullanarak toorun ve hata ayıklama Azure bulut hizmeti yerel makinede</span><span class="sxs-lookup"><span data-stu-id="9e8fa-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="9e8fa-104">Öykünücü Express kullanarak, test ve yönetici olarak Visual Studio çalıştırmadan bir bulut hizmetinde hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="9e8fa-105">Proje ayarları toouse Emulator Express ayarlayabilir veya Bulut hizmetiniz hello gereksinimlerine bağlı olarak tam öykünücü hello.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="9e8fa-106">Merhaba tam öykünücü hakkında daha fazla bilgi için bkz: [hello işlem öykünücüsü bir Azure uygulaması çalıştırmasına](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="9e8fa-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="9e8fa-107">Visual Studio öykünücüsü kullanarak</span><span class="sxs-lookup"><span data-stu-id="9e8fa-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="9e8fa-108">Azure SDK 2.3 veya daha sonra bir Azure projesi oluşturduğunuzda, Emulator Express otomatik olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="9e8fa-109">Önceki bir sürümünü hello Azure SDK'sı ile oluşturulan mevcut projeleri için aşağıdaki adımları tooselect Emulator Express hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="9e8fa-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="9e8fa-110">Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="9e8fa-111">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve, hello bağlam menüsünden seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="9e8fa-112">Başlangıç projeleri özellikler sayfalarında hello seçin **Web** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Bir Azure bulut hizmeti projesi özellikleri](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="9e8fa-114">Altında **yerel geliştirme sunucusu**seçin **IIS Express kullan seçeneği**.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="9e8fa-115">Altında **öykünücüsü**seçin **öykünücü kullan Express**.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="9e8fa-116">komutu bir komut isteminde aşağıdaki hello çalıştırmak toolaunch hello Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="9e8fa-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="9e8fa-117">Öykünücü Express sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="9e8fa-117">Emulator Express limitations</span></span>
<span data-ttu-id="9e8fa-118">Aşağıdaki sorunlar hello Emulator Express sınırlamaları bilinmektedir:</span><span class="sxs-lookup"><span data-stu-id="9e8fa-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="9e8fa-119">Öykünücü Express IIS Web sunucusu ile uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="9e8fa-120">Bulut hizmetinizi birden çok rol içerebilir, ancak her rol sınırlı tooone örneğidir.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="9e8fa-121">Bağlantı noktası numaralarını 1000 aşağıda erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="9e8fa-122">Normalde 1000 aşağıda bağlantı noktası kullanan bir kimlik doğrulama sağlayıcısı kullanırsanız, 1000'dir bu değeri tooa bağlantı noktası numarası toochange gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="9e8fa-123">Toohello Azure işlem öykünücüsü geçerli sınırlamalar tooEmulator Express de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="9e8fa-124">Örneğin, dağıtım başına 50'den fazla rol örneği sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e8fa-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="9e8fa-125">Hello Azure işlem öykünücüsü hakkında daha fazla bilgi için bkz: [hello işlem öykünücüsü bir Azure uygulaması çalıştırmasına](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="9e8fa-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e8fa-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e8fa-126">Next steps</span></span>
[<span data-ttu-id="9e8fa-127">Hata ayıklama Azure bulut Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="9e8fa-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
