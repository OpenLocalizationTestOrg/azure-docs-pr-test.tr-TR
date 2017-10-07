---
title: "Azure Active Directory'de aaaAdministrative birimleri Yönetimi Önizleme"
description: "Daha ayrıntılı Azure Active Directory izinleri için temsilci seçme için idari birim kullanma"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a><span data-ttu-id="9a60d-103">Azure AD - genel Önizleme idari Birim Yönetimi</span><span class="sxs-lookup"><span data-stu-id="9a60d-103">Administrative units management in Azure AD - public preview</span></span>
<span data-ttu-id="9a60d-104">Bu makalede idari birim – yeni bir Azure Active Directory kapsayıcısı kullanıcılar kümelerine ve uygulama ilkeleri tooa kullanıcı alt kümesini üzerinden yönetim izinleri temsilci için kullanılabilir kaynakların açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a60d-104">This article describes administrative units – a new Azure Active Directory container of resources that can be used for delegating administrative permissions over subsets of users and applying policies tooa subset of users.</span></span> <span data-ttu-id="9a60d-105">Azure Active Directory'de merkezi yöneticileri toodelegate izinleri tooregional yöneticileri veya ayrıntılı bir düzeyde tooset İlkesi idari birim etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9a60d-105">In Azure Active Directory, administrative units enable central administrators toodelegate permissions tooregional administrators or tooset policy at a granular level.</span></span>

<span data-ttu-id="9a60d-106">Bu, bağımsız bölümler, örneğin, birbirinden bağımsız olan birçok otonom okullar (iş okul, mühendislik Okul ve benzeri) oluşan bir büyük üniversite olan kuruluşlarda yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="9a60d-106">This is useful in organizations with independent divisions, for example, a large university that is made up of many autonomous schools (Business school, Engineering school, and so on) which are independent from each other.</span></span> <span data-ttu-id="9a60d-107">Bu tür bölümler, özellikle kendi bölme için ilkeler ayarlama erişimi denetlemek ve kullanıcıları yönetmek, kendi BT yöneticileri vardır.</span><span class="sxs-lookup"><span data-stu-id="9a60d-107">Such divisions have their own IT administrators who control access, manage users, and set policies specifically for their division.</span></span> <span data-ttu-id="9a60d-108">Merkezi yöneticileri toobe mümkün grant hello kullanıcılar kendi belirli bölümler üzerinden bu bölümsel yöneticileri izinleri istiyor.</span><span class="sxs-lookup"><span data-stu-id="9a60d-108">Central administrators want toobe able grant these divisional administrators permissions over hello users in their particular divisions.</span></span> <span data-ttu-id="9a60d-109">Daha belirgin olarak bu örneği kullanarak, merkezi bir yönetici, örneği için belirli bir okul (iş Okul) için bir yönetim birimi oluşturabilir ve yalnızca hello iş Okul kullanıcılarla doldurmak.</span><span class="sxs-lookup"><span data-stu-id="9a60d-109">More specifically, using this example, a central administrator can, for instance, create an administrative unit for a particular school (Business school) and populate it with only hello Business school users.</span></span> <span data-ttu-id="9a60d-110">Daha sonra merkezi yönetici hello iş Okul BT personeli kapsamlı tooa rolü, diğer bir deyişle, grant hello iş Okul yönetim izinleri yalnızca hello Okul yönetim departman üzerinden BT personeli ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a60d-110">Then a central administrator can add hello Business school IT staff tooa scoped role, in other words, grant hello IT staff of Business school administrative permissions only over hello Business school administrative unit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a60d-111">Yalnızca Azure Active Directory Premium etkinleştirirseniz yönetimsel birim kapsamlı yönetici rollerini atayabilir.</span><span class="sxs-lookup"><span data-stu-id="9a60d-111">You can assign administrative unit-scoped admin roles only if you enable Azure Active Directory Premium.</span></span> <span data-ttu-id="9a60d-112">Daha fazla bilgi için bkz: [Azure AD Premium ile çalışmaya başlama](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="9a60d-112">For more information, see [Getting started with Azure AD Premium](active-directory-get-started-premium.md).</span></span>
>


<span data-ttu-id="9a60d-113">Merhaba merkezi yöneticisinin bakış açısından, bir yönetici oluşturulan ve kaynaklarla doldurulan bir dizin nesnesi birimdir.</span><span class="sxs-lookup"><span data-stu-id="9a60d-113">From hello central administrator’s point of view, an administrative unit is a directory object that can be created and populated with resources.</span></span> <span data-ttu-id="9a60d-114">**Bu önizleme sürümünde bu kaynakları yalnızca kullanıcılar olabilir.**</span><span class="sxs-lookup"><span data-stu-id="9a60d-114">**In this preview release, these resources can be only users.**</span></span> <span data-ttu-id="9a60d-115">Oluşturulur ve doldurulur sonra hello yönetim birimi hello yönetim biriminde bulunan kaynakları üzerinden iznine sahip bir kapsam toorestrict hello olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9a60d-115">Once created and populated, hello administrative unit can be used as a scope toorestrict hello granted permission only over resources contained in hello administrative unit.</span></span>

## <a name="managing-administrative-units"></a><span data-ttu-id="9a60d-116">İdari Birim Yönetimi</span><span class="sxs-lookup"><span data-stu-id="9a60d-116">Managing administrative units</span></span>
<span data-ttu-id="9a60d-117">Bu önizleme sürümünde oluşturun ve idari birim hello Azure Active Directory için Windows PowerShell modülü cmdlet öğelerini kullanarak yönetin.</span><span class="sxs-lookup"><span data-stu-id="9a60d-117">In this preview release, you can create and manage administrative units using hello Azure Active Directory Module for Windows PowerShell cmdlets.</span></span> <span data-ttu-id="9a60d-118">toolearn nasıl hakkında daha fazla bilgi görmek, toodo [idari birim ile çalışma](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span><span class="sxs-lookup"><span data-stu-id="9a60d-118">toolearn more about how toodo that, see [Working with Administrative Units](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span></span>

<span data-ttu-id="9a60d-119">Merhaba sözdizimi, parametre açıklamaları ve örnekler dahil olmak üzere idari birim yönetmek için Azure AD modülü cmdlet'ler hakkında bilgi ve yazılım gereksinimleri ve yükleme hello Azure AD modülü hakkında daha fazla bilgi için bkz: [Azure Active Dizin PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="9a60d-119">For more information on software requirements and installing hello Azure AD module, and for information on hello Azure AD Module cmdlets for managing administrative units, including syntax, parameter descriptions, and examples, see [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a60d-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a60d-120">Next steps</span></span>
[<span data-ttu-id="9a60d-121">Azure Active Directory sürümleri</span><span class="sxs-lookup"><span data-stu-id="9a60d-121">Azure Active Directory editions</span></span>](active-directory-editions.md)
