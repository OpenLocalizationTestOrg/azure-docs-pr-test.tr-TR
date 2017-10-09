---
title: "Azure Active Directory etki alanı Hizmetleri: hello Azure AD DC Yöneticiler grubu oluşturma | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir
Bu makalede ve sizin tooenable Azure Active Directory etki alanı Hizmetleri (Azure AD DS) Azure Active Directory (Azure AD) kiracınız için gerekli olan hello yapılandırma görevleri anlatılmaktadır.

> [!NOTE]
> [**Bunun yerine Hello yeni (Önizleme) Azure portal deneyimi deneyin**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>Görev 1: hello Azure AD DC Yöneticiler grubu oluşturma
Merhaba ilk toocreate Azure AD kiracınıza yönetim grubunda bir görevdir. Bu özel yönetim grubu adı *AAD DC Yöneticiler*. Bu grubun üyeleri, etki alanına katılmış toohello Azure Active Directory etki alanı Hizmetleri tarafından yönetilen etki alanı olan makinelere sunucuda yönetici izinleri verilir. Etki alanına katılmış makinelerde toohello Yöneticiler grubunun bu gruba eklenir. Ayrıca, bu grubun üyeleri, Uzak Masaüstü tooconnect uzaktan toodomain katılmış makineler kullanabilirsiniz.  

> [!NOTE]
> Azure Active Directory etki alanı Hizmetleri kullanılarak oluşturulan hello yönetilen etki alanındaki etki alanı yöneticisi veya kuruluş yöneticisi izinlerine sahip değil. Yönetilen etki alanlarında, bu izinleri hello hizmeti tarafından ayrılmış ve hello Kiracı içinde kullanılabilir toousers duruma getirilmez. Hello özel yönetim grubu oluşturulan kullanabilirsiniz ancak bu yapılandırma görevi tooperform bazı işlemleri ayrıcalıklı. Bu işlemler, bilgisayarlar toohello etki alanına katılma, etki alanına katılan makineler toohello yönetim grubuna ait ve Grup İlkesi yapılandırma içerir.
>

Bu yapılandırma görevde hello yönetim grubu oluşturun ve bir veya daha fazla kullanıcı dizin toohello grubunuza ekleyin. Azure Active Directory etki alanı Hizmetleri, toocreate hello yönetim grubu hello aşağıdaki:

1. Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba Hello sol bölmesinde seçin **Active Directory** düğmesi.
3. Tooenable Azure Active Directory etki alanı Hizmetleri istediğiniz hello Azure AD kiracısını (dizin) seçin. Her Azure AD dizini için yalnızca bir etki alanı oluşturabilirsiniz.

    ![Azure AD dizini seçin](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Merhaba üzerinde **Önizleme dizin** hello sayfasında, **grupları** sekmesi.
5. hello görev bölmesinde hello pencerenin hello altındaki bir grubun tooyour Azure AD Kiracı tooadd tıklatın **Grup Ekle**.

    ![Merhaba Grup Ekle düğmesi](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. Merhaba, **Grup Ekle** iletişim kutusunda, adlı bir grup oluşturun **AAD DC Yöneticiler**ve ardından **grup türü** çok**güvenlik**.

   > [!WARNING]
   > Azure Active Directory etki alanı Hizmetleri tarafından yönetilen etki alanınızda, tooenable erişim tam bu ada sahip bir grup oluşturun.
   >
   >

    ![Merhaba Grup Ekle iletişim kutusu](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. Merhaba, **açıklama** kutusuna, diğerleri sağlayan bir açıklama girin toounderstand bu grup içinde Azure Active Directory etki alanı yönetim izinleri verir.
8. Hello grubu oluşturduktan sonra hello grup adı tooview, Özellikler'i tıklatın.
9. Merhaba pencerenin hello altındaki hello grubunun üyeleri olarak tooadd kullanıcılar'ı hello **Add Members** düğmesi.

    ![Grup üyeleri düğme ekleme](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. Merhaba, **üye eklemek** iletişim kutusu,, bu grubun üyesi olması ve hello hello onay işareti simgesine tıklayın select hello kullanıcılar alt sağ.

    ![Kullanıcıların tooadministrators grubu Ekle](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Sonraki adım
[Görev 2: oluşturun veya bir Azure sanal ağı seçin](active-directory-ds-getting-started-vnet.md)
