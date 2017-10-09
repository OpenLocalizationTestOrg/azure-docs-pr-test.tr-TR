---
title: "Azure aaaUse Windows istemci görüntüleri | Microsoft Docs"
description: "Nasıl toouse Visual Studio abonelik geliştirme ve test senaryoları için toodeploy Windows 7, Windows 8 veya Windows 10 Azure avantaj"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Windows İstemcisi Azure üzerinde geliştirme ve test senaryoları için kullanın.
Windows 10 azure'da geliştirme ve test senaryoları için uygun bir Visual Studio (önceki adıyla MSDN) aboneliğiniz olması koşuluyla veya Windows 7, Windows 8 kullanabilirsiniz. Bu makalede Azure galeri görüntüleri Windows İstemcisi Azure ve hello kullanımını çalıştırmak için hello uygunluk gereksinimleri özetlenmektedir.

## <a name="subscription-eligibility"></a>Abonelik uygunluk
Etkin Visual Studio abonelerinden (bir Visual Studio abonelik lisans kişiler) Windows İstemcisi geliştirme ve sınama amacıyla kullanabilirsiniz. Windows İstemcisi, kendi donanım ve herhangi bir türde Azure aboneliği çalışan Azure sanal makineler üzerinde kullanılabilir. Windows İstemcisi etkin Visual Studio abonelerinden olmayan kişiler tarafından kullanılan veya normal üretim kullanımı için Azure üzerinde kullanılan dağıtılan tooor olmayabilir.

Size kolaylık olması için biz belirli Windows 10 görüntüleri kullanılabilir içinde hello Azure galerisinden yaptığınız [uygun geliştirme ve test sunar](#eligible-offers). Visual Studio abonelerinden teklif herhangi bir türde içinde için de [yeterli hazırlayın ve oluşturun](prepare-for-upload-vhd-image.md) bir 64-bit Windows 7, Windows 8 veya Windows 10 görüntüsü ve ardından [tooAzure karşıya](upload-generalized-managed.md). Hello kullan sınırlı toodev ve test etkin Visual Studio aboneler tarafından kalır.

## <a name="eligible-offers"></a>Uygun teklifleri
Aşağıdaki tabloda Ayrıntılar hello hello uygun toodeploy Windows 10'hello Azure Galerisi aracılığıyla kimliklerini sunar. Merhaba Windows 10 görüntüleri yalnızca teklifleri aşağıdaki görünür toohello bağımsızdır. Visual Studio abonelerinden farklı Teklif türü toorun Windows istemcisinde duyan, çok[yeterli hazırlayın ve oluşturun](prepare-for-upload-vhd-image.md) bir 64-bit Windows 7, Windows 8 veya Windows 10 görüntüsü ve [tooAzurekarşıyayükleme](upload-generalized-managed.md).

| Teklif Adı | Teklif Numarası | Kullanılabilir istemci görüntüleri |
|:--- |:---:|:---:|
| [Kullandıkça Öde geliştirme ve Test](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Visual Studio Enterprise (MPN) aboneleri](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Visual Studio Professional aboneleri](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Visual Studio Test uzmanı aboneleri](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium with MSDN (avantajı)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Visual Studio Enterprise aboneleri](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Visual Studio Enterprise (BizSpark) aboneleri](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Enterprise geliştirme ve Test](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Azure aboneliğiniz denetleyin
Teklif kimliği bilmiyorsanız hello bu iki yoldan biriyle Azure portal aracılığıyla elde edebilirsiniz:  

- Merhaba 'Subscriptions' dikey penceresinde:

  ![Teklif kimliği ayrıntıları hello Azure portalı](./media/client-images/offer-id-azure-portal.png) 

- Veya tıklatın **faturalama** ve abonelik kimliğinizi tıklatın Merhaba Teklif kimliği hello faturalama dikey penceresinde görüntülenir.

Merhaba hello Teklif kimliği de görüntüleyebilirsiniz ['Abonelik' sekmesini](http://account.windowsazure.com/Subscriptions) hello Azure hesap portalı:

![Teklif kimliği ayrıntıları hello Azure hesap portalından](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>Sonraki adımlar
Kullanarak, Vm'lerde artık dağıtabilirsiniz [PowerShell](quick-create-powershell.md), [Resource Manager şablonları](ps-template.md), veya [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

