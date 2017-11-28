---
title: "Güvenli uygulamalar ve Azure RemoteApp kaynaklarında | Microsoft Docs"
description: "Uygulamalar ve Azure RemoteApp kaynakları kilitleme öğrenin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 1c052906788f0f4fe4ca9fd6d3af63336245174a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a><span data-ttu-id="1dfb2-103">Güvenli uygulamalar ve Azure RemoteApp Kaynakları</span><span class="sxs-lookup"><span data-stu-id="1dfb2-103">Secure apps and resources in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1dfb2-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1dfb2-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1dfb2-106">Azure RemoteApp kullanıcıların ne kullanıcılarınız ve yapamayacağı denetlemenize olanak sağlayan Windows uygulamalarını, merkezi olarak yönetilen erişmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-106">Azure RemoteApp provides users access to centrally-managed Windows apps, which lets you control what your users can and can't do.</span></span>  <span data-ttu-id="1dfb2-107">Bu kullanıcının yönetilmeyen bir CİHAZDAN (ör. kendi kişisel Macbook) bağlanma ve kullanıcı erişimini denetlemek veya deneyimi istediğinizde özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-107">This is particularly useful when the user is connecting from an unmanaged device (like their personal Macbook) and you want to control the user access or experience.</span></span>

<span data-ttu-id="1dfb2-108">Örneğin, kullanıcı kimlik doğrulaması için Active Directory'yi kullanarak ve kullanıcılarınızın bir uygulama dışında veri kopyalamasını engellemek istiyorsanız, bir Uzak Masaüstü Grup İlkesi blok kullanıcılara veri kopyalama yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-108">For example, if you are using Active Directory for user authentication and you want to prevent your users from copying data out of an app, you can configure a Remote Desktop Group Policy to block users from copying data.</span></span>

<span data-ttu-id="1dfb2-109">Belirli bir uygulamanın koleksiyonunuzdaki internet erişimini engellemek istiyorsanız başka bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-109">Another example is if you want to block internet access for a particular app in your collection.</span></span> <span data-ttu-id="1dfb2-110">Koleksiyonunuz için görüntüyü oluştururken erişimini engelleyen bir Windows Güvenlik duvarı kural oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-110">You can create a Windows Firewall rule that blocks the access when you create the image for your collection.</span></span>

## <a name="implementation-options"></a><span data-ttu-id="1dfb2-111">Uygulama Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="1dfb2-111">Implementation options</span></span>
  <span data-ttu-id="1dfb2-112">Gerektiğinde ayrı ayrı veya dağıtımınızla birlikte kullanılabilir anahtar uygulama seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1dfb2-112">Here are the key implementation options, which can be used individually or in tandem as needed:</span></span>

