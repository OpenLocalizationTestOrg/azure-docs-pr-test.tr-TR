---
title: "aaaAzure AD Microsoft Cloud Almanya Bağlan"
description: "Azure AD Connect, şirket içi dizinlerinizi Azure Active Directory ile tümleştirir. Bu, Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik Azure AD ile tümleşik tooprovide sağlar."
keywords: "Giriş tooAzure AD Connect, Azure AD Connect'e genel bakış, Azure AD Connect nedir active directory, Almanya, siyah orman yükleme"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="0dd07-105">Microsoft Bulut Almanya’da Azure AD Connect - Genel Önizleme</span><span class="sxs-lookup"><span data-stu-id="0dd07-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="0dd07-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="0dd07-106">Introduction</span></span>
<span data-ttu-id="0dd07-107">Azure AD Connect, şirket içi Active Directory’niz ile Azure Active Directory arasında eşitleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="0dd07-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="0dd07-108">Şu anda, birçok hello senaryolarda [Microsoft Cloud Almanya](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) hello operatör tarafından yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dd07-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="0dd07-109">Microsoft Cloud Almanya kullanırken hello aşağıdakilerin bilincinde olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0dd07-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="0dd07-110">Merhaba aşağıdaki URL'ler eşitleme toooccur için bir proxy sunucusu başarıyla açılması gerekir:</span><span class="sxs-lookup"><span data-stu-id="0dd07-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="0dd07-111">*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="0dd07-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="0dd07-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="0dd07-112">*.windows.net</span></span>
  * * <span data-ttu-id="0dd07-113">Sertifika İptal Listeleri</span><span class="sxs-lookup"><span data-stu-id="0dd07-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="0dd07-114">Tooyour Azure AD dizininde oturum açtığınızda hello onmicrosoft.de etki alanındaki bir hesabı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dd07-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="0dd07-115">özellikler aşağıdaki hello kullanılabilir değil:</span><span class="sxs-lookup"><span data-stu-id="0dd07-115">hello following features are not available:</span></span>
  * <span data-ttu-id="0dd07-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="0dd07-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="0dd07-117">Otomatik güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="0dd07-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="0dd07-118">İndir</span><span class="sxs-lookup"><span data-stu-id="0dd07-118">Download</span></span>
<span data-ttu-id="0dd07-119">Azure AD Connect hello portalındaki hello Azure AD Connect dikey penceresinden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dd07-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="0dd07-120">Merhaba toolocate hello Azure AD Connect dikey aşağıdaki yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="0dd07-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="0dd07-121">Hello Azure AD Connect dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="0dd07-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="0dd07-122">Toohello Azure portalında oturum açtıktan sonra aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="0dd07-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="0dd07-123">TooBrowse gidin</span><span class="sxs-lookup"><span data-stu-id="0dd07-123">Go tooBrowse</span></span>
2. <span data-ttu-id="0dd07-124">Azure Active Directory'yi seçin</span><span class="sxs-lookup"><span data-stu-id="0dd07-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="0dd07-125">Azure AD Connect'i seçin</span><span class="sxs-lookup"><span data-stu-id="0dd07-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="0dd07-126">Merhaba şunları görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0dd07-126">You should see hello following:</span></span>

![Azure AD Connect Dikey Penceresi](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="0dd07-128">Merhaba aşağıdaki tabloda hello dikey penceresinde gösterilen hello özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="0dd07-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="0dd07-129">Başlık</span><span class="sxs-lookup"><span data-stu-id="0dd07-129">Title</span></span> | <span data-ttu-id="0dd07-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0dd07-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0dd07-131">EŞİTLEME DURUMU</span><span class="sxs-lookup"><span data-stu-id="0dd07-131">SYNC STATUS</span></span> |<span data-ttu-id="0dd07-132">Eşitlemenin etkin mi yoksa devre dışı mı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0dd07-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="0dd07-133">SON EŞİTLEME</span><span class="sxs-lookup"><span data-stu-id="0dd07-133">LAST SYNC</span></span> |<span data-ttu-id="0dd07-134">Son başarılı eşitleme tamamlandı hello.</span><span class="sxs-lookup"><span data-stu-id="0dd07-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="0dd07-135">FEDERASYON ETKİ ALANLARI</span><span class="sxs-lookup"><span data-stu-id="0dd07-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="0dd07-136">Şu anda yapılandırılmış Federasyon etki alanı Hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0dd07-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="0dd07-137">Yükleme</span><span class="sxs-lookup"><span data-stu-id="0dd07-137">Installation</span></span>
<span data-ttu-id="0dd07-138">tooinstall Azure AD Connect, kullanabileceğiniz hello belgelerine [burada](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="0dd07-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="0dd07-139">Gelişmiş özellikler ve Ek Bilgiler</span><span class="sxs-lookup"><span data-stu-id="0dd07-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="0dd07-140">Özel ayarlar veya gelişmiş yapılandırmalar hakkında ek bilgiler ya da kılavuzluk edinmek için [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md) (Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme) makalesinden başlayın.</span><span class="sxs-lookup"><span data-stu-id="0dd07-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="0dd07-141">Bu sayfayı tooadditional Kılavuzu bilgi ve bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="0dd07-141">This page provides information and links tooadditional guidance.</span></span>

