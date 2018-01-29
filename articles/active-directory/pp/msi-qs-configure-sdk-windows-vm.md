---
title: "Bir Azure SDK'yı kullanarak bir Azure VM için bir kullanıcı tarafından atanan MSI yapılandırma"
description: "Azure bir Azure SDK'sını kullanarak VM için bir kullanıcı tarafından atanan yönetilen hizmet kimliği (MSI) yapılandırma için adım yönergeler tarafından adım."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/22/2017
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 19b6179803b8de4102818c1522b00e6b4881d0f0
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/22/2017
---
# <a name="configure-a-user-assigned-managed-service-identity-msi-for-a-vm-using-an-azure-sdk"></a>Bir Azure SDK'yı kullanarak bir VM için bir kullanıcı tarafından atanan yönetilen hizmet kimliği (MSI) yapılandırma

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

Yönetilen hizmet kimliği Azure Active Directory'deki yönetilen bir kimlikle Azure hizmetleri sağlar. Bu kimlik, Azure AD kimlik doğrulaması, kimlik bilgileri, kodunuzda gerek kalmadan destekleyen hizmetlerin kimlik doğrulaması için kullanabilirsiniz. 

Bu makalede, etkinleştirme ve Azure bir Azure SDK'sını kullanarak VM için kullanıcı tarafından atanan bir MSI kaldırma öğrenin.

## <a name="prerequisites"></a>Önkoşullar

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

## <a name="azure-sdks-with-msi-support"></a>Azure SDK'ları ile MSI desteği 

Azure destekleyen bir dizi programlama birden çok platform [Azure SDK'ları](https://azure.microsoft.com/downloads). Birkaç MSI desteklemek ve kullanım göstermek için karşılık gelen örnekleri sağlamak üzere güncelleştirilmiştir. Ek destek eklendikçe bu listeyi güncelleştirilmiştir:

| SDK | Örnek |
| --- | ------ | 
| Python | [MSI etkin bir VM oluşturma](https://azure.microsoft.com/resources/samples/compute-python-msi-vm/) |
| Ruby   | [Bir MSI ile Azure VM oluşturma](https://azure.microsoft.com/resources/samples/compute-ruby-msi-vm/) |

## <a name="next-steps"></a>Sonraki adımlar

- "Yapılandırma MSI için bir Azure Azure VM temelinde bir kullanıcı tarafından atanan MSI nasıl yapılandıracağınızı öğrenmek için VM" altında ilgili makalelerine bakın.

Geri bildirim sağlamak ve iyileştirmek ve içeriği şekil yardımcı olmak için aşağıdaki açıklamaları bölümü kullanın.
