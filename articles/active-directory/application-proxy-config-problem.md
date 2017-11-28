---
title: "Uygulama proxy'si uygulama oluşturma aaaProblem | Microsoft Docs"
description: "Nasıl tootroubleshoot hello Azure AD yönetim portalında uygulama proxy'si uygulama oluşturmayı sorunları"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="5a1a0-103">Uygulama proxy'si uygulama oluşturma sorunu</span><span class="sxs-lookup"><span data-stu-id="5a1a0-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="5a1a0-104">Aşağıda bazı hello yaygın sorunların çoğunu kişiler yüz yeni bir uygulama proxy'si uygulama oluştururken verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5a1a0-104">Below are some of hello common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="5a1a0-105">Önerilen belgeler</span><span class="sxs-lookup"><span data-stu-id="5a1a0-105">Recommended documents</span></span> 

<span data-ttu-id="5a1a0-106">Merhaba Yönetici portalı üzerinden uygulama proxy'si uygulama oluşturma hakkında daha fazla toolearn bkz [Azure AD uygulama proxy'si ile uygulama yayımlama](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="5a1a0-106">toolearn more about creating an Application Proxy application through hello Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="5a1a0-107">Belge hello adımlarını izleyerek ve Merhaba uygulaması oluşturulurken bir hata alma, hello hata ayrıntıları için bilgi ve öneriler nasıl toofix hello uygulama için bkz.</span><span class="sxs-lookup"><span data-stu-id="5a1a0-107">If you are following hello steps in that document and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="5a1a0-108">Çoğu hata iletileri önerilen bir düzeltmeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="5a1a0-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-toocheck"></a><span data-ttu-id="5a1a0-109">Belirli bir işlemi toocheck</span><span class="sxs-lookup"><span data-stu-id="5a1a0-109">Specific things toocheck</span></span>

<span data-ttu-id="5a1a0-110">tooavoid sık karşılaşılan doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="5a1a0-110">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="5a1a0-111">Bir yönetici izni toocreate uygulama proxy'si uygulama ile</span><span class="sxs-lookup"><span data-stu-id="5a1a0-111">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="5a1a0-112">Merhaba İç URL benzersizdir</span><span class="sxs-lookup"><span data-stu-id="5a1a0-112">hello internal URL is unique</span></span>

-   <span data-ttu-id="5a1a0-113">Merhaba dış URL benzersizdir</span><span class="sxs-lookup"><span data-stu-id="5a1a0-113">hello external URL is unique</span></span>

-   <span data-ttu-id="5a1a0-114">http veya https URL'leri başlangıcı hello ve sonunda bir "/"</span><span class="sxs-lookup"><span data-stu-id="5a1a0-114">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="5a1a0-115">Merhaba URL bir etki alanı adı ve IP adresi olmalıdır</span><span class="sxs-lookup"><span data-stu-id="5a1a0-115">hello URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="5a1a0-116">Merhaba uygulaması oluşturduğunuzda hello sağ üst köşedeki hello hata iletisi görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5a1a0-116">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="5a1a0-117">Merhaba bildirim simgesine toosee hello hata iletileri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a1a0-117">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Bildirim istemi](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="5a1a0-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5a1a0-119">Next steps</span></span>
[<span data-ttu-id="5a1a0-120">Hello Azure portalında uygulama ara sunucusunu etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5a1a0-120">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
