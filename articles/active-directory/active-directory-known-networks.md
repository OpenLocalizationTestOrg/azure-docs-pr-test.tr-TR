---
title: "Merhaba Klasik Azure portalı aaaKnown ağlarda | Microsoft Docs"
description: "Bilinen ağları yapılandırarak, birden çok coğrafyadan oturum ve şüpheli etkinlik raporları ile birlikte IP adreslerinden gerçekleştirilen oturum hello dahil, kuruluşunuzun sahip olduğu IP adreslerine sahip olmasına önleyebilirsiniz."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a><span data-ttu-id="0d8ce-103">Bilinen ağlar</span><span class="sxs-lookup"><span data-stu-id="0d8ce-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d8ce-104">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="0d8ce-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="0d8ce-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="0d8ce-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="0d8ce-106">Azure Active Directory'nin erişim ve kullanım raporları toogain görünürlük hello bütünlüğü ve güvenlik kuruluşunuzun dizininin kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d8ce-106">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="0d8ce-107">Bu bilgileri kullanarak bir dizin yönetici böylece bunlar yeterli bu riskleri toomitigate planlayabilirsiniz olası güvenlik riskleri burada bulunan daha iyi belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d8ce-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="0d8ce-108">Merhaba mümkün olan "*birden çok coğrafyadan oturum*"ve"*oturum açmalar IP adreslerinden şüpheli etkinliğe sahip*" raporları yanlış bayrak tarafından gerçekten ait IP adresleri, Kuruluş.</span><span class="sxs-lookup"><span data-stu-id="0d8ce-108">It is possible that hello “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="0d8ce-109">Örneğin, gerçekleşebilir zaman:</span><span class="sxs-lookup"><span data-stu-id="0d8ce-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="0d8ce-110">Bir kullanıcı, Boston ofisinizde uzaktan tooyour veri merkezinde San Francisco Tetikleyicileri hello "Birden çok coğrafyadan oturum açmalar" rapor imzaladığı</span><span class="sxs-lookup"><span data-stu-id="0d8ce-110">A user in your Boston office has signed in remotely tooyour data center in San Francisco triggers hello “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="0d8ce-111">Bir kullanıcı, kuruluşunuzun toosign açma birkaç kez yanlış parola Tetikleyicileri hello "Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum" rapor ile çalışır</span><span class="sxs-lookup"><span data-stu-id="0d8ce-111">A user of your organization tries toosign-on several times with an incorrect password triggers hello “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="0d8ce-112">Bu oluşturma yanıltıcı güvenlik çalışmalarından tooprevent raporları, bilinen IP adres aralıkları toohello listesi, kuruluşunuzun ortak IP adresinin eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d8ce-112">tooprevent these cases from generating misleading security reports, you should add known IP address ranges toohello list of your organization's public IP address.</span></span>    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a><span data-ttu-id="0d8ce-113">tooadd kuruluşunuzun ortak IP adresi aralıkları, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0d8ce-113">tooadd your organization’s public IP address ranges, perform hello following steps:</span></span>

1. <span data-ttu-id="0d8ce-114">Oturum açma toohello [Azure Yönetim Portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0d8ce-114">Sign-on toohello [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="0d8ce-115">Merhaba sol bölmede **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d8ce-115">In hello left pane, click **Active Directory**.</span></span> 

    ![Bilinen ağlar](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="0d8ce-117">Merhaba, **Directory** sekmesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="0d8ce-117">In hello **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="0d8ce-118">Hello içinde hello üst menüsünde **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="0d8ce-118">In hello menu on hello top, click **Configure**.</span></span> 

    ![Bilinen ağlar](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="0d8ce-120">Merhaba yapılandırma sekmesinde çok Git**, kuruluşların ortak IP adresi aralıkları**</span><span class="sxs-lookup"><span data-stu-id="0d8ce-120">On hello Configure tab, go too**your organizations public IP address ranges**</span></span> 

    ![Bilinen ağlar](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="0d8ce-122">Tıklatın **bilinen IP adres aralıklarını ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="0d8ce-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="0d8ce-123">Görüntülenen hello iletişim kutusunda, adres aralıklarını ekleyin ve işiniz bittiğinde hello onay düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0d8ce-123">Add your address ranges in hello dialog box that appears, and then click hello check button  when you are done.</span></span> 

    ![Bilinen ağlar](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="0d8ce-125">**Ek kaynaklar:**</span><span class="sxs-lookup"><span data-stu-id="0d8ce-125">**Additional resources:**</span></span>

* [<span data-ttu-id="0d8ce-126">Erişim ve kullanım raporlarınızı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="0d8ce-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="0d8ce-127">Şüpheli etkinliğe sahip IP adreslerinden oturum açmalar</span><span class="sxs-lookup"><span data-stu-id="0d8ce-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="0d8ce-128">Birden çok coğrafyadan oturum</span><span class="sxs-lookup"><span data-stu-id="0d8ce-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

