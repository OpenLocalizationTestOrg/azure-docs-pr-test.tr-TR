---
title: "Azure Active Directory etki alanı Hizmetleri: Güncelleştirme hello Azure sanal ağı için DNS ayarlarını | Microsoft Docs"
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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="37e73-103">Hello Azure sanal ağı için DNS ayarlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="37e73-103">Update DNS settings for hello Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="37e73-104">Görev 4: Güncelleştirme hello Azure sanal ağı için DNS ayarları</span><span class="sxs-lookup"><span data-stu-id="37e73-104">Task 4: Update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="37e73-105">Yapılandırma Görevleri önceki hello Azure Active Directory etki alanı Hizmetleri dizininiz için başarıyla etkinleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="37e73-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="37e73-106">Merhaba sonraki hello sanal ağ içinde bilgisayarlara bağlanmak ve bu hizmetleri kullanan tooensure bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="37e73-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="37e73-107">Bu makalede, Azure Active Directory etki alanı Hizmetleri hello sanal ağda kullanılabilir olduğu sanal ağ toopoint toohello iki IP adreslerinizi hello DNS sunucusu ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="37e73-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="37e73-108">Azure Active Directory etki alanı Hizmetleri hello dizin için etkinleştirdikten sonra Azure Active Directory etki alanı üzerinde hello görüntülenen Hizmetleri hello IP adreslerini Not **yapılandırma** dizininizin sekmesi.</span><span class="sxs-lookup"><span data-stu-id="37e73-108">After you've enabled Azure Active Directory Domain Services for hello directory, note hello IP addresses for Azure Active Directory Domain Services that are displayed on hello **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="37e73-109">tooupdate hello DNS sunucusu ayarını Azure Active Directory etki alanı Hizmetleri, aşağıdaki adımları tam hello etkinleştirdiğiniz hello sanal ağ için:</span><span class="sxs-lookup"><span data-stu-id="37e73-109">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="37e73-110">Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="37e73-110">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="37e73-111">Merhaba sol bölmesinde seçin **ağlar**.</span><span class="sxs-lookup"><span data-stu-id="37e73-111">In hello left pane, select **Networks**.</span></span>  
    <span data-ttu-id="37e73-112">Merhaba **ağlar** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="37e73-112">hello **Networks** window opens.</span></span>

    ![Sanal ağlar penceresi](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="37e73-114">Merhaba üzerinde **sanal ağlar** sekmesi, select hello sanal ağ içinde etkin Azure Active Directory etki alanı Hizmetleri tooview özellikleri.</span><span class="sxs-lookup"><span data-stu-id="37e73-114">On hello **Virtual Networks** tab, select hello virtual network in which you enabled Azure Active Directory Domain Services tooview its properties.</span></span>
4. <span data-ttu-id="37e73-115">Merhaba tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="37e73-115">Click hello **Configure** tab.</span></span>

    ![Sanal ağlar penceresi](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="37e73-117">Merhaba, **DNS sunucuları** bölümünde, hem de hello görüntülenen her hello IP adreslerini girin **etki alanı Hizmetleri** hello bölüm **yapılandırma** dizininizin sekmesi.</span><span class="sxs-lookup"><span data-stu-id="37e73-117">In hello **DNS servers** section, enter both of hello IP addresses that were displayed in hello **Domain Services** section on hello **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="37e73-118">toosave hello DNS sunucusu ayarlarını hello pencerenin hello altındaki hello görev bölmesindeki bu sanal ağ tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="37e73-118">toosave hello DNS server settings for this virtual network, in hello task pane at hello bottom of hello window, click **Save**.</span></span>

   ![Merhaba sanal ağ Hello DNS sunucusu ayarlarını güncelleştirme](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="37e73-120">Merhaba ağdaki sanal makinelerden yalnızca bir yeniden başlatma sonrasında hello yeni DNS ayarlarını alın.</span><span class="sxs-lookup"><span data-stu-id="37e73-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="37e73-121">Tooget hello güncelleştirilen DNS ayarlarını hemen gereksinim duyduğunuzda hello portal, PowerShell veya CLI hello yeniden tetikleyin.</span><span class="sxs-lookup"><span data-stu-id="37e73-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="37e73-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37e73-122">Next steps</span></span>
<span data-ttu-id="37e73-123">Görev 5: [parola eşitleme tooAzure Active Directory etki alanı Hizmetleri'ni etkinleştirme](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="37e73-123">Task 5: [Enable password synchronization tooAzure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
