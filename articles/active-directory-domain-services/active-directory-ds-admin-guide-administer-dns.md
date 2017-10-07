---
title: "Azure Active Directory etki alanı Hizmetleri: Yönetilen etki alanları DNS yönetme | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri yönetilen etki alanları DNS yönetme"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>Bir Azure AD etki alanı Hizmetleri yönetilen etki alanının DNS yönetme
Azure Active Directory etki alanı Hizmetleri hello yönetilen etki alanı için DNS çözümlemesi sağlayan bir DNS (etki alanı adı çözümlemesine) sunucusu içerir. Bazen, tooconfigure hello yönetilen etki alanı DNS gerekebilir. Birleştirilmiş toohello etki alanı olmayan makinelere yük Dengeleyiciler için sanal IP adreslerini yapılandırın veya dış DNS ileticileri Kurulum toocreate DNS kayıtlarını gerekebilir. Bu nedenle, toohello 'AAD DC Administrators' grubuna ait kullanıcılar hello yönetilen etki alanı DNS yönetim ayrıcalıkları verilir.

## <a name="before-you-begin"></a>Başlamadan önce
Bu makalede listelenen tooperform hello görevleri, aşağıdakiler gerekir:

1. Geçerli bir **Azure aboneliği**.
2. Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.
3. **Azure AD etki alanı Hizmetleri** hello Azure AD dizini için etkinleştirilmesi gerekir. Bunu yapmadıysanız, hello özetlenen tüm hello görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).
4. A **sanal makine etki alanına katılmış** , yönettiğiniz gelen hello Azure AD etki alanı Hizmetleri yönetilen etki alanı. Bu tür bir sanal makine yoksa, başlıklı hello makalesinde ana hatlarıyla tüm hello görevleri izleyin [Windows sanal makine tooa yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md).
5. Hello kimlik bilgilerini gereken bir **kullanıcı hesabına ait toohello 'AAD DC Yöneticiler' grubu** dizininizde, yönetilen etki alanınız için DNS tooadminister.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>Görev 1 - provizyon sanal makine etki alanına katılmış tooremotely hello yönetilen etki alanı için DNS yönetme
Azure AD etki alanı Hizmetleri yönetilen etki alanları, Active Directory Yönetim Merkezi (ADAC) veya AD PowerShell hello gibi bilinen Active Directory yönetim araçlarını kullanarak uzaktan yönetilebilir. Benzer şekilde, hello yönetilen etki alanı için DNS hello DNS sunucu yönetim araçları kullanarak uzaktan yönetilebilir.

Azure AD dizininizi yöneticileri ayrıcalıkları tooconnect toodomain denetleyicileri hello Uzak Masaüstü aracılığıyla yönetilen etki alanında yok. Merhaba 'AAD DC Yöneticiler' grubunun üyeleri, yönetilen etki alanına katılmış toohello bir Windows Server/istemci bilgisayardan DNS sunucu araçları kullanarak uzaktan yönetilen etki alanları için DNS yönetebilirsiniz. DNS sunucusu araçları hello Uzak Sunucu Yönetim Araçları (RSAT) Windows Server'da isteğe bağlı bir özellik bir parçası olarak yüklenebilir ve istemci makineleri toohello yönetilen etki alanına katıldı.

