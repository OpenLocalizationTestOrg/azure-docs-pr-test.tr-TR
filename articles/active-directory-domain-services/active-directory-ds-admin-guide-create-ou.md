---
title: "Azure Active Directory etki alanı Hizmetleri: Yönetim Kılavuzu | Microsoft Docs"
description: "Azure AD etki alanı Hizmetleri yönetilen etki alanlarında bir kuruluş birimi (OU) oluşturun"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>Bir Azure AD etki alanı Hizmetleri yönetilen etki alanında bir kuruluş birimi (OU) oluşturun
Azure AD etki alanı Hizmetleri yönetilen etki alanı 'AADDC bilgisayarlar' ve 'AADDC kullanıcılar' sırasıyla adlı iki yerleşik kapsayıcı içerir. Merhaba 'AADDC kapsayıcı olan tüm bilgisayarlar için bilgisayar nesneleri olan bilgisayarlar' toohello yönetilen etki alanına katıldı. Merhaba 'AADDC kullanıcılar' kapsayıcı hello Azure AD kiracısında kullanıcıları ve grupları içerir. Bazen, gerekli toocreate hizmet hesaplarını hello yönetilen etki alanı toodeploy iş yükleri üzerinde olabilir. Bu amaçla hello yönetilen etki alanında özel kuruluş birimi (OU) oluşturun ve o OU içinde hizmet hesapları oluşturun. Bu makale size nasıl gösterir toocreate yönetilen etki alanınızdaki bir OU.

## <a name="before-you-begin"></a>Başlamadan önce
Bu makalede listelenen tooperform hello görevleri, aşağıdakiler gerekir:

1. Geçerli bir **Azure aboneliği**.
2. Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.
3. **Azure AD etki alanı Hizmetleri** hello Azure AD dizini için etkinleştirilmesi gerekir. Bunu yapmadıysanız, hello özetlenen tüm hello görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).
4. Bir etki alanına katılmış sanal makine hello Azure AD etki alanı hizmetleri yönetmek, etki alanı yönetilen. Bu tür bir sanal makine yoksa, başlıklı hello makalesinde ana hatlarıyla tüm hello görevleri izleyin [Windows sanal makine tooa yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md).
5. Hello kimlik bilgilerini gereken bir **kullanıcı hesabına ait toohello 'AAD DC Yöneticiler' grubu** dizininizde, toocreate, yönetilen etki alanınızda özel bir OU.

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>Uzaktan Yönetim için etki alanına katılmış bir sanal makine AD yönetim araçlarını yükleyin
Azure AD etki alanı Hizmetleri yönetilen etki alanları, Active Directory Yönetim Merkezi (ADAC) veya AD PowerShell hello gibi bilinen Active Directory yönetim araçlarını kullanarak uzaktan yönetilebilir. Kiracı yöneticileri ayrıcalıkları tooconnect toodomain denetleyicileri hello Uzak Masaüstü aracılığıyla yönetilen etki alanında yok. tooadminister yönetilen etki alanı Merhaba, bir sanal makine birleştirilmiş toohello yönetilen etki alanında hello AD Yönetim Araçları özelliğini yükleyin. Başlıklı toohello makalesine başvurun [Azure AD etki alanı Hizmetleri yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md) yönergeler için.

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>Merhaba yönetilen etki alanında kuruluş birimi oluşturma
Merhaba AD Yönetimsel Araçlar yüklediniz hello üzerinde sanal makine etki alanına katılmış, biz Bu araçlar toocreate hello yönetilen etki alanında bir kuruluş birimi kullanabilirsiniz. Merhaba aşağıdaki adımları gerçekleştirin:

> [!NOTE]
> Yalnızca hello 'AAD DC Yöneticiler' grubunun üyeleri olan hello gerekli ayrıcalıklar toocreate özel bir OU'da. Merhaba toothis grubuna üye olduğu bir kullanıcı olarak aşağıdaki adımları gerçekleştirdiğinizden emin olun.
>
>

1. Merhaba başlangıç ekranından tıklatın **Yönetimsel Araçlar**. Merhaba AD Yönetimsel Araçlar hello sanal makinede yüklü görmeniz gerekir.

    ![Sunucuda yüklü Yönetim Araçları](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Tıklatın **Active Directory Yönetim Merkezi**.

    ![Active Directory Yönetim Merkezi](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooview hello etki alanı, hello etki alanı adı hello sol bölmesinde (örneğin, ' contoso100.com')'yi tıklatın.

    ![ADAC - görünüm etki alanı](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. Merhaba sağ tarafında **görevleri** bölmesinde tıklatın **yeni** hello etki alanı adı düğümü altında. Bu örnekte, ı **yeni** hello sağ tarafında hello 'contoso100(local)' düğümünde **görevleri** bölmesi.

    ![ADAC - yeni OU](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. Merhaba seçeneği toocreate kuruluş birimi görmeniz gerekir. Tıklatın **kuruluş birimi** toolaunch hello **kuruluş birimi oluşturma** iletişim.
6. Merhaba, **kuruluş birimi oluşturma** iletişim kutusunda, belirtin bir **adı** için yeni OU hello. Merhaba OU için kısa bir açıklama sağlayın. Merhaba da yerleştirebilir **yöneten** hello OU için alan. toocreate özel OU Merhaba, tıklatın **Tamam**.

    ![ADAC - Oluştur OU iletişim kutusu](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. OU yeni oluşturulan hello hello AD Yönetim Merkezi (ADAC) artık görünmelidir.

    ![ADAC - oluşturulan OU](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>Yeni oluşturulan OU'lar için izinleri/güvenliği
Varsayılan olarak, özel OU üzerinde yönetim ayrıcalıkları (tam denetim) verilir hello oluşturan hello kullanıcının (Merhaba 'AAD DC Yöneticiler' grup üyesi) hello OU. Hello kullanıcı sonra devam edin ve ayrıcalıkları tooother kullanıcılara veya toohello 'AAD DC Yöneticiler' grubu istenen olarak verin. Aşağıdaki ekran görüntüsü hello görüldüğü gibi kullanıcı hello 'bob@domainservicespreview.onmicrosoft.com' oluşturulan hello yeni 'MyCustomOU' kuruluş birimi tam denetime erişim izni verilmiş.

 ![ADAC - yeni OU güvenlik](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>Notlar özel OU'ları yönetme
Özel bir OU'da oluşturduğunuza göre şimdi ve kullanıcıları, grupları, bilgisayarlar ve hizmet hesapları bu OU'da oluşturun. Kullanıcıları veya grupları 'AADDC kullanıcılar' OU toocustom OU'lar hello taşınamıyor.

> [!WARNING]
> Kullanıcı hesaplarını, grupları, hizmet hesapları ve özel OU'lar altında oluşturduğunuz bilgisayar nesneleri, Azure AD kiracınızda kullanılabilir değil. Diğer bir deyişle, bu nesnelerin hello Azure AD Graph API kullanarak yukarı veya hello Azure AD kullanıcı Arabirimi gösterme. Bu nesneler, yalnızca Azure AD etki alanı Hizmetleri yönetilen etki alanında kullanılabilir.
>
>

## <a name="related-content"></a>İlgili İçerik
* [Azure AD Domain Services tarafından yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md)
* [Yönetilen bir etki alanında Grup İlkesi yapılandırma](active-directory-ds-admin-guide-administer-group-policy.md)
* [Active Directory Yönetim Merkezi: Başlarken](https://technet.microsoft.com/library/dd560651.aspx)
* [Hizmet hesapları adım adım kılavuzu](https://technet.microsoft.com/library/dd548356.aspx)
