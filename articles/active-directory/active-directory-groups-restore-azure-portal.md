---
title: "Azure Active Directory'de aaaRestore silinmiş bir Office 365 Grup | Microsoft Docs"
description: "Azure Active Directory'deki bir gruba toorestore silinen bir grupta, görünüm geri yüklenebilen grupları ve permamnently delete nasıl"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Azure Active Directory silinen bir Office 365 grubunda geri yükleme

Hello Azure Active Directory (Azure AD) bir Office 365 grubunda sildiğinizde, silinen hello 30 gün boyunca hello silme tarihinden tutulan ancak görünür grubudur. Bu, böylelikle Hello grup ve içeriği gerekirse geri yüklenebilir. Bu işlev sınırlandırılır özel olarak tooOffice 365 gruplarında Azure AD. Güvenlik grupları ve dağıtım grupları için kullanılabilir değil.

> [!NOTE] 
> Kullanmayan `Remove-MsolGroup` hello Grup kalıcı olarak temizler olduğundan. Her zaman kullanmak `Remove-AzureADMSGroup` toodelete bir O365 grubu. 

gerekli Hello izinler toorestore bir grup hello aşağıdakilerden herhangi birini olabilir:

Rol  | İzinler 
--------- | ---------
Şirket Yöneticisi, iş ortağı Tier2 destek ve Intune hizmet yöneticileri | Silinen tüm Office 365 grup geri yükleyebilirsiniz 
Kullanıcı hesabı yönetici ve iş ortağı Tier1 desteği | Silinen herhangi bir Office 365 grup şirket yöneticisi rolüne atanan bu toohello dışında geri yükleyebilirsiniz 
Kullanıcı | Bunlar ait silinen tüm Office 365 grup geri yükleyebilirsiniz 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>Görünüm Merhaba, kullanılabilir toorestore Office 365 gruplarını silindi
olanları ilgilendiğiniz değil henüz kalıcı olarak temizlenmiş veya cmdlet'leri aşağıdaki hello bir hello kullanılan tooview silinmiş hello grupları tooverify olabilir. Bu cmdlet'ler hello parçası olan [Azure AD PowerShell Modülü](https://www.powershellgallery.com/packages/AzureAD/). Bu modül hakkında daha fazla bilgi hello bulunabilir [Azure Active Directory PowerShell sürüm 2](/powershell/azure/install-adv2?view=azureadps-2.0) makalesi.

1.  Aşağıdaki cmdlet'i toodisplay tüm çalışma hello hala kullanılabilir toorestore kiracınızda Office 365 grupları silindi.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  Alternatif olarak, belirli bir grubun hello objectID bildiğiniz (ve 1. adımda hello cmdlet'inden alma varsa), belirli silinen grubun hello cmdlet tooverify aşağıdaki çalışma hello henüz kalıcı olarak temizlendi değil.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>Nasıl toorestore, Office 365 grubu silindi
Hala kullanılabilir toorestore bu hello grubudur doğruladıktan sonra geri yükleme hello aşağıdaki adımları hello biriyle grubu silindi. Merhaba grubu belgeleri, SP siteleri veya diğer kalıcı nesne içeriyorsa, bir grup ve içeriği too24 saatleri toofully geri geçmesi gerekebilir.

1.  Çalışma hello cmdlet toorestore hello grup ve içeriği aşağıdaki.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

Alternatif olarak, hello aşağıdaki cmdlet'i toopermanently Kaldır silinmiş hello Grup çalıştırılabilir.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>Bu çalışılan nasıl bilebilirsiniz?
Merhaba çalıştırmak bir Office 365 Grup başarıyla geri döndürdük tooverify `Get-AzureADGroup –ObjectId <objectId>` hello grubuyla ilgili cmdlet toodisplay bilgileri. Merhaba geri yüklendikten sonra isteği tamamlandı:
- Merhaba Grup Exchange hello sol gezinti çubuğunda görünür
- Merhaba grubu için Hello planı Planlayıcı görünür
- Tüm Sharepoint siteleri ve tüm içerikleri kullanılabilir olacak
- Merhaba Grup herhangi hello Exchange uç noktaları ve Office 365 grupları destekleyen diğer Office 365 iş yükü erişilebilir


## <a name="next-steps"></a>Sonraki adımlar
Bu makaleler Azure Active Directory gruplarına ek bilgiler sağlar.

* [Var olan grupları bakın](active-directory-groups-view-azure-portal.md)
* [Bir grubu ayarlarını yönetme](active-directory-groups-settings-azure-portal.md)
* [Bir grubun üyelerini yönetmek](active-directory-groups-members-azure-portal.md)
* [Bir grubun üyeliğini yönetme](active-directory-groups-membership-azure-portal.md)
* [Bir gruptaki kullanıcılar için dinamik kurallarını yönet](active-directory-groups-dynamic-membership-azure-portal.md)
