---
title: "PingAccess kullanmak için bir uygulama proxy'si uygulamasının nasıl yapılandırılacağını | Microsoft Docs"
description: "Üstbilgi tabanlı kimlik doğrulaması kullanan uygulamalar için uygulama proxy'si yararları genişletmek için PingAccess kullanmayı öğrenin"
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
ms.openlocfilehash: a9da67373465cebbdbecae5c8fb8bd0a0ee3c171
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application-to-use-pingaccess"></a><span data-ttu-id="0ade8-103">Uygulama proxy'si uygulamaya PingAccess kullanmak için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0ade8-103">How to configure an Application Proxy application to use PingAccess</span></span>

<span data-ttu-id="0ade8-104">PingAccess şimdi bizim işbirliğiyle üstbilgi tabanlı kimlik doğrulaması kullanan uygulamalar için uygulama proxy'si yararları genişletmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0ade8-104">Our collaboration with PingAccess now allows you to extend the benefits of Application Proxy to applications using header-based authentication.</span></span> <span data-ttu-id="0ade8-105">Uygulamalarınızı üstbilgileri kullanmıyorsanız bkz bizim [çoklu oturum açma belgelerine](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) diğer seçenekler hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="0ade8-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="0ade8-106">Adımlar ve önerilen belgeler genel bakış</span><span class="sxs-lookup"><span data-stu-id="0ade8-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="0ade8-107">Bir uygulama ile PingAccess yapılandırmak için dört adım vardır:</span><span class="sxs-lookup"><span data-stu-id="0ade8-107">To configure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="0ade8-108">Uygulama proxy'si bağlayıcıları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0ade8-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="0ade8-109">Azure AD uygulama proxy'si uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ade8-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="0ade8-110">Karşıdan & PingAccess yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0ade8-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="0ade8-111">İçinde PingAccess uygulamaları yapılandır</span><span class="sxs-lookup"><span data-stu-id="0ade8-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="0ade8-112">Bu adımların her biri hakkında daha fazla bilgi için bkz: bizim [çoklu oturum açma üstbilgileri belgelerine](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span><span class="sxs-lookup"><span data-stu-id="0ade8-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
