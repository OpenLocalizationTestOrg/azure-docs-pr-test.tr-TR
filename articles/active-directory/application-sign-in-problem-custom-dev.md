---
title: "tooan özel geliştirilmiş uygulamada imzalama aaaProblems | Microsoft Docs"
description: "Azure AD ile geliştirilen bir uygulamaya mümkün toosign toonot neden olabilecek yaygın rrors olabilir"
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
ms.openlocfilehash: cc302e68ae6c129b74387c6fc5ba4fb45ccb8fb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-custom-developed-application"></a><span data-ttu-id="cf3a4-103">Tooan özel geliştirilmiş uygulamada oturum sorunları</span><span class="sxs-lookup"><span data-stu-id="cf3a4-103">Problems signing in tooan custom-developed application</span></span>

<span data-ttu-id="cf3a4-104">Toonot mümkün toosign uygulamaya olması neden olabilecek çeşitli hatalar yoktur.</span><span class="sxs-lookup"><span data-stu-id="cf3a4-104">There are several errors that could be causing you toonot be able toosign into an app.</span></span> <span data-ttu-id="cf3a4-105">Bu sorunu değinilmektedir hello büyük yanlış yapılandırılmış uygulamaları nedenidir.</span><span class="sxs-lookup"><span data-stu-id="cf3a4-105">hello biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-too-misconfigured-apps"></a><span data-ttu-id="cf3a4-106">İlgili hatalarla ilgili çok yanlış yapılandırılmış uygulamalar</span><span class="sxs-lookup"><span data-stu-id="cf3a4-106">Errors related too misconfigured apps</span></span>

* <span data-ttu-id="cf3a4-107">Uygulamanızda sahip hello portalında hem hello yapılandırmalarla eşleşen doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cf3a4-107">Verify both hello configurations in hello portal match what you have in your app.</span></span> <span data-ttu-id="cf3a4-108">Özellikle, istemci/uygulama kimliği, yanıt URL'leri, istemci parolaları/anahtarları ve uygulama kimliği URI'si karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="cf3a4-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="cf3a4-109">Erişim tooin kodu hello yapılandırılmış hello izinlerle isteyen hello kaynak karşılaştırmak **gerekli kaynakları** yapılandırdığınız sekmesini toomake kaynakları yalnızca istek emin.</span><span class="sxs-lookup"><span data-stu-id="cf3a4-109">Compare hello resource you’re requesting access tooin code with hello configured permissions in hello **Required Resources** tab toomake sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="cf3a4-110">Bkz: [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) benzer hatalar veya sorunlar için.</span><span class="sxs-lookup"><span data-stu-id="cf3a4-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf3a4-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf3a4-111">Next steps</span></span>

[<span data-ttu-id="cf3a4-112">Azure AD Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="cf3a4-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="cf3a4-113">İzin ve tümleştirme uygulamalarını tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="cf3a4-113">Consent and Integrating Apps tooAzure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="cf3a4-114">Onay ve Azure AD v2.0 için adının uygulamaları Yakınsanan</span><span class="sxs-lookup"><span data-stu-id="cf3a4-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="cf3a4-115">Azure AD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="cf3a4-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
