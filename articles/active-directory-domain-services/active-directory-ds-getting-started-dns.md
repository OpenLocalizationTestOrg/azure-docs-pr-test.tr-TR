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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="a8c76-103">Azure Active Directory Domain Services'i etkinleştirme (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="a8c76-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="a8c76-104">Görev 4: Hello Azure sanal ağı için DNS ayarlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a8c76-104">Task 4: update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="a8c76-105">Yapılandırma Görevleri önceki hello Azure Active Directory etki alanı Hizmetleri dizininiz için başarıyla etkinleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="a8c76-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="a8c76-106">Merhaba sonraki hello sanal ağ içinde bilgisayarlara bağlanmak ve bu hizmetleri kullanan tooensure bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="a8c76-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="a8c76-107">Bu makalede, Azure Active Directory etki alanı Hizmetleri hello sanal ağda kullanılabilir olduğu sanal ağ toopoint toohello iki IP adreslerinizi hello DNS sunucusu ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a8c76-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

<span data-ttu-id="a8c76-108">tooupdate hello DNS sunucusu ayarını Azure Active Directory etki alanı Hizmetleri, aşağıdaki adımları tam hello etkinleştirdiğiniz hello sanal ağ için:</span><span class="sxs-lookup"><span data-stu-id="a8c76-108">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="a8c76-109">Merhaba **genel bakış** sekmesi listeler bir dizi **gerekli yapılandırma adımları** toobe gerçekleştirilen yönetilen etki alanınızın tam olarak sağlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="a8c76-109">hello **Overview** tab lists a set of **Required configuration steps** toobe performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="a8c76-110">Merhaba ilk yapılandırma adımı **sunucu için DNS ayarlarını güncelleştirme sanal ağınızı**.</span><span class="sxs-lookup"><span data-stu-id="a8c76-110">hello first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Etki Alanı Hizmetleri - Tamamen hazır haldeki Genel Bakış sekmesi](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="a8c76-112">Etki alanınız tamamen hazır hale getirildiğinde bu kutucukta iki IP adresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a8c76-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="a8c76-113">Bu IP adreslerinden her biri, yönetilen etki alanınıza yönelik bir etki alanı denetleyicisini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a8c76-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="a8c76-114">toocopy hello ilk IP adresi tooclipboard, hello Kopyala düğmesine bir sonraki tooit tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a8c76-114">toocopy hello first IP address tooclipboard, click hello copy button next tooit.</span></span> <span data-ttu-id="a8c76-115">Merhaba ardından **yapılandırmak DNS sunucuları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a8c76-115">Then click hello **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="a8c76-116">Merhaba ilk IP adresi hello yapıştırma **eklemek DNS sunucusu** metin kutusuna hello **DNS sunucuları** dikey.</span><span class="sxs-lookup"><span data-stu-id="a8c76-116">Paste hello first IP address into hello **Add DNS server** textbox in hello **DNS servers** blade.</span></span> <span data-ttu-id="a8c76-117">Kaydırma yatay toocopy hello ikinci IP adresi sol toohello ve hello yapıştırma **eklemek DNS sunucusu** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a8c76-117">Scroll horizontally toohello left toocopy hello second IP address and paste it into hello **Add DNS server** textbox.</span></span>

    ![Etki Alanı Hizmetleri - DNS'yi güncelleştirme](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="a8c76-119">Tıklatın **kaydetmek** tooupdate hello DNS sunucuları hello sanal ağ için bittiğinde.</span><span class="sxs-lookup"><span data-stu-id="a8c76-119">Click **Save** when you are done tooupdate hello DNS servers for hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="a8c76-120">Merhaba ağdaki sanal makinelerden yalnızca bir yeniden başlatma sonrasında hello yeni DNS ayarlarını alın.</span><span class="sxs-lookup"><span data-stu-id="a8c76-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="a8c76-121">Tooget hello güncelleştirilen DNS ayarlarını hemen gereksinim duyduğunuzda hello portal, PowerShell veya CLI hello yeniden tetikleyin.</span><span class="sxs-lookup"><span data-stu-id="a8c76-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="a8c76-122">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="a8c76-122">Next step</span></span>
[<span data-ttu-id="a8c76-123">Görev 5: parola eşitleme tooAzure Active Directory etki alanı Hizmetleri'ni etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a8c76-123">Task 5: enable password synchronization tooAzure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
