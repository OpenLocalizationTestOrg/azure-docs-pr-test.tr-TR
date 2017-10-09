---
title: "aaaThe Azure AD Privileged Identity Management Güvenlik Sihirbazı"
description: "Merhaba hello Azure Active Directory Privileged Identity Management uzantısı, ilk kullanışınızda, Güvenlik Sihirbazı ile sunulur. Bu makalede hello Sihirbazı'nı kullanarak hello adımları açıklanmaktadır."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="0295d-104">Azure AD Privileged Identity Management Hello Güvenlik Sihirbazı'nı kullanma</span><span class="sxs-lookup"><span data-stu-id="0295d-104">Using hello security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="0295d-105">Kuruluşunuz için hello ilk kişinin toorun Azure Privileged Identity Management (PIM) değilseniz, bir sihirbaz ile sunulur.</span><span class="sxs-lookup"><span data-stu-id="0295d-105">If you're hello first person toorun Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="0295d-106">Merhaba sihirbaz ayrıcalıklı kimlikleri hello güvenlik risklerini anlamanıza yardımcı olur ve nasıl toouse PIM tooreduce bu riskleri.</span><span class="sxs-lookup"><span data-stu-id="0295d-106">hello wizard helps you understand hello security risks of privileged identities and how toouse PIM tooreduce those risks.</span></span> <span data-ttu-id="0295d-107">Toodo tercih ederseniz, tüm değişiklikleri tooexisting rol atamalarını hello Sihirbazı'nda toomake gerekmeyen daha sonra.</span><span class="sxs-lookup"><span data-stu-id="0295d-107">You don't need toomake any changes tooexisting role assignments in hello wizard, if you prefer toodo it later.</span></span>

## <a name="what-tooexpect"></a><span data-ttu-id="0295d-108">Hangi tooexpect</span><span class="sxs-lookup"><span data-stu-id="0295d-108">What tooexpect</span></span>
<span data-ttu-id="0295d-109">PIM kullanarak kuruluşunuz başlamadan önce tüm rol atamalarını kalıcı: hello kullanıcıların her zaman bu rollerde dahi şu anda ayrıcalıklarını gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0295d-109">Before your organization starts using PIM, all role assignments are permanent: hello users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="0295d-110">hello Sihirbazı'nın Hello ilk adım, yüksek ayrıcalıklı rolleri listesini ve kaç kullanıcı şu anda bu rollerden gösterir.</span><span class="sxs-lookup"><span data-stu-id="0295d-110">hello first step of hello wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="0295d-111">Bir veya daha fazlası tanımıyorsanız tooa belirli rol toolearn kullanıcılar hakkında daha fazla ayrıntıya inebilir.</span><span class="sxs-lookup"><span data-stu-id="0295d-111">You can drill in tooa particular role toolearn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="0295d-112">Başlangıç Sihirbazı'nın ikinci adım Hello fırsat toochange yöneticinin rol atamalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0295d-112">hello second step of hello wizard gives you an opportunity toochange administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="0295d-113">En az bir genel yönetici ve bir kurumsal hesap (Microsoft hesabı değil) ile birden fazla ayrıcalıklı Rol Yöneticisi olması da önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0295d-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="0295d-114">Tek bir ayrıcalıklı rol yöneticisi ise, bu hesabı silinirse hello kuruluş mümkün toomanage PIM olmaz.</span><span class="sxs-lookup"><span data-stu-id="0295d-114">If there is only one privileged role administrator, hello organization will not be able toomanage PIM if that account is deleted.</span></span>
> <span data-ttu-id="0295d-115">Ayrıca, rol atamaları bir kullanıcının bir Microsoft hesabı (Skype ve Outlook.com gibi tooMicrosoft Hizmetleri'ndeki toosign kullandıkları hesabı) varsa kalıcı tutun.</span><span class="sxs-lookup"><span data-stu-id="0295d-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use toosign in tooMicrosoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="0295d-116">Bu rol için etkinleştirme için MFA toorequire düşünüyorsanız, bu kullanıcının kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="0295d-116">If you plan toorequire MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="0295d-117">Değişiklikleri yaptıktan sonra Başlangıç Sihirbazı'nı artık görünecektir.</span><span class="sxs-lookup"><span data-stu-id="0295d-117">After you have made changes, hello wizard will no longer show up.</span></span> <span data-ttu-id="0295d-118">Merhaba, veya başka bir ayrıcalıklı Rol Yöneticisi PIM, sonraki kullanışınızda hello PIM Pano görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0295d-118">hello next time you or another privileged role administrator use PIM, you will see hello PIM dashboard.</span></span>  

* <span data-ttu-id="0295d-119">İster tooadd veya kullanıcıların rollerini kaldırın veya, kalıcı tooeligible atamalarını değiştirme hakkında daha fazla okuma [nasıl tooadd veya kullanıcı rolünü kaldırmak](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="0295d-119">If you would like tooadd or remove users from roles or change assignments from permanent tooeligible, read more at [how tooadd or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="0295d-120">Daha fazla kullanıcı toogive isterseniz toomanage PIM, erişim, okuma hakkında daha fazla [nasıl toogive erişim PIM toomanage](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="0295d-120">If you would like toogive more users access toomanage PIM, read more at [how toogive access toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0295d-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0295d-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

