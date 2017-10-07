---
title: "aaaPreview Office 365 grupları Azure Active Directory'de sona erme | Microsoft Docs"
description: "Office 365 için sona erme yukarı tooset Azure Active Directory'de (Önizleme) nasıl grupları"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>Office 365 grupları süre sonu (Önizleme) yapılandırma

Seçtiğiniz herhangi bir Office 365 grup için sona erme ayarlayarak artık Office 365 grupları hello yaşam döngüsü yönetebilirsiniz. Bu süre sonu ayarladıktan sonra bu grupları sahipleri olan hala hello grupları gerekiyorsa bunları gruplara toorenew sorulan. Değil yenilendiğinden herhangi bir Office 365 grubu silinir. Silindi herhangi bir Office 365 grubu 30 gün içinde hello Grup sahipleri veya hello Yöneticisi tarafından geri yüklenebilir.  


> [!NOTE]
> Süre sonu yalnızca Office 365 grupları için ayarlayabilirsiniz.
>
> O365 grupları için sona erme ayarlamak için bir Azure AD Premium lisansı atanmış gerekiyor
>   - Merhaba Kiracı hello süre sonu ayarlarını yapılandıran hello Yöneticisi
>   - Bu ayar için seçilmiş hello grupları tüm üyeleri

## <a name="set-office-365-groups-expiration"></a>Office 365 grupları sona erme ayarlayın

1. Açık hello [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) Azure AD kiracınızda genel yönetici olan bir hesapla.

2. Açık Azure AD, select **kullanıcılar ve gruplar**.

3. Seçin **grup ayarları** ve ardından **sona erme** tooopen hello sona erme ayarları.
  
  ![Sona erme dikey penceresi](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. Merhaba üzerinde **sona erme** dikey penceresinde aşağıdakileri yapabilirsiniz:

  * Merhaba Grup ömrü gün olarak ayarlayın. Aşağıdakilerden birini seçebilirsiniz hello önceden değerleri veya (olmalıdır 31 gün veya daha fazla) özel bir değer. 
  * Bir grup sahibi olduğunda burada hello yenileme ve süre sonu bildirimleri gönderilmesi gereken bir e-posta adresi belirtin. 
  * Office 365 grupları sona seçin. Süre sonu için etkinleştirebilirsiniz **tüm** Office 365 grupları hello Office 365 grupları kümelerini seçebilirsiniz veya seçtiğiniz **hiçbiri** süre sonu tüm gruplar için devre dışı bırakmak için.
  * Seçerek bittiğinde ayarlarınızı kaydetmek **kaydetmek**.

Microsoft PowerShell modülü tooconfigure sona erme tarihi Office 365 grupları PowerShell aracılığıyla nasıl toodownload ve yükleme hello ile ilgili yönergeler için bkz: [Azure Active Directory V2 PowerShell modülü - genel Önizleme sürümü 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).

Bunun gibi e-posta bildirimleri toohello Office 365 Grup sahiplerinin 30 gün, 15 gün ve 1 gün önceki tooexpiration hello grubunun gönderilir.

![Sona erme e-posta bildirimi](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

Merhaba Grup sahibi seçip **yenileme grup** toorenew Office 365 Grup hello ya da seçebilirsiniz **Git toogroup** toosee hello üyeleri ve ilgili diğer ayrıntıları hello grubu.

Bir grup süresi dolduğunda hello Grup bir gün hello sona erme tarihinden sonra silinir. Merhaba geçerlilik süresi ve bunların Office 365 grubunun sonraki silinmesi hakkında bildiren toohello Office 365 Grup sahipleri bunun gibi bir e-posta bildirimi gönderilir.

![Grup silme e-posta bildirimi](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

Merhaba grubu geri yükleyebilirsiniz seçerek **geri yükleme grup** veya [geri yükleme silinmiş bir Office 365 Grup Azure Active Directory'de] bölümünde açıklanan PowerShell cmdlet'lerini kullanarak (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).
    
Merhaba grubu geri yüklemekte belgeler, SharePoint siteleri veya diğer kalıcı nesne içeriyorsa, too24 saatleri toofully geri yükleme hello grup ve içeriği alabilir.

> [!NOTE]
> * Merhaba sona erme ayarları dağıtırken hello sona erme penceresinden daha eski olan bazı grupları olabilir. Bu gruplar olması hemen silinmez, ancak olan too30 gün dolmasına ayarlayın. bir gün içinde Hello ilk yenileme bildirim e-posta gönderilir. Örneğin, grubu A, 400 gün önce oluşturulduğu ve hello sona erme aralığını ayarlanmış too180 gün. Sona erme tarihi geçerli olduğunda, onu hello sahibi yeniler sürece gruba silinmeden önce 30 gün sahiptir.
> * Dinamik bir grup silinir ve geri, yeni Grup ve yeniden doldurulan according toohello kural görülür. Bu işlemin too24 saat sürebilir.

## <a name="next-steps"></a>Sonraki adımlar
Bu makaleler Azure AD grupları hakkında ek bilgiler sağlar.

* [Var olan grupları bakın](active-directory-groups-view-azure-portal.md)
* [Bir grubu ayarlarını yönetme](active-directory-groups-settings-azure-portal.md)
* [Bir grubun üyelerini yönetmek](active-directory-groups-members-azure-portal.md)
* [Bir grubun üyeliğini yönetme](active-directory-groups-membership-azure-portal.md)
* [Bir gruptaki kullanıcılar için dinamik kurallarını yönet](active-directory-groups-dynamic-membership-azure-portal.md)
