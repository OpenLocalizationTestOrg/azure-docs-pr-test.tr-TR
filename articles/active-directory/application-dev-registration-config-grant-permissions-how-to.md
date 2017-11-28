---
title: "aaaHow toogrant izinleri tooa özel geliştirilmiş uygulama | Microsoft Docs"
description: "Nasıl toogrant izinleri tooyour özel geliştirilmiş uygulama kullanarak hello Azure AD portalı veya bir URL parametresi"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a><span data-ttu-id="5004f-103">Nasıl toogrant izinleri tooa özel geliştirilmiş uygulama</span><span class="sxs-lookup"><span data-stu-id="5004f-103">How toogrant permissions tooa custom-developed application</span></span>

<span data-ttu-id="5004f-104">Toogrant izin erken önlem uygulamanıza istediğiniz veya bir hata, tooan uygulama rıza değil, çalışan, aşağıdaki adımları deneyin.</span><span class="sxs-lookup"><span data-stu-id="5004f-104">If you want toogrant consent preemptively on your app or are running into an error that you have not consented tooan app, try these steps below.</span></span>

## <a name="how-tooperform-admin-consent-for-your-application"></a><span data-ttu-id="5004f-105">Nasıl uygulamanız için yönetici onayı tooperform</span><span class="sxs-lookup"><span data-stu-id="5004f-105">How tooperform Admin Consent for your application</span></span>

<span data-ttu-id="5004f-106">Bu, kuruluşunuzdaki tüm kullanıcılar için onay toohello uygulama verme hello etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="5004f-106">This has hello effect of granting consent toohello application for all users in your organization.</span></span>

1. <span data-ttu-id="5004f-107">Toohello gidin **uygulama kayıtlar** dikey olarak bir **genel yönetici**seçeneğini belirleyip hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="5004f-107">Navigate toohello **App Registrations** blade as a **global administrator**, then select hello app.</span></span>

2. <span data-ttu-id="5004f-108">Seçin **gerekli izinler**ve son olarak, hello isabet **izinler** hello dikey penceresinde hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5004f-108">Select **Required Permissions**, and finally hit hello **Grant Permissions** button at hello top of hello blade.</span></span>

<span data-ttu-id="5004f-109">Alternatif olarak, bir istek çok oluşturabileceğiniz*login.microsoftonline.com* uygulama yapılandırmaları ile ve üzerinde ilave *& komut istemi Yönetim =\_onayı*.</span><span class="sxs-lookup"><span data-stu-id="5004f-109">Alternatively, you can construct a request too*login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="5004f-110">Yönetici kimlik bilgileriyle oturum sonra hello uygulama tüm kullanıcılar için izin verildi.</span><span class="sxs-lookup"><span data-stu-id="5004f-110">After signing in with admin credentials, hello app has been granted consent for all users.</span></span>

## <a name="how-tooforce-user-consent-for-your-application"></a><span data-ttu-id="5004f-111">Nasıl tooforce kullanıcı onayı uygulamanız için</span><span class="sxs-lookup"><span data-stu-id="5004f-111">How tooforce User Consent for your application</span></span>

* <span data-ttu-id="5004f-112">Kimlik doğrulama istekleri ekleme *& sor onay =* kimlik doğrulaması her zaman son kullanıcıların tooconsent gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5004f-112">Append onto auth requests *&prompt=consent* which require end users tooconsent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5004f-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5004f-113">Next steps</span></span>

[<span data-ttu-id="5004f-114">İzin ve tümleştirme uygulamalarını tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="5004f-114">Consent and Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="5004f-115">İzin ve adının Azuread'i v2.0 için uygulamalar Yakınsanan</span><span class="sxs-lookup"><span data-stu-id="5004f-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="5004f-116">Azuread'i StackOverflow</span><span class="sxs-lookup"><span data-stu-id="5004f-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
