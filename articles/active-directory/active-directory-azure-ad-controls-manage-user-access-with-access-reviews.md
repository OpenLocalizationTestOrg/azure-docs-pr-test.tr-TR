---
title: "Azure AD erişim gözden geçirmeleriyle kullanıcı erişimini yönetme| Microsoft Docs"
description: "Azure Active Directory erişim gözden geçirmeleri ile bir grup üyeliği veya bir uygulamaya atama aracılığıyla kullanıcı erişimini yönetmeyi öğrenin"
services: active-directory
documentationcenter: 
author: markwahl-msft
manager: mtillman
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/19/2017
ms.author: billmath
ms.openlocfilehash: 6a4d25b2eb228cafab48419a0d0eda92bba9f1ec
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="manage-user-access-with-azure-ad-access-reviews"></a>Azure AD erişim gözden geçirmeleriyle kullanıcı erişimini yönetme

Azure Active Directory (Azure AD) sayesinde kullanıcıların uygun erişime sahip olduğundan kolayca emin olabilirsiniz. Kullanıcılardan veya bir karar verenden erişim gözden geçirmesine katılmasını ve kullanıcıların erişimini yeniden onaylamasını (veya doğrulamasını) isteyebilirsiniz. Gözden geçirenler, Azure AD önerilerine dayanarak her kullanıcının erişiminin devam edip etmemesine yönelik girişler ekleyebilir. Bir erişim gözden geçirmesi tamamlandığında, değişiklikler yapabilir ve artık erişime ihtiyaç duymayan kullanıcıların erişimini kaldırabilirsiniz.

> [!NOTE]
> Tüm kullanıcı türlerinin erişimini yerine yalnızca konuk kullanıcıların erişimini gözden geçirmek istiyorsanız [Erişim gözden geçirmeleriyle konuk kullanıcı erişimini yönetme](active-directory-azure-ad-controls-manage-guest-access-with-access-reviews.md) konusunu inceleyin. Genel yönetici gibi yönetim rollerindeki kullanıcı üyeliklerini gözden geçirmek istiyorsanız [Azure AD Privileged Identity Management’ta erişim gözden geçirmesi başlatma](active-directory-privileged-identity-management-how-to-start-security-review.md) konusunu inceleyin. 
>
>

## <a name="prerequisites"></a>Ön koşullar 

Erişim gözden geçirmeleri, Azure AD’nin Microsoft Enterprise Mobility + Security, E5’e dahil olan Premium P2 sürümü ile kullanılabilir. Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md). Bir gözden geçirme oluşturmak, gözden geçirmeye erişmek veya gözden geçirme uygulamak üzere bu özellikle etkileşimde bulunan her kullanıcının bir lisansı olması gerekir.


## <a name="create-and-perform-an-access-review"></a>Erişim gözden geçirmesi oluşturma ve gerçekleştirme

Bir erişim gözden geçirmesinde bir veya daha çok kullanıcı gözden geçiren olabilir.  

1. Azure AD'de bir veya daha fazla üyesi olan bir grup seçin. Veya Azure AD’ye bağlı olup bir ya da daha fazla kullanıcı atanmış bir uygulama seçin. 

2. Her kullanıcının kendi erişimini mi gözden geçireceğine yoksa bir veya daha fazla kullanıcının tüm kullanıcıların erişimini mi gözden geçireceğine karar verin.

3. Erişim gözden geçirmelerini gözden geçiren kişinin erişim panellerinde görünmesi için etkinleştirin. Bir genel yönetici olarak, [erişim gözden geçirmeleri sayfasına](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/) gidin.

4. Erişim gözden geçirmesini başlatın. Daha fazla bilgi için [Erişim gözden geçirmesi oluşturma](active-directory-azure-ad-controls-create-access-review.md) konusunu inceleyin.

5. Gözden geçirenlerden bilgileri girmelerini isteyin. Varsayılan olarak, tüm gözden geçirenler Azure AD’den [erişim gözden geçirmelerini gerçekleştirecekleri](active-directory-azure-ad-controls-perform-access-review.md) erişim paneline yönlendiren bir bağlantı içeren bir e-posta alır.

6. Gözden geçirenler bilgi girmediyse, Azure AD’nin onlara bir anımsatıcı göndermesini isteyebilirsiniz. Varsayılan olarak, bitiş tarihine kadar olan sürenin yarısına ulaşıldığında, Azure AD henüz yanıt vermemiş olan gözden geçirenlere bir anımsatıcı gönderir.

7. Gözden geçirenler bilgileri girdikten sonra erişim gözden geçirmesini durdurun ve değişiklikleri uygulayın. Daha fazla bilgi için [Erişim gözden geçirmesini tamamlama](active-directory-azure-ad-controls-complete-access-review.md) konusunu inceleyin.


## <a name="next-steps"></a>Sonraki adımlar

[Bir grubun üyeleri veya bir uygulamaya erişim için erişim gözden geçirmesi oluşturma](active-directory-azure-ad-controls-create-access-review.md)




