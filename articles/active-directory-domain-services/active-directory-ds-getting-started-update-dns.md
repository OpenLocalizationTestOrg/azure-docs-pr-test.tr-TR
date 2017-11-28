---
title: "Azure Active Directory Domain Services: Azure sanal ağı için DNS ayarlarını güncelleştirme | Microsoft Docs"
description: "Azure Active Directory Etki Alanı Hizmetleri ile çalışmaya başlama"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 8bee2a25f196d645b27f30f21305b1550e44e07a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="3d960-103">Azure sanal ağı için DNS ayarlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3d960-103">Update DNS settings for the Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="3d960-104">Görev 4: Azure sanal ağı için DNS ayarlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3d960-104">Task 4: Update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="3d960-105">Önceki yapılandırma görevlerinde dizininiz için Azure Active Directory Domain Services başarıyla etkinleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="3d960-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="3d960-106">Sonraki göreviniz sanal ağınızdaki bilgisayarların bu hizmetlere bağlanabilmesini ve bu hizmetleri kullanabilmesini sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="3d960-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="3d960-107">Bu makalede, sanal ağınızdaki DNS sunucusu ayarlarını, sanal ağda Azure Active Directory Domain Services’in kullanılabilir olduğu iki IP adresini işaret edecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3d960-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="3d960-108">Azure Active Directory Domain Services'i dizin için etkinleştirdikten sonra, dizinin **Yapılandır** sekmesinde görüntülenen Azure Active Directory Domain Services'in IP adreslerini not edin.</span><span class="sxs-lookup"><span data-stu-id="3d960-108">After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="3d960-109">Azure Active Directory Domain Services'i etkinleştirdiğiniz sanal ağın DNS sunucusu ayarını güncelleştirmek için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="3d960-109">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="3d960-110">[Klasik Azure portalı](https://manage.windowsazure.com)'na gidin.</span><span class="sxs-lookup"><span data-stu-id="3d960-110">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3d960-111">Sol bölmede **Ağlar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3d960-111">In the left pane, select **Networks**.</span></span>  
    <span data-ttu-id="3d960-112">**Ağlar** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="3d960-112">The **Networks** window opens.</span></span>

    ![Sanal ağlar penceresi](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="3d960-114">**Sanal Ağlar** sekmesinde, Azure Active Directory Domain Services'i etkinleştirdiğiniz sanal ağı seçerek özelliklerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="3d960-114">On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.</span></span>
4. <span data-ttu-id="3d960-115">**Configure (Yapılandır)** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3d960-115">Click the **Configure** tab.</span></span>

    ![Sanal ağlar penceresi](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="3d960-117">**DNS sunucuları** bölümünde, dizininizin **Yapılandır** sekmesindeki **Domain Services** kısmında görüntülenen her iki IP adresini de girdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3d960-117">In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="3d960-118">Bu sanal ağa ait DNS sunucusu ayarlarını kaydetmek için pencerenin alt kısmındaki görev bölmesinde **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3d960-118">To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.</span></span>

   ![Sanal ağın DNS sunucusu ayarlarını güncelleştirme](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="3d960-120">Ağ üzerindeki sanal makineler, yeni DNS ayarlarını yalnızca yeniden başlatma işleminin ardından alabilir.</span><span class="sxs-lookup"><span data-stu-id="3d960-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="3d960-121">Sanal makinelerin güncelleştirilen DNS ayarlarını doğrudan almasını istiyorsanız portal, PowerShell veya CLI aracılığıyla bir yeniden başlatma tetikleyin.</span><span class="sxs-lookup"><span data-stu-id="3d960-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3d960-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d960-122">Next steps</span></span>
<span data-ttu-id="3d960-123">Görev 5: [Azure Active Directory Domain Services ile parola eşitlemeyi etkinleştirme](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="3d960-123">Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
