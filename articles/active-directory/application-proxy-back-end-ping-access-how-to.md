---
title: Uygulama proxy'si uygulama toouse PingAccess aaaHow tooconfigure | Microsoft Docs
description: "Nasıl toouse PingAccess tooextend hello üstbilgi tabanlı kimlik doğrulaması kullanarak uygulama proxy'si tooapplications avantajları öğrenin"
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
ms.openlocfilehash: fa4c9747b7bf5a135425be270e4f7eadf95248fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-pingaccess"></a><span data-ttu-id="a6988-103">Nasıl tooconfigure uygulama proxy'si uygulama toouse PingAccess</span><span class="sxs-lookup"><span data-stu-id="a6988-103">How tooconfigure an Application Proxy application toouse PingAccess</span></span>

<span data-ttu-id="a6988-104">PingAccess şimdi bizim işbirliğiyle tooextend hello üstbilgi tabanlı kimlik doğrulaması kullanarak uygulama proxy'si tooapplications yararları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6988-104">Our collaboration with PingAccess now allows you tooextend hello benefits of Application Proxy tooapplications using header-based authentication.</span></span> <span data-ttu-id="a6988-105">Uygulamalarınızı üstbilgileri kullanmıyorsanız bkz bizim [çoklu oturum açma belgelerine](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) diğer seçenekler hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a6988-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="a6988-106">Adımlar ve önerilen belgeler genel bakış</span><span class="sxs-lookup"><span data-stu-id="a6988-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="a6988-107">bir uygulama ile PingAccess, tooconfigure dört adım vardır:</span><span class="sxs-lookup"><span data-stu-id="a6988-107">tooconfigure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="a6988-108">Uygulama proxy'si bağlayıcıları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a6988-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="a6988-109">Azure AD uygulama proxy'si uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6988-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="a6988-110">Karşıdan & PingAccess yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a6988-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="a6988-111">İçinde PingAccess uygulamaları yapılandır</span><span class="sxs-lookup"><span data-stu-id="a6988-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="a6988-112">Bu adımların her biri hakkında daha fazla bilgi için bkz: bizim [çoklu oturum açma üstbilgileri belgelerine](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span><span class="sxs-lookup"><span data-stu-id="a6988-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
