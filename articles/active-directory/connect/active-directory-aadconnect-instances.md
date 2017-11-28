---
title: "Azure AD Connect: Eşitleme hizmeti örnekleri | Microsoft Docs"
description: "Bu sayfa, Azure AD örnekleri için özel hususlar belgeler."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="f3d2a-103">Azure AD Connect: Özel konular örnekleri</span><span class="sxs-lookup"><span data-stu-id="f3d2a-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="f3d2a-104">Azure AD Connect Merhaba Dünya çapında Azure AD örneğinizle en yaygın olarak kullanılan ve Office 365.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="f3d2a-105">Ancak aynı zamanda diğer örneği vardır ve bu URL'leri ve diğer özel durumlar için farklı gereksinimlere sahip.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="f3d2a-106">Microsoft Bulut Almanya</span><span class="sxs-lookup"><span data-stu-id="f3d2a-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="f3d2a-107">Merhaba [Microsoft Cloud Almanya](http://www.microsoft.de/cloud-deutschland) Almanca veri güvenliği tarafından işletilen bir sovereign bulut.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="f3d2a-108">Proxy sunucu olarak URL'leri tooopen</span><span class="sxs-lookup"><span data-stu-id="f3d2a-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="f3d2a-109">\*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="f3d2a-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="f3d2a-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="f3d2a-110">\*.windows.net</span></span> |
| <span data-ttu-id="f3d2a-111">+ Sertifika iptal listeleri</span><span class="sxs-lookup"><span data-stu-id="f3d2a-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="f3d2a-112">Tooyour Azure AD kiracısı'nda oturum açtığınızda hello onmicrosoft.de etki alanındaki bir hesabı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="f3d2a-113">Özellikleri hello Microsoft Cloud Almanya şu anda yok:</span><span class="sxs-lookup"><span data-stu-id="f3d2a-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="f3d2a-114">**Azure AD Connect Health** kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="f3d2a-115">**Otomatik Güncelleştirmeler** kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="f3d2a-116">**Parola geri yazma** 1.1.570.0 Azure AD Connect sürümüyle ve sonra Önizleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="f3d2a-117">Diğer Azure AD Premium hizmetlerine kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="f3d2a-118">Microsoft Azure kamu bulut</span><span class="sxs-lookup"><span data-stu-id="f3d2a-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="f3d2a-119">Merhaba [Microsoft Azure kamu bulut](https://azure.microsoft.com/features/gov/) ABD devlet kurumları için bir bulut.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="f3d2a-120">Bu bulut DirSync önceki sürümleri tarafından desteklenen.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="f3d2a-121">Yapıdan Azure AD Connect 1.1.180, yeni nesil hello bulut hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="f3d2a-122">Bu oluşturma yalnızca ABD tabanlı uç noktalarını kullanarak ve proxy sunucunuzun URL'leri tooopen farklı bir listesi vardır.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="f3d2a-123">Proxy sunucu olarak URL'leri tooopen</span><span class="sxs-lookup"><span data-stu-id="f3d2a-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="f3d2a-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="f3d2a-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="f3d2a-125">\*. microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="f3d2a-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="f3d2a-126">\*. gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="f3d2a-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="f3d2a-127">+ Sertifika iptal listeleri</span><span class="sxs-lookup"><span data-stu-id="f3d2a-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="f3d2a-128">Azure AD Connect mümkün değil tooautomatically algılamak Azure AD kiracınıza hello Bulutu bulunur.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="f3d2a-129">Bunun yerine, Azure AD Connect yüklediğinizde eylemleri aşağıdaki tootake hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="f3d2a-130">Hello Azure AD Connect yüklemesi başlatın.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="f3d2a-131">Burada tooaccept hello EULA beklenen hello ilk sayfasını gördüğünüzde devam eder ancak hello Yükleme Sihirbazı'nı çalıştıran bırakın.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="f3d2a-132">Regedit başlatın ve hello kayıt defteri anahtarını değiştirin `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello değeri `2`.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="f3d2a-133">Toohello Azure AD Connect Yükleme Sihirbazı'nı geri dönün, hello EULA kabul edin ve devam edin.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="f3d2a-134">Yükleme sırasında emin toouse hello olun **özel yapılandırma** yükleme yolu (ve hızlı yükleme).</span><span class="sxs-lookup"><span data-stu-id="f3d2a-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="f3d2a-135">Ardından hello yükleme her zamanki gibi devam edin.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="f3d2a-136">Özellikleri hello Microsoft Azure kamu bulutta şu anda yok:</span><span class="sxs-lookup"><span data-stu-id="f3d2a-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="f3d2a-137">**Azure AD Connect Health** kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="f3d2a-138">**Otomatik Güncelleştirmeler** kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="f3d2a-139">**Parola geri yazma** 1.1.570.0 Azure AD Connect sürümüyle ve sonra Önizleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="f3d2a-140">Diğer Azure AD Premium hizmetlerine kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3d2a-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f3d2a-141">Next steps</span></span>
<span data-ttu-id="f3d2a-142">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="f3d2a-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
