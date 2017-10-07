---
title: "Güvenli LDAP (LDAPS) Azure AD Etki Alanı Hizmetleri'nde aaaConfigure | Microsoft Docs"
description: "Güvenli LDAP (LDAPS) bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yapılandırın"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
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


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>Görev 3 - güvenli LDAP hello Klasik Azure portalını kullanarak hello yönetilen etki alanı için etkinleştirme
tooenable LDAP güvenli, hello aşağıdaki yapılandırma adımları gerçekleştirin:

1. Toohello gidin  **[Klasik Azure portalı](https://manage.windowsazure.com)**.
2. Select hello **Active Directory** hello sol bölmedeki düğüm.
3. Azure AD Etki Alanı Hizmetleri'ni etkinleştirdiğiniz hello Azure AD dizini (Ayrıca başvurulan tooas 'Kiracı'), seçin.

    ![Azure AD Dizini Seçme](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Merhaba tıklatın **yapılandırma** sekmesi.

    ![Dizinin yapılandır sekmesi](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Başlıklı toohello bölümüne aşağı kaydırın **etki alanı Hizmetleri**. Başlıklı bir seçenek görmelisiniz **güvenli LDAP (LDAPS)** hello ekran aşağıdaki gösterildiği gibi:

    ![Etki Alanı Hizmetleri yapılandırma bölümü](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. Merhaba tıklatın **yapılandırma sertifika...**  hello yukarı düğmesi toobring **güvenli LDAP için sertifika Yapılandır** iletişim.

    ![Güvenli LDAP için sertifika yapılandırma](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. Başlangıç klasörü simgesi aşağıdaki **ile PFX dosyasını sertifika** güvenli LDAP erişim toohello toouse istediğiniz hello sertifikasını içeren toospecify hello PFX dosyası yönetilen etki alanı. Ayrıca hello toohello sertifika.pfx dosyası dışarı aktarılırken belirtilir hello parolayı girin. Merhaba alt düğmesinde bitti hello'ye tıklayın.

    ![Güvenli LDAP PFX dosyası ve parola belirtin](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. Merhaba **etki alanı Hizmetleri** hello bölümünü **yapılandırma** sekmesi gri ve hello olduğu **bekleyen...**  birkaç dakika için durum. Bu süre boyunca hello LDAPS sertifika doğruluğu için doğrulanır ve güvenli LDAP yönetilen etki alanınız için yapılandırılır.

    ![LDAP - bekleme durumunda güvenli](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > Tooenable güvenli LDAP yönetilen etki alanınız için yaklaşık 10 too15 dakika sürer. Merhaba güvenli LDAP sertifika eşleşmiyor sağladıysanız hello ölçütleri gerekli, güvenli LDAP dizin için etkin değil ve bir hata görebilirsiniz. Örneğin, hello etki alanı adı hatalı olduğu, hello sertifikanın süresi dolmuş veya süresi yakında doluyor.
   >
   >

9. Güvenli LDAP başarıyla yönetilen etki alanınız için etkinleştirildiğinde, hello **bekleniyor...**  ileti görünmemelidir. Merhaba sertifikanın parmak izini görüntülenen hello görmeniz gerekir.

    ![Güvenli LDAP Etkin](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>Görev 4 - hello güvenli LDAP erişimi etkinleştirmek Internet
**İsteğe bağlı görev** - LDAPS kullanarak tooaccess hello yönetilen etki alanı düşünmüyorsanız üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.

Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).

1. Bir seçenek çok görmeniz gerekir**etkinleştirmek güvenli LDAP erişim üzerinden INTERNET hello** hello içinde **etki alanı Hizmetleri** hello bölümünü **yapılandırma** sayfası. Bu seçenek çok ayarlanır**Hayır** Internet erişimi toohello yönetilen beri varsayılan etki alanı güvenli LDAP üzerinde varsayılan olarak devre dışıdır.

    ![Güvenli LDAP Etkin](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. İki durumlu **etkinleştirmek güvenli LDAP erişim üzerinden INTERNET hello** çok**Evet**. Merhaba tıklatın **KAYDETMEK** hello alt paneli düğmesinde.
    ![Güvenli LDAP Etkin](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. Merhaba **etki alanı Hizmetleri** hello bölümünü **yapılandırma** sekmesi gri ve hello olduğu **bekleyen...**  birkaç dakika için durum. Bir süre sonra Internet erişim tooyour yönetilen etki alanı güvenli LDAP üzerinden etkinleştirilir.

    ![LDAP - bekleme durumunda güvenli](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > Yaklaşık 10 dakika sürer yönetilen etki alanınız için güvenli LDAP üzerinden tooenable internet erişimi.
   >
   >
4. Güvenli LDAP erişim tooyour Internet başarıyla etkinleştirildi hello etki alanı yönetildiğinde hello **bekleniyor...**  ileti görünmemelidir. Merhaba dış IP adresini görmelisiniz kullanılan tooaccess hello alanında LDAPS üzerinden dizininize olabilir **dış IP adresi için LDAPS erişim**.

    ![Güvenli LDAP Etkin](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Görev 5 - DNS tooaccess hello yönetilen etki alanından hello yapılandırma Internet
**İsteğe bağlı görev** - LDAPS kullanarak tooaccess hello yönetilen etki alanı düşünmüyorsanız üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.

Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 4](#task-4---enable-secure-ldap-access-over-the-internet).

Internet üzerinden güvenli LDAP erişim etkinleştirdikten sonra Merhaba, yönetilen etki alanı için istemci bilgisayarlar bu yönetilen etki alanı bulabilmesi için tooupdate DNS gerekir. Görev 4 Hello sonunda, dış IP adresi üzerinde hello görüntülenir **yapılandırma** sekmesinde **dış IP adresi için LDAPS erişim**.

Dış DNS sağlayıcınız bu hello hello DNS adını (örneğin, ' ldaps.contoso100.com') etki alanı noktaları toothis dış IP adresi yönetilen şekilde yapılandırın. Bizim örneğimizde, DNS girişi aşağıdaki toocreate hello gerekir:

    ldaps.contoso100.com  -> 52.165.38.113

İşte bu kadar - yönetilen hazır tooconnect toohello sunulmuştur hello Internet üzerinden güvenli LDAP kullanarak etki alanı.

> [!WARNING]
> İstemci bilgisayarları hello LDAPS sertifika toobe mümkün tooconnect hello verenin başarıyla güvenmelidir unutmayın toohello yönetilen LDAPS kullanarak etki alanı. Bir kuruluş sertifika yetkilisi veya genel olarak güvenilir bir sertifika yetkilisi kullanıyorsanız, istemci bilgisayarlar bu sertifikayı verenler güven olduğundan, toodo herhangi bir şey gerekmez. Kendinden imzalı bir sertifika kullanıyorsanız, hello istemci bilgisayarda hello güvenilen sertifika deposuna tooinstall hello ortak parçasını hello kendinden imzalı bir sertifika gerekir.
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Kilitleme LDAPS erişim tooyour yönetilen etki alanı hello internet
> [!NOTE]
> **İsteğe bağlı görev** - LDAPS etkinleştirmediyseniz erişim toohello yönetilen etki alanı üzerinde Internet Merhaba, bu yapılandırma görevi atlayın.
>
>

Bu görev başlamadan önce özetlenen hello adımlarını tamamladığınızdan emin olun [görev 4](#task-4---enable-secure-ldap-access-over-the-internet).

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
