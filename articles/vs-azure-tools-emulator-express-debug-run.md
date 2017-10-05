---
title: "Çalıştırın ve bir Azure bulut hizmeti yerel makinede hata ayıklamak için emulator Express kullanarak | Microsoft Docs"
description: "Öykünücü Express'i çalıştırın ve bir bulut hizmeti yerel makinede hata ayıklamak için kullanma"
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
ms.openlocfilehash: d7d87045569fdc473333deae05f95d1df343b68c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="3b1d9-103">Öykünücü Express'i çalıştırın ve bir Azure bulut hizmeti yerel makinede hata ayıklamak için kullanma</span><span class="sxs-lookup"><span data-stu-id="3b1d9-103">Using Emulator Express to run and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="3b1d9-104">Öykünücü Express kullanarak, test ve yönetici olarak Visual Studio çalıştırmadan bir bulut hizmetinde hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="3b1d9-105">Proje ayarlarınızı Emulator Express veya Bulut hizmetinizin gereksinimlerine bağlı olarak tam öykünücü kullanacak şekilde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-105">You can set your project settings to use either Emulator Express or the full emulator, depending on the requirements of your cloud service.</span></span> <span data-ttu-id="3b1d9-106">Tam öykünücü hakkında daha fazla bilgi için bkz: [Azure uygulamanın işlem Öykünücüde çalıştırma](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="3b1d9-106">For more information about the full emulator, see [Run an Azure Application in the Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="3b1d9-107">Visual Studio öykünücüsü kullanarak</span><span class="sxs-lookup"><span data-stu-id="3b1d9-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="3b1d9-108">Azure SDK 2.3 veya daha sonra bir Azure projesi oluşturduğunuzda, Emulator Express otomatik olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="3b1d9-109">Azure SDK'ın önceki bir sürümü ile oluşturulmuş mevcut projeleri için Emulator Express seçmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="3b1d9-109">For existing projects that were created with an earlier version of the Azure SDK, use the following steps to select Emulator Express:</span></span>

1. <span data-ttu-id="3b1d9-110">Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="3b1d9-111">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve bağlam menüsünden seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>

1. <span data-ttu-id="3b1d9-112">Proje Özellikleri sayfaları seçin **Web** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-112">In the projects properties pages, select the **Web** tab.</span></span>

    ![Bir Azure bulut hizmeti projesi özellikleri](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="3b1d9-114">Altında **yerel geliştirme sunucusu**seçin **IIS Express kullan seçeneği**.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="3b1d9-115">Altında **öykünücüsü**seçin **öykünücü kullan Express**.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="3b1d9-116">Öykünücü Express başlatmak için komut isteminde aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3b1d9-116">To launch the Emulator Express, run the following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="3b1d9-117">Öykünücü Express sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="3b1d9-117">Emulator Express limitations</span></span>
<span data-ttu-id="3b1d9-118">Aşağıdaki sorunlar Emulator Express sınırlamaları bilinmektedir:</span><span class="sxs-lookup"><span data-stu-id="3b1d9-118">The following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="3b1d9-119">Öykünücü Express IIS Web sunucusu ile uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="3b1d9-120">Bulut hizmetinizi birden çok rol içerebilir, ancak her rol için bir örnek sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-120">Your cloud service can contain multiple roles, but each role is limited to one instance.</span></span>
- <span data-ttu-id="3b1d9-121">Bağlantı noktası numaralarını 1000 aşağıda erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="3b1d9-122">Normalde 1000 aşağıda bağlantı noktası kullanan bir kimlik doğrulama sağlayıcısı kullanırsanız, bu değer 1000'dir bir bağlantı noktası numarasını değiştirmek gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-122">If you use an authentication provider that normally uses a port below 1000, you might need to change this value to a port number that's above 1000.</span></span>
- <span data-ttu-id="3b1d9-123">Azure işlem öykünücüsü için geçerli sınırlamalar Emulator Express için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-123">Any limitations that apply to the Azure Compute Emulator also apply to Emulator Express.</span></span> <span data-ttu-id="3b1d9-124">Örneğin, dağıtım başına 50'den fazla rol örneği sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="3b1d9-125">Azure işlem öykünücüsü hakkında daha fazla bilgi için bkz: [Azure uygulamanın işlem Öykünücüde çalıştırma](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="3b1d9-125">For more information about the Azure Compute Emulator, see [Run an Azure Application in the Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b1d9-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3b1d9-126">Next steps</span></span>
[<span data-ttu-id="3b1d9-127">Hata ayıklama Azure bulut Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="3b1d9-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
