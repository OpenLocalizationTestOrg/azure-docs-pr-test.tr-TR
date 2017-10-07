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
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Azure AD - genel Önizleme idari Birim Yönetimi
Bu makalede idari birim – yeni bir Azure Active Directory kapsayıcısı kullanıcılar kümelerine ve uygulama ilkeleri tooa kullanıcı alt kümesini üzerinden yönetim izinleri temsilci için kullanılabilir kaynakların açıklanmaktadır. Azure Active Directory'de merkezi yöneticileri toodelegate izinleri tooregional yöneticileri veya ayrıntılı bir düzeyde tooset İlkesi idari birim etkinleştirin.

Bu, bağımsız bölümler, örneğin, birbirinden bağımsız olan birçok otonom okullar (iş okul, mühendislik Okul ve benzeri) oluşan bir büyük üniversite olan kuruluşlarda yararlıdır. Bu tür bölümler, özellikle kendi bölme için ilkeler ayarlama erişimi denetlemek ve kullanıcıları yönetmek, kendi BT yöneticileri vardır. Merkezi yöneticileri toobe mümkün grant hello kullanıcılar kendi belirli bölümler üzerinden bu bölümsel yöneticileri izinleri istiyor. Daha belirgin olarak bu örneği kullanarak, merkezi bir yönetici, örneği için belirli bir okul (iş Okul) için bir yönetim birimi oluşturabilir ve yalnızca hello iş Okul kullanıcılarla doldurmak. Daha sonra merkezi yönetici hello iş Okul BT personeli kapsamlı tooa rolü, diğer bir deyişle, grant hello iş Okul yönetim izinleri yalnızca hello Okul yönetim departman üzerinden BT personeli ekleyebilirsiniz.

> [!IMPORTANT]
> Yalnızca Azure Active Directory Premium etkinleştirirseniz yönetimsel birim kapsamlı yönetici rollerini atayabilir. Daha fazla bilgi için bkz: [Azure AD Premium ile çalışmaya başlama](active-directory-get-started-premium.md).
>


Merhaba merkezi yöneticisinin bakış açısından, bir yönetici oluşturulan ve kaynaklarla doldurulan bir dizin nesnesi birimdir. **Bu önizleme sürümünde bu kaynakları yalnızca kullanıcılar olabilir.** Oluşturulur ve doldurulur sonra hello yönetim birimi hello yönetim biriminde bulunan kaynakları üzerinden iznine sahip bir kapsam toorestrict hello olarak kullanılabilir.

## <a name="managing-administrative-units"></a>İdari Birim Yönetimi
Bu önizleme sürümünde oluşturun ve idari birim hello Azure Active Directory için Windows PowerShell modülü cmdlet öğelerini kullanarak yönetin. toolearn nasıl hakkında daha fazla bilgi görmek, toodo [idari birim ile çalışma](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Merhaba sözdizimi, parametre açıklamaları ve örnekler dahil olmak üzere idari birim yönetmek için Azure AD modülü cmdlet'ler hakkında bilgi ve yazılım gereksinimleri ve yükleme hello Azure AD modülü hakkında daha fazla bilgi için bkz: [Azure Active Dizin PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory sürümleri](active-directory-editions.md)
