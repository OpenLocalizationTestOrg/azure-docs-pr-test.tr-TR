---
title: "aaaSign birden çok hatadan sonra bileşenleri"
description: "Birden çok ardışık oturum girişimlerinde başarısız olduktan sonra başarıyla açmış kullanıcılar gösteren bir rapor."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="cf48c-103">Birden çok hatadan sonra gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="cf48c-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="cf48c-104">Bu rapor, birden çok ardışık oturum girişimlerinde başarısız olduktan sonra başarıyla açmış kullanıcılar gösterir.</span><span class="sxs-lookup"><span data-stu-id="cf48c-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="cf48c-105">Olası nedenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cf48c-105">Possible causes include:</span></span>

* <span data-ttu-id="cf48c-106">Kullanıcı kendi parolasını unutursa</span><span class="sxs-lookup"><span data-stu-id="cf48c-106">User had forgotten their password</span></span></li><li><span data-ttu-id="cf48c-107">Deneme yanılma saldırısı tahmin başarılı bir parola hello kurbanı kullanıcıdır</span><span class="sxs-lookup"><span data-stu-id="cf48c-107">User is hello victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="cf48c-108">Bu rapor sonuçlarından yapılan art arda başarısız oturum açma denemeleri önceki toohello başarılı oturum açma sayısı hello ve ilişkili bir zaman damgası hello ilk başarılı oturum açma gösterir.</span><span class="sxs-lookup"><span data-stu-id="cf48c-108">Results from this report will show you hello number of consecutive failed sign-in attempts made prior toohello successful sign-in and a timestamp associated with hello first successful sign-in.</span></span>

<span data-ttu-id="cf48c-109">**Rapor ayarları**: hello raporda görüntülenen gerçekleşmelidir denemesinden hello minimum art arda başarısız oturum sayısını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf48c-109">**Report Settings**: You can configure hello minimum number of consecutive failed sign in attempts that must occur before it can be displayed in hello report.</span></span> <span data-ttu-id="cf48c-110">Ayarlamak toothis olan değişiklik yaptığınızda bu değişiklikleri uygulanan tooany başarısız mevcut olmayacağını önemli toonote şu anda mevcut raporda görünmesini bileşenler oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cf48c-110">When you make changes toothis setting it is important toonote that these changes will not be applied tooany existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="cf48c-111">Ancak, kullanıcılar uygulanan tooall gelecekteki oturum açma işlemleri. Değişiklikleri toothis raporu, yalnızca lisanslı yöneticileri tarafından yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="cf48c-111">However, they will be applied tooall future sign-ins. Changes toothis report can only be made by licensed admins.</span></span>

![Birden çok hatadan sonra oturum açmalar](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

