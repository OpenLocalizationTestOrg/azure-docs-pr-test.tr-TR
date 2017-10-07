---
title: "Güvenli LDAP (LDAPS) Azure AD Etki Alanı Hizmetleri'nde aaaConfigure | Microsoft Docs"
description: "Güvenli LDAP (LDAPS) bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yapılandırın"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Güvenli LDAP (LDAPS) Azure AD etki alanı Hizmetleri yönetilen etki alanı için yapılandırma

## <a name="before-you-begin"></a>Başlamadan önce
Tamamlandı olun [görev 2 - verme hello güvenli LDAP sertifika tooa. PFX dosyası](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Toouse Önizleme Azure portal deneyimi hello veya bu görevi Azure Klasik portalı toocomplete hello seçin.
> [!div class="op_single_selector"]
> * **Azure portal (Önizleme)**: [etkinleştir LDAP hello Azure portal kullanarak güvenli](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Klasik Azure portalı**: [etkinleştir güvenli LDAP hello Klasik Azure portalını kullanarak](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>Görev 3 - güvenli LDAP hello Azure portal (Önizleme) kullanarak hello yönetilen etki alanı için etkinleştirme
tooenable LDAP güvenli, hello aşağıdaki yapılandırma adımları gerçekleştirin:

1. Toohello gidin  **[Azure portal](https://portal.azure.com)**.

2. ' Etki alanı Hizmetleri'nde' hello Ara **arama kaynakları** arama kutusu. Seçin **Azure AD etki alanı Hizmetleri** hello arama sonuç. Merhaba **Azure AD etki alanı Hizmetleri** dikey penceresinde, yönetilen etki alanınız listelenir.

    ![Yönetilen etki alanı sağlanacak Bul](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Merhaba etki alanı hakkında daha fazla ayrıntı hello yönetilen etki alanı (örneğin, ' contoso100.com') toosee Hello adına tıklayın.

    ![Etki alanı hizmetleri - sağlama durumu](./media/getting-started/domain-services-provisioning-state.png)

3. Tıklatın **güvenli LDAP** hello Gezinti Bölmesi.

    ![Etki Alanı Hizmetleri - güvenli LDAP dikey penceresi](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. Varsayılan olarak güvenli LDAP erişim tooyour yönetilen etki alanı devre dışıdır. İki durumlu **güvenli LDAP** çok**etkinleştirmek**.

    ![Güvenli LDAP etkinleştir](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. Varsayılan olarak, güvenli LDAP erişim tooyour etki alanı Internet devre dışı hello yönetilir. İki durumlu **Internet üzerinden güvenli LDAP erişim izni ver hello** çok**etkinleştirmek**istenirse. 

6. Başlangıç klasörü simgesi aşağıdaki **. Güvenli LDAP Sertifika PFX dosyası**. Güvenli LDAP erişim toohello yönetilen etki alanı için hello sertifikasıyla Hello yol toohello PFX dosyası belirtin.

7. Merhaba belirtin **parola toodecrypt. PFX dosyası**. Merhaba sağlamak hello toohello sertifika.pfx dosyası dışa aktarırken kullanılan aynı parola.

8. İşiniz bittiğinde, hello tıklatın **kaydetmek** düğmesi.

9. Güvenli LDAP hello yönetilen etki alanı için yapılandırılmış bildiren bir bildirim görür. Bu işlem tamamlanana kadar diğer hello etki alanı ayarlarını değiştiremezsiniz.

    ![Güvenli LDAP hello yönetilen etki alanı için yapılandırma](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> Tooenable güvenli LDAP yönetilen etki alanınız için yaklaşık 10 too15 dakika sürer. Merhaba güvenli LDAP sertifika eşleşmiyor sağladıysanız hello ölçütleri gerekli, güvenli LDAP dizin için etkin değil ve bir hata görebilirsiniz. Örneğin, hello etki alanı adı hatalı olduğu, hello sertifikanın süresi dolmuş veya süresi yakında doluyor. Bu durumda, geçerli bir sertifikayla yeniden deneyin.
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Görev 4 - DNS tooaccess hello yönetilen etki alanından hello yapılandırma Internet
> [!NOTE]
> **İsteğe bağlı görev** - LDAPS kullanarak tooaccess hello yönetilen etki alanı düşünmüyorsanız üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.
>
>

Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Internet üzerinden güvenli LDAP erişim etkinleştirdikten sonra Merhaba, yönetilen etki alanı için istemci bilgisayarlar bu yönetilen etki alanı bulabilmesi için tooupdate DNS gerekir. Görev 3 Hello sonunda, dış IP adresi üzerinde hello görüntülenir **özellikleri** dikey penceresinde **dış IP adresi için LDAPS erişim**.

Dış DNS sağlayıcınız bu hello hello DNS adını (örneğin, ' ldaps.contoso100.com') etki alanı noktaları toothis dış IP adresi yönetilen şekilde yapılandırın. Bizim örneğimizde, DNS girişi aşağıdaki toocreate hello gerekir:

    ldaps.contoso100.com  -> 52.165.38.113

İşte bu kadar - yönetilen hazır tooconnect toohello sunulmuştur hello Internet üzerinden güvenli LDAP kullanarak etki alanı.

> [!WARNING]
> İstemci bilgisayarları hello LDAPS sertifika toobe mümkün tooconnect hello verenin başarıyla güvenmelidir unutmayın toohello yönetilen LDAPS kullanarak etki alanı. Genel olarak güvenilir bir sertifika yetkilisi kullanıyorsanız, istemci bilgisayarlar bu sertifikayı verenler güven olduğundan, toodo herhangi bir şey gerekmez. Kendinden imzalı bir sertifika kullanıyorsanız, hello otomatik olarak imzalanan sertifika ortak parçasını hello hello istemci bilgisayarda hello güvenilen sertifika deposuna yükleyin.
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Görev 5 - kilitleme LDAPS erişim tooyour yönetilen etki alanı üzerinde hello Internet
> [!NOTE]
> **İsteğe bağlı görev** - LDAPS etkinleştirmediyseniz erişim toohello yönetilen etki alanı üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.
>
>

Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Internet hello yönetilen etki alanınız LDAPS erişim için gösterme bir güvenlik tehdidi temsil eder. Merhaba yönetilen etki hello erişilebildiğinden güvenli LDAP için kullanılan hello noktasındaki Internet (diğer bir deyişle, bağlantı noktası 636). Bu nedenle, IP adreslerini bilinen toorestrict erişim toohello yönetilen etki alanı toospecific seçebilirsiniz. Gelişmiş güvenlik için bir ağ güvenlik grubu (NSG) oluşturun ve Azure AD Etki Alanı Hizmetleri'ni etkinleştirdiğiniz hello alt ağı ile ilişkilendirin.

Merhaba aşağıdaki tabloda gösterilmektedir örnek yapılandırabilirsiniz, NSG toolock hello üzerinden güvenli LDAP erişim tuşunu Internet. Merhaba NSG gelen LDAPS erişim TCP bağlantı noktası IP adreslerinin üzerinden 636 belirtilen kümesinden yalnızca izin veren kurallar kümesini içerir. Merhaba varsayılan 'DenyAll' Kural tooall diğer gelen trafiği hello geçerlidir Internet. Merhaba NSG kuralı tooallow LDAPS erişimi hello üzerinden internet'ten belirtilen IP adreslerini hello DenyAll NSG kural daha yüksek önceliğe sahiptir.

![Merhaba Internet üzerinden örnek NSG toosecure LDAPS erişim](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Daha fazla bilgi** - [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>İlgili içerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Azure AD Domain Services tarafından yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md)
* [Grup İlkesi, bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-group-policy.md)
* [Ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md)
* [Bir ağ güvenlik grubu oluşturun](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
