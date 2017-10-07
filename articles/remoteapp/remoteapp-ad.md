---
title: "aaaAzure AD + Azure RemoteApp için Active Directory gereksinimleri | Microsoft Docs"
description: "Bilgi nasıl tooset Azure RemoteApp ile Active Directory toowork ayarlama."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="42348-103">Azure AD + Azure RemoteApp için Active Directory gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="42348-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="42348-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="42348-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="42348-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="42348-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="42348-106">Azure RemoteApp karma koleksiyonu veya toofederate AD Connect kullanarak istediğiniz bulut koleksiyonu toodo hello aşağıdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="42348-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="42348-107">Azure AD connect ve Active Directory</span><span class="sxs-lookup"><span data-stu-id="42348-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="42348-108">Azure AD kiracınıza ve şirket içi Active Directory ortamınızı tooconnect istiyorsanız, AD Connect kullanın.</span><span class="sxs-lookup"><span data-stu-id="42348-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="42348-109">Bu, yalnızca sürer [4 tıklama](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello iki dizini.</span><span class="sxs-lookup"><span data-stu-id="42348-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="42348-110">Not - dizin eşitleme karma koleksiyonlar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="42348-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="42348-111">Emin olun, "@domain.com" eşleşmesi</span><span class="sxs-lookup"><span data-stu-id="42348-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="42348-112">Başlamadan önce şirket içi orman eşleşmeleri hello soneki Azure AD etki alanınızın bu Merhaba UPN emin olun.</span><span class="sxs-lookup"><span data-stu-id="42348-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="42348-113">Azure AD'de hello UPN etki alanı soneki ayarladıktan sonra Azure Remoteapp'te oturum açan tüm kullanıcılar olarak oturum açacak "kullanıcı @<hello suffix you set up>."</span><span class="sxs-lookup"><span data-stu-id="42348-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="42348-114">Kullanıcılar ayrıca oturum hello aynı oturum emin emin olun user@suffix hello şirket içi etki alanına.</span><span class="sxs-lookup"><span data-stu-id="42348-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="42348-115">Belirli durumlarda bir etki alanı adı hello kullanıcı-tesis içi için farklı bir etki alanı sonekini belirten sırasında Azure AD'de ayarlayabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="42348-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="42348-116">Bu durumda, kullanıcılarınızın mümkün tooconnect tooany etki alanına katılmış bilgisayarlara veya Azure RemoteApp aracılığıyla kaynaklara olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="42348-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="42348-117">Örneğin, UPN etki alanı soneki AAD contoso.com olarak ayarlamak, ancak şirket içi/AD üzerinde bazı kullanıcılar ile yapılandırılmış toolog @contoso.uk, bu kullanıcıların hello ARA koleksiyonu mümkün toocorrectly günlüğüne olmaz.</span><span class="sxs-lookup"><span data-stu-id="42348-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="42348-118">Kullanıcıların UPN AAD ve AD olmalıdır aynı hello oturum açma toobe olası hello"</span><span class="sxs-lookup"><span data-stu-id="42348-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="42348-119">Azure RemoteApp için nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="42348-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="42348-120">Ayrıca şirket içi Active Directory nesnelerini aşağıdaki toocreate hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="42348-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="42348-121">Bir hizmet hesabı tooprovide toodomain erişimine RDSH bitiş noktalarını toohello şirket içi etki alanına katılarak RemoteApp programları.</span><span class="sxs-lookup"><span data-stu-id="42348-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="42348-122">Bir kuruluş birimi (OU) toocontain RemoteApp makine nesnesi.</span><span class="sxs-lookup"><span data-stu-id="42348-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="42348-123">Önerilen (ancak gerekli değildir) tooisolate hello hesaplar ve ilkeler, RemoteApp ile kullanacağınız hello OU kullanımıdır.</span><span class="sxs-lookup"><span data-stu-id="42348-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="42348-124">RemoteApp koleksiyonunuzun oluşturduğunuzda, bu nesnelerin her ikisi gerekir böylece emin toodo adımları ilk olabilir.</span><span class="sxs-lookup"><span data-stu-id="42348-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>

