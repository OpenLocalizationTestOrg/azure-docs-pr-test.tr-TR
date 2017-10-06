---
title: "Azure Active Directory etki alanı Hizmetleri: Grup İlkesi, yönetilen etki alanlarını yönetme | Microsoft Docs"
description: "Yönetici Grup İlkesi Azure Active Directory etki alanı Hizmetleri, yönetilen etki alanları"
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
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>Grup İlkesi, bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yönetme
Azure Active Directory etki alanı Hizmetleri hello 'AADDC kullanıcılar' ve 'AADDC Bilgisayarları' kapsayıcıları için yerleşik Grup İlkesi nesneleri (GPO'lar) içerir. Bu yerleşik GPO'ları tooconfigure hello yönetilen etki alanı Grup İlkesi özelleştirebilirsiniz. Ayrıca, hello 'AAD DC Yöneticiler' grubunun üyeleri, kendi özel OU'lar hello yönetilen etki alanında oluşturabilirsiniz. Bunlar ayrıca özel GPO'ları oluşturmak ve bunları toothese özel bağlantı OU'lar. Toohello 'AAD DC Administrators' grubuna ait kullanıcılar hello yönetilen etki alanı Grup İlkesi yönetim ayrıcalıkları verilir.

## <a name="before-you-begin"></a>Başlamadan önce
Bu makalede listelenen tooperform hello görevleri, aşağıdakiler gerekir:

1. Geçerli bir **Azure aboneliği**.
2. Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.
3. **Azure AD etki alanı Hizmetleri** hello Azure AD dizini için etkinleştirilmesi gerekir. Bunu yapmadıysanız, hello özetlenen tüm hello görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).
4. A **sanal makine etki alanına katılmış** , yönettiğiniz gelen hello Azure AD etki alanı Hizmetleri yönetilen etki alanı. Bu tür bir sanal makine yoksa, başlıklı hello makalesinde ana hatlarıyla tüm hello görevleri izleyin [Windows sanal makine tooa yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md).
5. Hello kimlik bilgilerini gereken bir **kullanıcı hesabına ait toohello 'AAD DC Yöneticiler' grubu** dizininizde, yönetilen etki alanınız için Grup İlkesi tooadminister.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>Görev 1 - provizyon sanal makine etki alanına katılmış tooremotely hello yönetilen etki alanı için Grup İlkesi yönetme
Azure AD etki alanı Hizmetleri yönetilen etki alanları, Active Directory Yönetim Merkezi (ADAC) veya AD PowerShell hello gibi bilinen Active Directory yönetim araçlarını kullanarak uzaktan yönetilebilir. Benzer şekilde, Grup İlkesi hello yönetilen etki alanı için hello Grup İlkesi yönetim araçları kullanarak uzaktan yönetilebilir.

Azure AD dizininizi yöneticileri ayrıcalıkları tooconnect toodomain denetleyicileri hello Uzak Masaüstü aracılığıyla yönetilen etki alanında yok. Merhaba 'AAD DC Yöneticiler' grubunun üyeleri, Grup İlkesi yönetilen etki alanları için uzaktan yönetebilirsiniz. Bunlar, bir Windows Server/istemcisi bilgisayar birleştirilmiş toohello yönetilen etki alanında Grup İlkesi araçları kullanabilirsiniz. Grup İlkesi araçları, Windows Server ve istemci makinelerde hello Grup İlkesi Yönetimi isteğe bağlı özellik parçası toohello yönetilen etki alanına katılmış olarak yüklenebilir.

