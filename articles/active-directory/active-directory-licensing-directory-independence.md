---
title: "Azure Active Directory aaaCharacteristics Kiracı intercaction | Microsoft Docs"
description: "Azure Active Kiracı kiracılarınız kiracılarınız tamamen bağımsız kaynaklar olarak anlayarak yönetme"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>Birden çok Azure Active Directory kiracıları etkileşim anlama

Azure Active Directory (Azure AD), her Kiracı tamamen bağımsız bir kaynaktır: mantıksal olarak bağımsızdır bir eş hello yönettiğiniz diğer kiracılar. Kiracılar arasında üst-alt ilişkisi yoktur. Kiracılar arasındaki bu bağımsızlığa kaynak bağımsızlığı, yönetim bağımsızlığı ve eşitleme bağımsızlığı dahildir.

## <a name="resource-independence"></a>Kaynak bağımsızlığı
* Oluşturursanız veya bir kiracı kaynak silin, dış kullanıcıların hello kısmi durumla başka bir kiracı herhangi bir kaynak üzerinde hiçbir etkisi yoktur. 
* Bir kiracı ile etki alanı adlarından birini kullanırsanız, başka hiçbir kiracıyla kullanılamaz.

## <a name="administrative-independence"></a>Yönetim bağımsızlığı
Kiracı 'Contoso' yönetici olmayan bir kullanıcı bir test Kiracı 'Test' ardından oluşturursa:

* Varsayılan olarak, bir kiracı oluşturur hello kullanıcının bir dış kullanıcı, yeni Kiracı ve Kiracı içinde atanan hello genel yönetici rolü olarak eklenir.
* bir yönetici 'Test' özellikle vermediği sürece Kiracı 'Contoso' hello Yöneticiler hiçbir doğrudan yönetim ayrıcalıkları tootenant 'Test' sahiptir. Ancak, 'Test' oluşturulan hello kullanıcı hesabı denetimi yöneticileri olarak 'Contoso' erişim tootenant 'Test' denetleyebilir
* Eklemek veya bir kullanıcı bir kiracı Yönetici rolü Kaldır, hello değişiklik değil etkileyen hello yönetici rolleri o hello yapar. kullanıcı başka bir kiracı sahiptir.

## <a name="synchronization-independence"></a>Eşitleme bağımsızlığı
Her Azure yapılandırabilirsiniz AD Kiracı bağımsız olarak herhangi birinin tek bir örneğinden tooget verileri:

* Hello Azure AD Connect aracı, tek bir AD ormanında toosynchronize verilerle.
* Azure Active Kiracı bağlayıcı için Forefront Identity Manager, bir toosynchronize verilerle hello veya daha fazla şirket içi ormanları ve/veya Azure olmayan AD veri kaynakları.

## <a name="add-an-azure-ad-tenant"></a>Azure AD kiracısı ekleme
tooadd hello Azure portal, Azure AD kiracısında oturum çok[Azure portal hello](https://portal.azure.com) Azure AD genel yönetici olan bir hesapla, hello sol, seçin ve **yeni**.

> [!NOTE]
> Diğer Azure kaynaklarının aksine, kiracılar bir Azure aboneliğinin alt kaynakları değildir. Azure aboneliğinizin süresi doldu veya iptal edilirse, Kiracı verilerinizi Azure PowerShell, hello Azure grafik API'sini veya hello Office 365 Yönetim merkezini kullanarak erişmeye devam edebilirsiniz. Ayrıca, başka bir abonelik hello Kiracı ile ilişkilendirebilirsiniz.
>

## <a name="next-steps"></a>Sonraki adımlar
Azure AD lisans sorunları ve en iyi yöntemler genel bakış için bkz: [ne olduğu Azure Active Kiracı lisans?](active-directory-licensing-whatis-azure-portal.md)