1. <span data-ttu-id="1dfb2-113">RemoteApp koleksiyonunuzun etki alanına katılmış ise herhangi zorlayabilir [Grup İlkesi](https://technet.microsoft.com/library/cc725828.aspx) (açıklanan boşta ve bağlantı kesme zaman aşımı ilkeleri dışında [burada](../azure-subscription-service-limits.md)).</span><span class="sxs-lookup"><span data-stu-id="1dfb2-113">If your RemoteApp collection is domain joined you can enforce any [Group Policy](https://technet.microsoft.com/library/cc725828.aspx) (with the exception of the Idle and Disconnect timeout policies described [here](../azure-subscription-service-limits.md)).</span></span>
2. <span data-ttu-id="1dfb2-114">Grup (koleksiyonunuzu etki alanına katılmış veya AD'de sağ ayrıcalığa sahip değilsiniz değilse) ilkesi alternatif olarak, yapılandırdığınız [yerel ilkeler](https://technet.microsoft.com/library/cc775702.aspx) şablon görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-114">As an alternative to Group Policy (if your collection is not domain joined or you don't have the right privileges in AD), you can configure [Local Polices](https://technet.microsoft.com/library/cc775702.aspx) into your template image.</span></span>  <span data-ttu-id="1dfb2-115">Bir çakışma olduğunda bu grubun koz yerel ilkeleri ilkeler unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-115">Note that group polices trump local policies when there is a conflict.</span></span>
3. <span data-ttu-id="1dfb2-116">Bazı işletim sistemi/uygulama ayarları için ilke aracılığıyla yapılandırılabilir değildir, ancak bu kayıt defteri anahtarı kullanarak aracılığıyla olabilir [RegEdit aracı](remoteapp-hybridtrouble.md) şablon görüntünüzü yapılandırılırken.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-116">Some OS/app settings are not configurable via policy, but can be via registry key using the [RegEdit tool](remoteapp-hybridtrouble.md) while configuring your template image.</span></span>
4. <span data-ttu-id="1dfb2-117">Kullanabileceğiniz [Windows Güvenlik Duvarı](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) uygulamanın çalıştığı makine gelen ve giden ağ erişimi denetlemek.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-117">You can use [Windows Firewall](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) to control network access to and from the machine where the app is running.</span></span> <span data-ttu-id="1dfb2-118">Yalnızca URL'lerin ve bağlantı noktalarının burada tanımlanan engelleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-118">Just make sure you don't block the URLs and ports defined here.</span></span>
5. <span data-ttu-id="1dfb2-119">Kullanabileceğiniz [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) denetimine hangi uygulamaları ve dosyaları kullanıcıların çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-119">You can use [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) to control which applications and files users can run.</span></span> <span data-ttu-id="1dfb2-120">Örneğin, deneyimli kullanıcılar, yayımlanmayacak ancak koleksiyonu oluşturmak için kullanılan görüntüde kullanılabilir - AppLocker'ın bu engelleme uygulamaları çalıştırmak nasıl anlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-120">For example, savvy users can figure out how to run applications that you did not publish but that are available in the image you used to create the collection - AppLocker can block this.</span></span>

## <a name="detailed-information"></a><span data-ttu-id="1dfb2-121">Ayrıntılı bilgi</span><span class="sxs-lookup"><span data-stu-id="1dfb2-121">Detailed information</span></span>
* <span data-ttu-id="1dfb2-122">Aşağıdaki RDS ilkeleri büyük olasılıkla en yararlı şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1dfb2-122">The following RDS policies are likely to be most useful:</span></span>
  * [<span data-ttu-id="1dfb2-123">Cihaz ve kaynak yeniden yönlendirmesi</span><span class="sxs-lookup"><span data-stu-id="1dfb2-123">Device and Resource Redirection</span></span>](https://technet.microsoft.com/library/ee791794.aspx)
  * [<span data-ttu-id="1dfb2-124">Yazıcı yeniden yönlendirme</span><span class="sxs-lookup"><span data-stu-id="1dfb2-124">Printer Redirection</span></span>](https://technet.microsoft.com/library/ee791784.aspx)
  * <span data-ttu-id="1dfb2-125">[Profilleri](https://technet.microsoft.com/library/ee791865.aspx).</span><span class="sxs-lookup"><span data-stu-id="1dfb2-125">[Profiles](https://technet.microsoft.com/library/ee791865.aspx).</span></span>
* <span data-ttu-id="1dfb2-126">Bu yapılandırma Not RemoteApp PowerShell modülü aracılığıyla yeniden yönlendirme (görülen [burada](remoteapp-redirection.md)) güvenlik birincil amacı ise politikasını şablon görüntüsü aracılığıyla istersiniz ilkeyi uygulamak için istemci makinede kullanır Yerel ilke veya Grup İlkesi aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="1dfb2-126">Note that configuring redirections via the RemoteApp PowerShell module (as seen [here](remoteapp-redirection.md)) relies on the client machine to enforce the policy, so if security is the primary objective you'll want to enforce the policy via the template image local policy or via group policy.</span></span>
* <span data-ttu-id="1dfb2-127">[Windows Server 2012 R2 ilkeleri](https://technet.microsoft.com/library/hh831791.aspx).</span><span class="sxs-lookup"><span data-stu-id="1dfb2-127">[Windows Server 2012 R2 policies](https://technet.microsoft.com/library/hh831791.aspx).</span></span>
* <span data-ttu-id="1dfb2-128">[Office 2013 ilkeleri](https://technet.microsoft.com/library/cc178969.aspx) (dahil olmak üzere [Office araç çubuğunu özelleştirme](https://technet.microsoft.com/library/cc179143.aspx)).</span><span class="sxs-lookup"><span data-stu-id="1dfb2-128">[Office 2013 polices](https://technet.microsoft.com/library/cc178969.aspx) (including [how to customize the Office toolbar](https://technet.microsoft.com/library/cc179143.aspx)).</span></span>

