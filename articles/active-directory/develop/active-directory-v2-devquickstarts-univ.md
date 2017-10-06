---
title: aaaAzure AD v2.0 Windows Evrensel uygulama | Microsoft Docs
description: "Nasıl toobuild bir Windows Evrensel uygulaması, kullanıcıların hem kişisel Microsoft Account oturum açtığında ve iş veya Okul hesapları."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: d2c92b65-3c1d-46d1-81c8-88f32f6b2c4b
ms.service: active-directory
ms.workload: identity
ms.topic: article
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.date: 02/20/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 49b26c74fa5a76664c3229256c9bd128563b830c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-universal-app-using-hello-v20-endpoint"></a><span data-ttu-id="9054c-103">Merhaba v2.0 uç kullanarak oturum açma tooa Windows Evrensel uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="9054c-103">Add sign-in tooa Windows Universal app using hello v2.0 endpoint</span></span>
  <span data-ttu-id="9054c-104">Windows Evrensel uygulamaları için hızlı başlangıç Öğreticisi Hello oldukça hazır değil... Geri yakında & arama güncelleştirmelerini denetimi @AzureAD Twitter'da.</span><span class="sxs-lookup"><span data-stu-id="9054c-104">hello quick-start tutorial for Windows Universal apps isn't quite ready... Check back soon & look for updates from @AzureAD on Twitter.</span></span>

> [!NOTE]
> <span data-ttu-id="9054c-105">Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9054c-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="9054c-106">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9054c-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

    ## Get security updates for our products

<span data-ttu-id="9054c-107">Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="9054c-107">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

