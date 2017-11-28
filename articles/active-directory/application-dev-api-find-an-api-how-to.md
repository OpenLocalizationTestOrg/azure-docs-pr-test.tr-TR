---
title: "aaaHow toofind özel geliştirilmiş bir uygulama için gereken belirli bir API | Microsoft Docs"
description: "Azure AD uygulaması tooaccess belirli bir API'yi kendi özel gereksinim tooconfigure hello izinleri nasıl geliştirilmiş"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="a838e-103">Nasıl toofind belirli bir API özel geliştirilmiş bir uygulama için gerekli</span><span class="sxs-lookup"><span data-stu-id="a838e-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="a838e-104">Erişim tooAPIs erişim kapsamları ve rol yapılandırılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a838e-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="a838e-105">Tooconfigure erişim kapsamları ve rolleri, kaynak uygulama web API'leri tooclient uygulamalarınızı tooexpose istiyorsanız Merhaba API gerekir.</span><span class="sxs-lookup"><span data-stu-id="a838e-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="a838e-106">Bir istemci uygulama tooaccess web API'si istiyorsanız tooconfigure izinleri tooaccess hello API hello uygulama kaydı gerekir.</span><span class="sxs-lookup"><span data-stu-id="a838e-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="a838e-107">Bir kaynak uygulama tooexpose web API'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a838e-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="a838e-108">Web API, kullanıma zaman hello API hello görüntülenmesi **bir API seçin** listesinde izinleri tooan uygulama kaydı eklerken.</span><span class="sxs-lookup"><span data-stu-id="a838e-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="a838e-109">tooadd erişim kapsamları adımları özetlenen hello [erişim ekleme kapsamları tooyour kaynak uygulama](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="a838e-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="a838e-110">Bir istemci uygulama tooaccess web API'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a838e-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="a838e-111">İzinleri tooyour uygulama kaydı eklediğinizde, şunları yapabilirsiniz **API erişim Ekle** tooexposed web API'leri.</span><span class="sxs-lookup"><span data-stu-id="a838e-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="a838e-112">tooaccess web API'leri, özetlenen hello adımları [kimlik bilgileri veya izinleri tooaccess web API'leri eklemek](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="a838e-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a838e-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a838e-113">Next steps</span></span>

-   [<span data-ttu-id="a838e-114">Uygulamaları Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="a838e-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="a838e-115">Hello Azure Active Directory Uygulama bildirimini anlama</span><span class="sxs-lookup"><span data-stu-id="a838e-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