Merhaba ilk tooprovision birleştirilmiş toohello yönetilen etki alanı olan bir Windows Server sanal makineye bir görevdir. Yönergeler için başlıklı toohello makalesine başvurun [Windows Server sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>Görev 2 - hello sanal makineye yükleme Grup İlkesi Araçları
Adımları tooinstall hello Grup İlkesi Yönetim Araçları hello etki alanına katılmış sanal makinede aşağıdaki hello gerçekleştirin.

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
9. Merhaba üzerinde **özellikleri** sayfası, select hello **Grup İlkesi Yönetimi** özelliği.

    ![Özellikler sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. Merhaba üzerinde **onay** sayfasında, **yükleme** tooinstall hello Grup İlkesi Yönetimi özelliğini hello sanal makine üzerinde. Özellik yükleme işlemi başarıyla tamamlandığında tıklatın **Kapat** tooexit hello **rol ve Özellik Ekle** Sihirbazı.

    ![Onay sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>Görev 3 - başlatma hello Grup İlkesi Yönetim Konsolu tooadminister Grup İlkesi
Merhaba sanal makine etki alanına katılmış tooadminister hello yönetilen etki alanı Grup İlkesi hello Grup İlkesi Yönetim Konsolu'nu kullanabilirsiniz.

> [!NOTE]
> Toobe hello 'AAD DC Yöneticiler' grubu, tooadminister Grup İlkesi'hello yönetilen etki alanı üyesi gerekir.
>
>

1. Merhaba başlangıç ekranından tıklatın **Yönetimsel Araçlar**. Merhaba görmelisiniz **Grup İlkesi Yönetimi** hello sanal makinede yüklü konsol.

    ![Başlatma Grup İlkesi Yönetimi](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. Tıklatın **Grup İlkesi Yönetimi** toolaunch hello Grup İlkesi Yönetim Konsolu.

    ![Grup İlkesi konsolu](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>Görev 4 - yerleşik Grup İlkesi nesnelerini özelleştirme
İki yerleşik Grup İlkesi nesneleri (GPO'lar) - her biri için hello 'AADDC bilgisayarlar' ve 'AADDC kullanıcılar' kapsayıcılarındaki yönetilen etki alanınız vardır. Bu GPO'ları tooconfigure Grup İlkesi hello yönetilen etki alanında özelleştirebilirsiniz.

1. Merhaba, **Grup İlkesi Yönetimi** tooexpand hello konsolunda, **orman: contoso100.com** ve **etki alanları** , yönetilen etki alanınız için düğümleri toosee hello grup ilkeleri.

    ![Yerleşik GPO'ları](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. Bu yerleşik GPO'ları tooconfigure grup ilkeleri yönetilen etki alanınızda özelleştirebilirsiniz. Merhaba GPO sağ tıklatıp **Düzenle...**  toocustomize hello yerleşik GPO. Merhaba Grup İlkesi yapılandırma Düzenleyicisi araç, toocustomize hello GPO sağlar.

    ![Yerleşik bir GPO'yu düzenleyin](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. Merhaba artık kullanabilirsiniz **Grup İlkesi Yönetimi Düzenleyicisi** tooedit hello yerleşik GPO konsol. Örneğin, ekran aşağıdaki hello nasıl toocustomize hello yerleşik 'AADDC bilgisayarlar' GPO gösterir.

    ![GPO özelleştirme](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>Görev 5 - bir özel Grup İlkesi nesnesi (GPO) oluşturun.
Oluşturun veya kendi özel Grup İlkesi nesneleri içeri aktarın. Ayrıca özel GPO'ları tooa özel bağlayabilirsiniz OU yönetilen etki alanınızda oluşturdunuz. Özel Kuruluş birimi oluşturma hakkında daha fazla bilgi için bkz: [yönetilen bir etki alanına özel bir OU oluşturmanız](active-directory-ds-admin-guide-create-ou.md).

> [!NOTE]
> Toobe hello 'AAD DC Yöneticiler' grubu, tooadminister Grup İlkesi'hello yönetilen etki alanı üyesi gerekir.
>
>

1. Merhaba, **Grup İlkesi Yönetimi** konsolunda, özel, kuruluş birimi (OU) tooselect'ı tıklatın. Merhaba OU'yu sağ tıklatın ve **bu etki alanında GPO oluştur ve buraya bağla...** .

    ![Özel bir GPO oluşturun](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. Merhaba yeni GPO için bir ad belirtin ve tıklayın **Tamam**.

    ![GPO için bir ad belirtin](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. Yeni bir GPO oluşturulur ve bağlı tooyour özel OU. Merhaba GPO sağ tıklatıp **Düzenle...**  hello menüsünde.

    ![Yeni oluşturulmuş GPO](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. Yeni oluşturulan hello GPO'yu hello kullanarak özelleştirebileceğiniz **Grup İlkesi Yönetimi Düzenleyicisi**.

    ![Yeni GPO özelleştirme](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


Kullanma hakkında daha fazla bilgi [Grup İlkesi Yönetim Konsolu](https://technet.microsoft.com/library/cc753298.aspx) Technet üzerindeki kullanılabilir.

## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Windows Server sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md)
* [Azure AD Domain Services tarafından yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md)
* [Grup İlkesi Yönetim Konsolu](https://technet.microsoft.com/library/cc753298.aspx)
