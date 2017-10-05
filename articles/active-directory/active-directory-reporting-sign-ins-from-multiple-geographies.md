---
title: "Birden çok coğrafyadan oturum"
description: "Farklı bölgelerdeki ve bileşenler kullanıcının bu bölgeler arasında Seyahat etmiş olması imkansız yapar oturum arasındaki süre kaynaklanan için iki oturum kullanıcıları gösteren bir rapor görüldü."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a><span data-ttu-id="74ca8-103">Birden çok coğrafyadan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="74ca8-103">Sign-ins from multiple geographies</span></span>
<span data-ttu-id="74ca8-104">Bu rapor, başarılı oturum açma işlemleri burada iki oturum açma işlemleri farklı bölgelerden kaynaklanacak şekilde görünen ve oturum açma işlemleri arasındaki süre kullanıcının bu bölgeler arasında Seyahat etmiş mümkün kılar, bir kullanıcıdan içerir.</span><span class="sxs-lookup"><span data-stu-id="74ca8-104">This report includes successful sign-ins from a user where two sign-ins appeared to originate from different regions and the time between the sign-ins makes it impossible for the user to have traveled between those regions.</span></span> <span data-ttu-id="74ca8-105">Olası nedenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="74ca8-105">Possible causes include:</span></span>

* <span data-ttu-id="74ca8-106">Kullanıcı parolalarını diğer kullanıcılarla paylaşma</span><span class="sxs-lookup"><span data-stu-id="74ca8-106">User is sharing their password with other users</span></span>
* <span data-ttu-id="74ca8-107">Kullanıcı oturum açma için bir web tarayıcısı başlatmak için bir Uzak Masaüstü'nü kullanma</span><span class="sxs-lookup"><span data-stu-id="74ca8-107">User is using a remote desktop to launch a web browser for sign-in</span></span>
* <span data-ttu-id="74ca8-108">Bir bilgisayar korsanının bir kullanıcı hesabı için farklı bir ülkeden oturum açtığı</span><span class="sxs-lookup"><span data-stu-id="74ca8-108">A hacker has signed in to the account of a user from a different country</span></span>
* <span data-ttu-id="74ca8-109">Kullanıcı bir VPN ya da proxy kullanma</span><span class="sxs-lookup"><span data-stu-id="74ca8-109">User is using a VPN or proxy</span></span>
* <span data-ttu-id="74ca8-110">Kullanıcı birden çok cihazı aynı zamanda, bir masaüstü ve cep telefonu gibi oturum ve cep telefonu IP adresini olağandışıdır.</span><span class="sxs-lookup"><span data-stu-id="74ca8-110">User is signed in from multiple devices at the same time, such as a desktop and a mobile phone, and the IP address of the mobile phone is unusual.</span></span>

<span data-ttu-id="74ca8-111">Bu rapor sonuçlarını Bu bölgeler arasında başarılı oturum açma olayları, oturum açma işlemleri, burada oturum açma işlemleri kaynaklanan görüldü bölgeler ve tahmini seyahat saat arasındaki zaman birlikte gösterilir.</span><span class="sxs-lookup"><span data-stu-id="74ca8-111">Results from this report will show you the successful sign-in events, together with the time between the sign-ins, the regions where the sign-ins appeared to originate from, and the estimated travel time between those regions.</span></span> <span data-ttu-id="74ca8-112">Gösterilen seyahat zaman sadece bir tahmindir ve konumları arasında gerçek seyahat zamandan farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="74ca8-112">The travel time shown is only an estimate and may be different from the actual travel time between the locations.</span></span>

![Birden çok coğrafyadan oturum](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)

