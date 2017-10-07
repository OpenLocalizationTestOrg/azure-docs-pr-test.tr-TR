---
title: "aaaCloud Proxy Hizmetleri için uygulama bulma kayıt defteri ayarları | Microsoft Docs"
description: "Merhaba amacı, bu konuda, hello sizinle adımları tooprovide tooperform tooset hello gerekli bağlantı noktası hello Cloud App Discovery Aracısı çalıştıran hello bilgisayarlarda gerekir ' dir."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="a95fe-103">Proxy Hizmetleri için cloud App Discovery kayıt defteri ayarları</span><span class="sxs-lookup"><span data-stu-id="a95fe-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="a95fe-104">Varsayılan olarak, hello Cloud App Discovery Aracısı yapılandırılmış toouse yalnızca başlangıç bağlantı noktası 80 veya 443 ' dir.</span><span class="sxs-lookup"><span data-stu-id="a95fe-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="a95fe-105">Cloud App Discovery, özel bir bağlantı noktası (80 ne 443) kullanarak bir proxy sunucusu olan bir ortamda yüklemeyi planlıyorsanız, aracıları toouse tooconfigure gereken Bu bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="a95fe-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="a95fe-106">Merhaba yapılandırma, bir kayıt defteri anahtarı temel alır.</span><span class="sxs-lookup"><span data-stu-id="a95fe-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="a95fe-107">Merhaba amacı, bu konuda, hello sizinle adımları tooprovide tooperform tooset hello gerekli bağlantı noktası hello Cloud App Discovery Aracısı çalıştıran hello bilgisayarlarda gerekir ' dir.</span><span class="sxs-lookup"><span data-stu-id="a95fe-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="a95fe-108">**Merhaba Cloud App Discovery Aracısı çalıştıran hello bilgisayar tarafından kullanılan toomodify hello bağlantı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a95fe-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="a95fe-109">Merhaba Kayıt Defteri Düzenleyicisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="a95fe-109">Start hello registry editor.</span></span> <br> ![Çalıştırın](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="a95fe-111">Gezinme tooor hello aşağıdaki kayıt defteri anahtarı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a95fe-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="a95fe-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud uygulama Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="a95fe-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="a95fe-113">Yeni bir **çok dizeli** adlı değeri **bağlantı noktalarını**.</span><span class="sxs-lookup"><span data-stu-id="a95fe-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="a95fe-114">![Yeni](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="a95fe-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="a95fe-115">tooopen hello **Çoklu Dize Düzenle** iletişim kutusunda, başlangıç bağlantı noktası değeri çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a95fe-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="a95fe-116">Merhaba değer veri metin kutusuna, değerleri aşağıdaki hello yazın ve kuruluşunuz tarafından kullanılan tüm özel bağlantı noktalarını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a95fe-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="a95fe-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="a95fe-117">
   **80**</span></span> <br><span data-ttu-id="a95fe-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="a95fe-118">
   **8080**</span></span> <br><span data-ttu-id="a95fe-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="a95fe-119">
   **8118**</span></span> <br><span data-ttu-id="a95fe-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="a95fe-120">
   **8888**</span></span> <br><span data-ttu-id="a95fe-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="a95fe-121">
   **81**</span></span> <br><span data-ttu-id="a95fe-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="a95fe-122">
   **12080**</span></span> <br><span data-ttu-id="a95fe-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="a95fe-123">
**6999**</span></span> <br><span data-ttu-id="a95fe-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="a95fe-124">
**30606**</span></span> <br><span data-ttu-id="a95fe-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="a95fe-125">
**31595**</span></span> <br><span data-ttu-id="a95fe-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="a95fe-126">
**4080**</span></span> <br><span data-ttu-id="a95fe-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="a95fe-127">
**443**</span></span> <br><span data-ttu-id="a95fe-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="a95fe-128">
**1110**</span></span> <br><br><span data-ttu-id="a95fe-129">
![Çoklu Dize Düzenle](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="a95fe-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="a95fe-130">Tıklatın **Tamam** tooclose hello **Çoklu Dize Düzenle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a95fe-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="a95fe-131">**Ek Kaynaklar**</span><span class="sxs-lookup"><span data-stu-id="a95fe-131">**Additional Resources**</span></span>

* [<span data-ttu-id="a95fe-132">Nasıl ı Kuruluşum içinde kullanılan onaylanmamış bulut uygulamaları bulabilir</span><span class="sxs-lookup"><span data-stu-id="a95fe-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

