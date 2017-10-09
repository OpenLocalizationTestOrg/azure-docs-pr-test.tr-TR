---
title: "Azure AD tooan galeri uygulama sağlama aaaUser olan alma saat veya daha fazla bilgi | Microsoft Docs"
description: "Nasıl neden tooyour uygulama sağlama, uzun sürüyor çıkışı toofind bekleniyor"
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
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="feea5-103">Azure AD tooan galeri uygulama sağlama alma saat veya daha fazla kullanıcıdır</span><span class="sxs-lookup"><span data-stu-id="feea5-103">User provisioning tooan Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="feea5-104">Önce bir uygulama için otomatik sağlama etkinleştirirken, hello ilk eşitleme herhangi bir yere hello boyutunu hello Azure AD dizini ve hello sayısı, kullanıcı sağlama kapsamında bağlı olarak 20 dakika tooseveral saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="feea5-104">When first enabling automatic provisioning for an application, hello initial sync can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="feea5-105">Sonraki eşitlemeler hello ilk eşitleme sonra daha hızlı olması hizmet sağlama hello sonraki eşitlemeler performansını iyileştirme hello ilk eşitleme sonrasında her iki sistemle hello durumunu temsil filigranlar depolar.</span><span class="sxs-lookup"><span data-stu-id="feea5-105">Subsequent syncs after hello initial sync be faster, as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-tooimprove-provisioning-performance"></a><span data-ttu-id="feea5-106">Nasıl tooimprove performans sağlama</span><span class="sxs-lookup"><span data-stu-id="feea5-106">How tooimprove provisioning performance</span></span>

<span data-ttu-id="feea5-107">Merhaba ilk eşitleme birkaç saat sürüyorsa tooimprove performans yapabileceğiniz bir şey vardır:</span><span class="sxs-lookup"><span data-stu-id="feea5-107">If hello initial sync is taking more than a few hours, there is one thing you can do tooimprove performance:</span></span>

-   <span data-ttu-id="feea5-108">**Kullanıcı kapsam filtreleri.**</span><span class="sxs-lookup"><span data-stu-id="feea5-108">**User scoping filters.**</span></span> <span data-ttu-id="feea5-109">Kapsam filtreleri sağlama hizmeti ayıklar Azure AD'den belirli öznitelik değerlerine göre kullanıcılar filtreleyerek hello toofine ayarlama hello veri izin verin.</span><span class="sxs-lookup"><span data-stu-id="feea5-109">Scoping filters allow you toofine tune hello data that hello provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="feea5-110">Kapsam belirleme filtreleri ile ilgili daha fazla bilgi için bkz: [kapsam belirleme filtreleri ile öznitelik tabanlı uygulama sağlama](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="feea5-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="feea5-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="feea5-111">Next steps</span></span>
[<span data-ttu-id="feea5-112">Kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS Azure Active Directory ile uygulamaları otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="feea5-112">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

