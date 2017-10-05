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
ms.openlocfilehash: e8321c3d16253226a5931cacbce6fa5d50b697bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="1b2ca-103">Azure AD Connect: Özel konular örnekleri</span><span class="sxs-lookup"><span data-stu-id="1b2ca-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="1b2ca-104">Azure AD Connect ile Azure AD dünya çapındaki örneğini en yaygın olarak kullanılan ve Office 365.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="1b2ca-105">Ancak aynı zamanda diğer örneği vardır ve bu URL'leri ve diğer özel durumlar için farklı gereksinimlere sahip.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="1b2ca-106">Microsoft Bulut Almanya</span><span class="sxs-lookup"><span data-stu-id="1b2ca-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="1b2ca-107">[Microsoft Cloud Almanya](http://www.microsoft.de/cloud-deutschland) Almanca veri güvenliği tarafından işletilen bir sovereign bulut.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="1b2ca-108">Proxy sunucu açmak için URL'leri</span><span class="sxs-lookup"><span data-stu-id="1b2ca-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="1b2ca-109">\*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="1b2ca-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="1b2ca-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="1b2ca-110">\*.windows.net</span></span> |
| <span data-ttu-id="1b2ca-111">+ Sertifika iptal listeleri</span><span class="sxs-lookup"><span data-stu-id="1b2ca-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="1b2ca-112">Azure AD kiracınıza oturum açtığınızda onmicrosoft.de etki alanındaki bir hesabı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="1b2ca-113">Özellikleri Microsoft Cloud Almanya şu anda yok:</span><span class="sxs-lookup"><span data-stu-id="1b2ca-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="1b2ca-114">**Azure AD Connect Health** kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="1b2ca-115">**Otomatik Güncelleştirmeler** kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="1b2ca-116">**Parola geri yazma** 1.1.570.0 Azure AD Connect sürümüyle ve sonra Önizleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="1b2ca-117">Diğer Azure AD Premium hizmetlerine kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="1b2ca-118">Microsoft Azure kamu bulut</span><span class="sxs-lookup"><span data-stu-id="1b2ca-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="1b2ca-119">[Microsoft Azure kamu bulut](https://azure.microsoft.com/features/gov/) ABD devlet kurumları için bir bulut.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="1b2ca-120">Bu bulut DirSync önceki sürümleri tarafından desteklenen.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="1b2ca-121">Yapıdan Azure AD Connect 1.1.180, yeni nesil bulut desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="1b2ca-122">Bu oluşturma yalnızca ABD tabanlı uç noktalarını kullanarak ve URL'leri proxy sunucunuzun açmak için farklı bir listesi vardır.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="1b2ca-123">Proxy sunucu açmak için URL'leri</span><span class="sxs-lookup"><span data-stu-id="1b2ca-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="1b2ca-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1b2ca-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="1b2ca-125">\*. microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="1b2ca-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="1b2ca-126">\*. gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1b2ca-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="1b2ca-127">+ Sertifika iptal listeleri</span><span class="sxs-lookup"><span data-stu-id="1b2ca-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="1b2ca-128">Azure AD Connect otomatik olarak Azure AD kiracınıza kamu bulutta bulunduğundan algılayabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-128">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="1b2ca-129">Bunun yerine, Azure AD Connect yüklediğinizde aşağıdaki eylemleri gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-129">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="1b2ca-130">Azure AD Connect yüklemesi başlatın.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-130">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="1b2ca-131">Burada EULA'yı kabul beklenir ilk sayfasını gördüğünüzde devam eder ancak Yükleme Sihirbazı'nı çalıştıran bırakın.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-131">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="1b2ca-132">Regedit başlatın ve kayıt defteri anahtarını değiştirin `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` değerine `2`.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-132">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="1b2ca-133">Azure AD Connect Yükleme Sihirbazı'için geri EULA'yı kabul edin ve devam gidin.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-133">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="1b2ca-134">Yükleme sırasında kullandığınızdan emin olun **özel yapılandırma** yükleme yolu (ve hızlı yükleme).</span><span class="sxs-lookup"><span data-stu-id="1b2ca-134">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="1b2ca-135">Ardından yükleme işlemine devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-135">Then continue the installation as usual.</span></span>

<span data-ttu-id="1b2ca-136">Özellikleri Microsoft Azure kamu bulutta şu anda yok:</span><span class="sxs-lookup"><span data-stu-id="1b2ca-136">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="1b2ca-137">**Azure AD Connect Health** kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="1b2ca-138">**Otomatik Güncelleştirmeler** kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="1b2ca-139">**Parola geri yazma** 1.1.570.0 Azure AD Connect sürümüyle ve sonra Önizleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="1b2ca-140">Diğer Azure AD Premium hizmetlerine kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b2ca-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1b2ca-141">Next steps</span></span>
<span data-ttu-id="1b2ca-142">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1b2ca-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
