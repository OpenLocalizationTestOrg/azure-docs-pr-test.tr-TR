---
title: "Azure AD v2.0 Windows Evrensel uygulaması | Microsoft Docs"
description: "Hem kişisel Microsoft Account oturum kullanıcılar oturum açtığında bir Windows Evrensel uygulamasının nasıl oluşturulacağını ve iş veya Okul hesapları."
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
ms.openlocfilehash: 369802f1a42b8720aa730d5ac7e5576ed20eeddf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-universal-app-using-the-v20-endpoint"></a><span data-ttu-id="bdd38-103">Oturum açma v2.0 uç noktası kullanarak bir Windows Evrensel uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="bdd38-103">Add sign-in to a Windows Universal app using the v2.0 endpoint</span></span>
  <span data-ttu-id="bdd38-104">Windows Evrensel uygulamaları için hızlı başlangıç Öğreticisi oldukça hazır değil... Geri yakında & arama güncelleştirmelerini denetimi @AzureAD Twitter'da.</span><span class="sxs-lookup"><span data-stu-id="bdd38-104">The quick-start tutorial for Windows Universal apps isn't quite ready... Check back soon & look for updates from @AzureAD on Twitter.</span></span>

> [!NOTE]
> <span data-ttu-id="bdd38-105">Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="bdd38-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="bdd38-106">V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="bdd38-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

    ## Get security updates for our products

<span data-ttu-id="bdd38-107">[Bu sayfayı](https://technet.microsoft.com/security/dd252948) ziyaret ederek ve Güvenlik Önerisi Uyarılarına abone olarak güvenlik olaylarının ne zaman ortaya çıkacağı hakkında bildirimleri almanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="bdd38-107">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