Merhaba ilk tooprovision birleştirilmiş toohello yönetilen etki alanı olan bir Windows Server sanal makineye bir görevdir. Yönergeler için başlıklı toohello makalesine başvurun [Windows Server sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>Görev 2 - hello sanal makineye yükleme DNS Sunucusu Araçları
Adımları tooinstall hello DNS Yönetim Araçları hello etki alanına katılmış sanal makinede aşağıdaki hello gerçekleştirin. Daha fazla bilgi için [yükleme ve uzak sunucu yönetim araçları kullanarak](https://technet.microsoft.com/library/hh831501.aspx), Technet konusuna bakın.

1. Çok gidin**sanal makineleri** hello Klasik Azure portalı düğümünde. Görev 1'de oluşturduğunuz Hello sanal makineyi seçin ve tıklatın **Bağlan** hello hello pencerenin hello altındaki komut çubuğunda.

    ![TooWindows sanal makineye bağlanma](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. Merhaba Klasik portal tooopen komut istemleri veya kullanılan tooconnect toohello sanal makine olduğu '.rdp' uzantılı bir dosyayı kaydedin. Yükleme tamamlandığında hello dosyasına tıklayın.
3. Merhaba oturum açma isteminde hello toohello 'AAD DC Yöneticiler' grubuna ait olan bir kullanıcı kimlik bilgilerini kullanın. Örneğin, kullandığımız 'bob@domainservicespreview.onmicrosoft.com' bizim durumda.
4. Merhaba başlangıç ekranından açmak **Sunucu Yöneticisi'ni**. Tıklatın **rol ve Özellik Ekle** hello merkezi bölmesinde hello Sunucu Yöneticisi penceresi.

    ![Sanal makine üzerinde Sunucu Yöneticisi'ni başlatın](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. Merhaba üzerinde **başlamadan önce** hello sayfasının **Ekle roller ve Özellikler Sihirbazı**, tıklatın **sonraki**.

    ![Başlamadan önce sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. Merhaba üzerinde **yükleme türü** sayfasında, hello bırakın **rol tabanlı veya özellik tabanlı yükleme** işaretli seçeneğini ve tıklayın **sonraki**.

    ![Yükleme türü sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. Merhaba üzerinde **sunucu seçimi** sayfasında hello sunucu havuzundan hello geçerli sanal makine seçin ve tıklatın **sonraki**.

    ![Sunucu seçimi sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. Merhaba üzerinde **sunucu rolleri** sayfasında, **sonraki**. Biz herhangi bir rol hello sunucusuna yüklemiyorsanız beri Biz bu sayfayı atla.
9. Merhaba üzerinde **özellikleri** tooexpand hello sayfasında, **Uzak Sunucu Yönetim Araçları** düğümü ve tooexpand hello ardından **Rol Yönetim Araçları** düğümü. Seçin **DNS Sunucusu Araçları** Rol Yönetim Araçları'nın hello listeden özelliği.

    ![Özellikler sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. Merhaba üzerinde **onay** sayfasında, **yükleme** tooinstall hello DNS sunucu araçları hello sanal makinede özelliği. Özellik yükleme işlemi başarıyla tamamlandığında tıklatın **Kapat** tooexit hello **rol ve Özellik Ekle** Sihirbazı.

    ![Onay sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>Görev 3 - başlatma hello DNS Yönetim Konsolu tooadminister DNS
Etki alanına katılmış sanal makine Hello DNS Sunucusu Araçları özelliği yüklü Merhaba, hello DNS araçları tooadminister DNS hello yönetilen etki alanında kullanabilirsiniz.

> [!NOTE]
> Toobe tooadminister hello yönetilen etki alanı DNS hello 'AAD DC Yöneticiler' grubunun bir üyesine gerekir.
>
>

1. Merhaba başlangıç ekranından tıklatın **Yönetimsel Araçlar**. Merhaba görmelisiniz **DNS** hello sanal makinede yüklü konsol.

    ![Yönetim Araçları - DNS konsolunu](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. Tıklatın **DNS** toolaunch hello DNS Yönetim Konsolu.
3. Merhaba, **tooDNS sunucu bağlanmak** iletişim kutusunda, başlıklı hello seçeneğini **hello bilgisayar**ve hello yönetilen etki alanının (örneğin, ' contoso100.com') hello DNS etki alanı adını girin.

    ![DNS konsolunu - toodomain Bağlan](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. Merhaba DNS konsolunu toohello yönetilen etki alanına bağlanır.

    ![DNS konsolunu - etki alanını yönetme](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. Merhaba DNS konsolunu tooadd DNS girişlerini artık AAD etki alanı Hizmetleri'ni etkinleştirdikten hello sanal ağ içindeki bilgisayarlar için de kullanabilirsiniz.

> [!WARNING]
> Yönetilen DNS yönetim araçları kullanarak etki alanı DNS Merhaba yönetme dikkatli olun. Sağlamak sizin **silmeyin veya hello etki alanındaki etki alanı Hizmetleri tarafından kullanılan hello yerleşik DNS kayıtlarını değiştirme**. Yerleşik DNS kayıtları etki alanı DNS kayıtları, ad sunucusu kayıtlarını ve DC konumu için kullanılan diğer kayıtlarını içerir. Bu kayıtları değiştirirseniz, etki alanı Hizmetleri hello sanal ağda herhangi bir kesinti.
>
>

Merhaba bkz [DNS araçları Technet makalesi](https://technet.microsoft.com/library/cc753579.aspx) DNS yönetme hakkında daha fazla bilgi için.

## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Windows Server sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md)
* [Azure AD Domain Services tarafından yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md)
* [DNS Yönetim Araçları](https://technet.microsoft.com/library/cc753579.aspx)
