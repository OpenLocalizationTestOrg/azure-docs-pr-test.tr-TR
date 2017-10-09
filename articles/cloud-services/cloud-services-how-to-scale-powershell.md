---
title: Windows PowerShell'de Azure bulut hizmeti aaaScale | Microsoft Docs
description: "(Klasik) Bilgi nasıl toouse PowerShell tooscale bir web rolü veya içinde veya azure'da çalışan rolü."
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
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a><span data-ttu-id="f7f64-103">Nasıl tooscale bir bulut hizmeti PowerShell'de</span><span class="sxs-lookup"><span data-stu-id="f7f64-103">How tooscale a cloud service in PowerShell</span></span>

<span data-ttu-id="f7f64-104">Ekleyerek veya kaldırarak örnekleri, bir web rolü veya çalışan rolü veya Windows PowerShell tooscale kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7f64-104">You can use Windows PowerShell tooscale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-tooazure"></a><span data-ttu-id="f7f64-105">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="f7f64-105">Log in tooAzure</span></span>

<span data-ttu-id="f7f64-106">Aboneliğinizi PowerShell aracılığıyla herhangi bir işlem gerçekleştirmeden önce oturum gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7f64-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="f7f64-107">Hesabınızla ilişkili birden çok aboneliğiniz varsa, bulut hizmetinizin bulunduğu bağlı olarak toochange hello geçerli abonelik gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f7f64-107">If you have multiple subscriptions associated with your account, you may need toochange hello current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="f7f64-108">toocheck hello geçerli abonelik, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f7f64-108">toocheck hello current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="f7f64-109">Toochange hello geçerli abonelik gerekiyorsa, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f7f64-109">If you need toochange hello current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a><span data-ttu-id="f7f64-110">Merhaba geçerli örnek sayısını rolünüz için denetleyin</span><span class="sxs-lookup"><span data-stu-id="f7f64-110">Check hello current instance count for your role</span></span>

<span data-ttu-id="f7f64-111">toocheck hello geçerli durumunu sizin rolünüz çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f7f64-111">toocheck hello current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="f7f64-112">Geçerli işletim sistemi sürümü ve örneğindeki sayımına dahil hello rolünün hakkında bilgi geri almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7f64-112">You should get back information about hello role, including its current OS version and instance count.</span></span> <span data-ttu-id="f7f64-113">Bu durumda, tek bir örnek hello rolüne sahip.</span><span class="sxs-lookup"><span data-stu-id="f7f64-113">In this case, hello role has a single instance.</span></span>

![Merhaba rolü hakkında bilgi](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a><span data-ttu-id="f7f64-115">Daha fazla örnekleri ekleyerek Hello rolünün ölçeğini genişletme</span><span class="sxs-lookup"><span data-stu-id="f7f64-115">Scale out hello role by adding more instances</span></span>

<span data-ttu-id="f7f64-116">tooscale rolünüze çıkışı geçişi hello istenen örneklerinin sayısını hello olarak **sayısı** parametresi toohello **kümesi AzureRole** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f7f64-116">tooscale out your role, pass hello desired number of instances as hello **Count** parameter toohello **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="f7f64-117">Merhaba cmdlet blokları hello yeni örnekleri sırasında kısa bir süre içinde sağlanan ve başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="f7f64-117">hello cmdlet blocks momentarily while hello new instances are provisioned and started.</span></span> <span data-ttu-id="f7f64-118">Yeni bir PowerShell penceresi ve çağrı açarsanız, bu süre boyunca **Get-AzureRole** daha önce gösterildiği gibi hello yeni hedef örneği sayısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f7f64-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see hello new target instance count.</span></span> <span data-ttu-id="f7f64-119">Ve hello rol durumu hello portalında inceleyin, başlamasını hello yeni örnek görmelisiniz:</span><span class="sxs-lookup"><span data-stu-id="f7f64-119">And if you inspect hello role status in hello portal, you should see hello new instance starting up:</span></span>

![VM örneği portalında başlatılıyor](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="f7f64-121">Merhaba yeni örnekleri başladıktan sonra hello cmdlet başarıyla döndürür:</span><span class="sxs-lookup"><span data-stu-id="f7f64-121">Once hello new instances have started, hello cmdlet will return successfully:</span></span>

![Rol örneği artış başarılı](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a><span data-ttu-id="f7f64-123">Ölçek kaldırarak hello rolü örnekleri</span><span class="sxs-lookup"><span data-stu-id="f7f64-123">Scale in hello role by removing instances</span></span>

<span data-ttu-id="f7f64-124">Hello örnekleri kaldırarak bir rolde ölçeklendirebilirsiniz aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="f7f64-124">You can scale in a role by removing instances in hello same way.</span></span> <span data-ttu-id="f7f64-125">Kümesi hello **sayısı** parametresini **kümesi AzureRole** toohello numarası örneklerini hello ölçek işleminde tamamlandıktan sonra toohave istiyor.</span><span class="sxs-lookup"><span data-stu-id="f7f64-125">Set hello **Count** parameter on **Set-AzureRole** toohello number of instances you want toohave after hello scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7f64-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f7f64-126">Next steps</span></span>

<span data-ttu-id="f7f64-127">PowerShell bulut hizmetlerinden için olası tooconfigure otomatik ölçek olmadığı.</span><span class="sxs-lookup"><span data-stu-id="f7f64-127">It is not possible tooconfigure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="f7f64-128">bkz, toodo [nasıl tooauto ölçeklendirme bir bulut hizmeti](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f7f64-128">toodo that, see [How tooauto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
