---
title: "Windows PowerShell'de Azure bulut hizmeti ölçeklendirin | Microsoft Docs"
description: "(Klasik) Bir web rolü veya çalışan rolü veya Azure'da ölçeklendirmek için PowerShell kullanmayı öğrenin."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="67c6c-103">Bir bulut hizmeti PowerShell'de ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="67c6c-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="67c6c-104">Bir web rolü veya çalışan rolü giriş veya çıkış ekleyerek veya kaldırarak örnekleri ölçeklendirmek için Windows PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67c6c-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="67c6c-105">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="67c6c-105">Log in to Azure</span></span>

<span data-ttu-id="67c6c-106">Aboneliğinizi PowerShell aracılığıyla herhangi bir işlem gerçekleştirmeden önce oturum gerekir:</span><span class="sxs-lookup"><span data-stu-id="67c6c-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="67c6c-107">Hesabınızla ilişkili birden çok aboneliğiniz varsa, bulut hizmetinizin bulunduğu bağlı olarak geçerli abonelik değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="67c6c-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="67c6c-108">Geçerli aboneliğe denetlemek için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="67c6c-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="67c6c-109">Geçerli aboneliğe değiştirmeniz gerekiyorsa, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="67c6c-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="67c6c-110">Geçerli örnek sayısını rolünüz için denetleyin</span><span class="sxs-lookup"><span data-stu-id="67c6c-110">Check the current instance count for your role</span></span>

<span data-ttu-id="67c6c-111">Rolünüze geçerli durumunu denetlemek için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="67c6c-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="67c6c-112">Geçerli işletim sistemi sürümü ve örneğindeki sayımına dahil rolünün hakkında bilgi geri almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="67c6c-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="67c6c-113">Bu durumda, rolü tek bir örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="67c6c-113">In this case, the role has a single instance.</span></span>

![Rolü hakkında bilgi](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="67c6c-115">Daha fazla örnekleri ekleyerek rolünün ölçeğini genişletme</span><span class="sxs-lookup"><span data-stu-id="67c6c-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="67c6c-116">Rolünün ölçeğini genişletmek için örnek istenen sayısı geçirmek **sayısı** parametresi **kümesi AzureRole** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="67c6c-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="67c6c-117">Cmdlet blokları yeni örnekleri sırasında kısa bir süre içinde sağlanan ve başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="67c6c-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="67c6c-118">Yeni bir PowerShell penceresi ve çağrı açarsanız, bu süre boyunca **Get-AzureRole** daha önce gösterildiği gibi yeni hedef örneği sayısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="67c6c-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="67c6c-119">Ve Portalı'nda rol durumu inceleyin, başlamasını yeni örnek görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="67c6c-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![VM örneği portalında başlatılıyor](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="67c6c-121">Yeni örnekleri başladıktan sonra cmdlet başarıyla döndürür:</span><span class="sxs-lookup"><span data-stu-id="67c6c-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![Rol örneği artış başarılı](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="67c6c-123">Rol örnekleri kaldırarak ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="67c6c-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="67c6c-124">Aynı şekilde örnekleri kaldırarak bir rolde ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67c6c-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="67c6c-125">Ayarlama **sayısı** parametresini **kümesi AzureRole** istediğinizi ölçek işlemi tamamlandıktan sonra örnek sayısı için.</span><span class="sxs-lookup"><span data-stu-id="67c6c-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67c6c-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67c6c-126">Next steps</span></span>

<span data-ttu-id="67c6c-127">PowerShell bulut hizmetlerinden için Otomatik ölçek yapılandırmak mümkün değil.</span><span class="sxs-lookup"><span data-stu-id="67c6c-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="67c6c-128">Bunu yapmak için bkz: [ölçek bir bulut hizmeti otomatik olarak nasıl](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="67c6c-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
