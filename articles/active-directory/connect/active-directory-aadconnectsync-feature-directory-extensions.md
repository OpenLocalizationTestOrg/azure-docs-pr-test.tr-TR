---
title: "Azure AD Connect eşitleme: dizin uzantıları | Microsoft Docs"
description: "Bu konu, Azure AD CONNECT'te hello dizin uzantıları özelliğini açıklar."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="9106e-103">Azure AD Connect eşitleme: dizin uzantıları</span><span class="sxs-lookup"><span data-stu-id="9106e-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="9106e-104">Dizin uzantıları sağlar. tooextend hello şema şirket içi Active Directory'den kendi özniteliklerle Azure ad'deki.</span><span class="sxs-lookup"><span data-stu-id="9106e-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="9106e-105">Bu özellik toomanage şirket içi devam öznitelikleri kullanma toobuild LOB uygulamalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9106e-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="9106e-106">Bu öznitelikler aracılığıyla tüketilebilir [Azure AD grafik dizin uzantıları](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) veya [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="9106e-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="9106e-107">Merhaba öznitelikleri kullanılabilir kullanarak görebilirsiniz [Azure AD Graph Explorer'a](https://graphexplorer.cloudapp.net) ve [Microsoft Graph Explorer'a](https://graphexplorer2.azurewebsites.net/) sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="9106e-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="9106e-108">Şu anda hiçbir Office 365 iş yükü bu öznitelikler tüketir.</span><span class="sxs-lookup"><span data-stu-id="9106e-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="9106e-109">Hangi ek öznitelikleri yapılandırabilirsiniz hello Yükleme Sihirbazı'nı hello özel ayarları yolunda toosynchronize istiyor.</span><span class="sxs-lookup"><span data-stu-id="9106e-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="9106e-110">![Şema genişletme Sihirbazı](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="9106e-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="9106e-111">Geçerli adaylar öznitelikleri aşağıdaki hello Hello yüklemesini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="9106e-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="9106e-112">Kullanıcı ve grup nesne türleri</span><span class="sxs-lookup"><span data-stu-id="9106e-112">User and Group object types</span></span>
* <span data-ttu-id="9106e-113">Tek değerli öznitelikler: dize, Boolean, tamsayı, ikili</span><span class="sxs-lookup"><span data-stu-id="9106e-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="9106e-114">Birden çok değerli öznitelikleri: dize, ikili</span><span class="sxs-lookup"><span data-stu-id="9106e-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="9106e-115">Azure AD Connect yüklemesi sırasında oluşturulan hello şema önbelleğinden Hello özniteliklerinin listesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="9106e-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="9106e-116">Ek öznitelikler ile Merhaba Active Directory şemasını genişlettiyseniz, ardından hello [şema yenileneceğini](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) önce bu yeni öznitelikler görünür.</span><span class="sxs-lookup"><span data-stu-id="9106e-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="9106e-117">Azure AD'de bir nesne too100 dizin uzantıları nitelikler olabilir.</span><span class="sxs-lookup"><span data-stu-id="9106e-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="9106e-118">Merhaba uzunluk üst sınırı 250 karakterdir.</span><span class="sxs-lookup"><span data-stu-id="9106e-118">hello max length is 250 characters.</span></span> <span data-ttu-id="9106e-119">Bir öznitelik değeri uzunsa hello eşitleme altyapısı tarafından kesilir.</span><span class="sxs-lookup"><span data-stu-id="9106e-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="9106e-120">Azure AD Connect yüklemesi sırasında bir uygulama bu öznitelikler kullanılabildiği kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="9106e-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="9106e-121">Bu uygulamada hello Azure portal görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9106e-121">You can see this application in hello Azure portal.</span></span>  
![Şema uzantısı uygulama](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="9106e-123">Bu öznitelikler artık grafik kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="9106e-123">These attributes are now available through Graph:</span></span>  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="9106e-125">Merhaba öznitelikleri uzantısıyla önekli\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="9106e-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="9106e-126">Merhaba AppClientId aynı Azure AD kiracınızdaki tüm öznitelikleri değeri hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9106e-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9106e-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9106e-127">Next steps</span></span>
<span data-ttu-id="9106e-128">Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="9106e-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="9106e-129">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9106e-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
