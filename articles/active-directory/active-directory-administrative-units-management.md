---
title: "Azure Active Directory'de idari birim yönetimi Önizleme"
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
ms.openlocfilehash: e12a0aea8264b1ea67c26294ec5bbe9c404a171e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a><span data-ttu-id="a5a95-103">Azure AD - genel Önizleme idari Birim Yönetimi</span><span class="sxs-lookup"><span data-stu-id="a5a95-103">Administrative units management in Azure AD - public preview</span></span>
<span data-ttu-id="a5a95-104">Bu makalede idari birim – yeni bir Azure Active Directory kapsayıcısı kullanıcılar ve kullanıcı alt kümesine ilkelerini uygulama kümelerine üzerinden yönetim izinleri temsilci için kullanılabilir kaynakların açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a5a95-104">This article describes administrative units – a new Azure Active Directory container of resources that can be used for delegating administrative permissions over subsets of users and applying policies to a subset of users.</span></span> <span data-ttu-id="a5a95-105">Azure Active Directory'de merkezi yöneticileri temsilci izinleri bölgesel yöneticilere veya ayrıntılı bir düzeyde İlkesi ayarlamak için idari birim etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a5a95-105">In Azure Active Directory, administrative units enable central administrators to delegate permissions to regional administrators or to set policy at a granular level.</span></span>

<span data-ttu-id="a5a95-106">Bu, bağımsız bölümler, örneğin, birbirinden bağımsız olan birçok otonom okullar (iş okul, mühendislik Okul ve benzeri) oluşan bir büyük üniversite olan kuruluşlarda yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="a5a95-106">This is useful in organizations with independent divisions, for example, a large university that is made up of many autonomous schools (Business school, Engineering school, and so on) which are independent from each other.</span></span> <span data-ttu-id="a5a95-107">Bu tür bölümler, özellikle kendi bölme için ilkeler ayarlama erişimi denetlemek ve kullanıcıları yönetmek, kendi BT yöneticileri vardır.</span><span class="sxs-lookup"><span data-stu-id="a5a95-107">Such divisions have their own IT administrators who control access, manage users, and set policies specifically for their division.</span></span> <span data-ttu-id="a5a95-108">Merkezi Yöneticiler olması istiyorsanız bu bölümsel vermek kullanıcılar kendi belirli bölümler üzerinden Yöneticiler izinleri.</span><span class="sxs-lookup"><span data-stu-id="a5a95-108">Central administrators want to be able grant these divisional administrators permissions over the users in their particular divisions.</span></span> <span data-ttu-id="a5a95-109">Daha belirgin olarak bu örneği kullanarak, merkezi bir yönetici, örneği için belirli bir okul (iş Okul) için bir yönetim birimi oluşturabilir ve yalnızca iş Okul kullanıcılarla doldurmak.</span><span class="sxs-lookup"><span data-stu-id="a5a95-109">More specifically, using this example, a central administrator can, for instance, create an administrative unit for a particular school (Business school) and populate it with only the Business school users.</span></span> <span data-ttu-id="a5a95-110">Daha sonra bir merkezi yönetici iş Okul BT personeli kapsamlı bir role ekleyebilirsiniz diğer bir deyişle, iş Okul yönetim izinleri BT personeli yalnızca Okul yönetim departman verin.</span><span class="sxs-lookup"><span data-stu-id="a5a95-110">Then a central administrator can add the Business school IT staff to a scoped role, in other words, grant the IT staff of Business school administrative permissions only over the Business school administrative unit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5a95-111">Yalnızca Azure Active Directory Premium etkinleştirirseniz yönetimsel birim kapsamlı yönetici rollerini atayabilir.</span><span class="sxs-lookup"><span data-stu-id="a5a95-111">You can assign administrative unit-scoped admin roles only if you enable Azure Active Directory Premium.</span></span> <span data-ttu-id="a5a95-112">Daha fazla bilgi için bkz: [Azure AD Premium ile çalışmaya başlama](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="a5a95-112">For more information, see [Getting started with Azure AD Premium](active-directory-get-started-premium.md).</span></span>
>


<span data-ttu-id="a5a95-113">Merkezi yöneticisinin bakış açısından, bir yönetici oluşturulan ve kaynaklarla doldurulan bir dizin nesnesi birimdir.</span><span class="sxs-lookup"><span data-stu-id="a5a95-113">From the central administrator’s point of view, an administrative unit is a directory object that can be created and populated with resources.</span></span> <span data-ttu-id="a5a95-114">**Bu önizleme sürümünde bu kaynakları yalnızca kullanıcılar olabilir.**</span><span class="sxs-lookup"><span data-stu-id="a5a95-114">**In this preview release, these resources can be only users.**</span></span> <span data-ttu-id="a5a95-115">Oluşturulur ve doldurulur sonra Yönetim birimi verilen yönetim biriminde bulunan kaynakları üzerinden erişimi kısıtlamak için kapsam olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a5a95-115">Once created and populated, the administrative unit can be used as a scope to restrict the granted permission only over resources contained in the administrative unit.</span></span>

## <a name="managing-administrative-units"></a><span data-ttu-id="a5a95-116">İdari Birim Yönetimi</span><span class="sxs-lookup"><span data-stu-id="a5a95-116">Managing administrative units</span></span>
<span data-ttu-id="a5a95-117">Bu önizleme sürümünde oluşturun ve Azure Active Directory için Windows PowerShell modülü cmdlet öğelerini kullanarak idari birim yönetin.</span><span class="sxs-lookup"><span data-stu-id="a5a95-117">In this preview release, you can create and manage administrative units using the Azure Active Directory Module for Windows PowerShell cmdlets.</span></span> <span data-ttu-id="a5a95-118">Bunun hakkında daha fazla bilgi edinmek için [idari birim ile çalışma](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span><span class="sxs-lookup"><span data-stu-id="a5a95-118">To learn more about how to do that, see [Working with Administrative Units](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span></span>

<span data-ttu-id="a5a95-119">Sözdizimi, parametre açıklamaları ve örnekler dahil olmak üzere idari birim yönetmek için Azure AD modülü cmdlet'ler hakkında bilgi ve yazılım gereksinimleri ve Azure AD modülünü yükleme hakkında daha fazla bilgi için bkz: [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="a5a95-119">For more information on software requirements and installing the Azure AD module, and for information on the Azure AD Module cmdlets for managing administrative units, including syntax, parameter descriptions, and examples, see [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5a95-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a5a95-120">Next steps</span></span>
[<span data-ttu-id="a5a95-121">Azure Active Directory sürümleri</span><span class="sxs-lookup"><span data-stu-id="a5a95-121">Azure Active Directory editions</span></span>](active-directory-editions.md)
