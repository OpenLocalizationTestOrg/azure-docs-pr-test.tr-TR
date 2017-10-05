---
title: "Güvenli LDAP (LDAPS) Azure AD Etki Alanı Hizmetleri'nde yapılandırma | Microsoft Docs"
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
ms.openlocfilehash: 3b19f078b0d6dc3e02d951014056406fd1b099a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Güvenli LDAP (LDAPS) Azure AD etki alanı Hizmetleri yönetilen etki alanı için yapılandırma

## <a name="before-you-begin"></a>Başlamadan önce
Tamamlandı olun [görev 2 - güvenli LDAP sertifika verme bir. PFX dosyası](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Bu görevi tamamlamak için Azure portal deneyimi Önizleme veya Klasik Azure Portalı'nı kullanıp kullanmayacağınızı seçin.
> [!div class="op_single_selector"]
> * **Azure portal (Önizleme)**: [etkinleştir güvenli LDAP Azure Portalı'nı kullanarak](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Klasik Azure portalı**: [etkinleştir güvenli LDAP Klasik Azure Portalı'nı kullanarak](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview"></a>Görev 3 - güvenli LDAP (Önizleme) Azure portalını kullanarak yönetilen etki alanı için etkinleştirme
Güvenli LDAP etkinleştirmek için aşağıdaki yapılandırma adımlarını gerçekleştirin:

1. Gidin  **[Azure portal](https://portal.azure.com)**.

2. Arama 'etki alanı Hizmetleri'nde' **arama kaynakları** arama kutusu. Seçin **Azure AD etki alanı Hizmetleri** arama sonuç. **Azure AD etki alanı Hizmetleri** dikey penceresinde, yönetilen etki alanınız listelenir.

    ![Yönetilen etki alanı sağlanacak Bul](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Etki alanı hakkında daha fazla ayrıntı görmek için yönetilen etki alanının adını (örneğin, ' contoso100.com')'yi tıklatın.

    ![Etki alanı hizmetleri - sağlama durumu](./media/getting-started/domain-services-provisioning-state.png)

3. Tıklatın **güvenli LDAP** Gezinti Bölmesi.

    ![Etki Alanı Hizmetleri - güvenli LDAP dikey penceresi](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. Varsayılan olarak, yönetilen etki alanınız için güvenli LDAP erişim devre dışıdır. İki durumlu **güvenli LDAP** için **etkinleştirmek**.

    ![Güvenli LDAP etkinleştir](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. Varsayılan olarak, internet üzerinden yönetilen etki alanınız için güvenli LDAP erişim devre dışıdır. İki durumlu **Internet üzerinden güvenli LDAP erişim izni** için **etkinleştirmek**istenirse. 

6. Klasör simgesine aşağıdaki **. Güvenli LDAP Sertifika PFX dosyası**. Güvenli LDAP erişim yönetilen etki alanı için sertifikayla PFX dosyasının yolunu belirtin.

7. Belirtin **şifresini çözmek için parola. PFX dosyası**. Sertifika PFX dosyasına dışarı aktarılırken kullanılan aynı parolayı belirtin.

8. İşiniz bittiğinde tıklatın **kaydetmek** düğmesi.

9. Yönetilen etki alanı için yapılandırılan LDAP güvenli bildiren bir bildirim görürsünüz. Bu işlem tamamlanana kadar diğer etki alanı ayarlarını değiştiremezsiniz.

    ![Güvenli LDAP yönetilen etki alanı için yapılandırma](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> Yönetilen etki alanınız için güvenli LDAP etkinleştirmek için yaklaşık 10-15 dakika sürer. Sağlanan güvenli LDAP sertifika gereken ölçütleri eşleşmiyorsa, güvenli LDAP dizin için etkin değil ve bir hata görebilirsiniz. Örneğin, etki alanı adı hatalı olduğu, sertifikanın süresi dolmuş veya süresi yakında doluyor. Bu durumda, geçerli bir sertifikayla yeniden deneyin.
>
>

<br>

## <a name="task-4---configure-dns-to-access-the-managed-domain-from-the-internet"></a>Görev 4 - internet'ten yönetilen etki alanına erişmek için DNS yapılandırma
> [!NOTE]
> **İsteğe bağlı görev** -, düşünmüyorsanız LDAPS kullanarak internet yönetilen etki alanına erişmek için bu yapılandırma görevi atlayın.
>
>

Bu görev başlamadan önce özetlenen adımları tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Güvenli LDAP erişim internet üzerinden yönetilen etki alanınız için etkinleştirdikten sonra DNS istemci bilgisayarları Bu yönetilen etki alanı bulabilmesi için güncelleştirmeniz gerekir. Dış IP adresini gösterilir görev 3 sonunda **özellikleri** dikey penceresinde **dış IP adresi için LDAPS erişim**.

(Örneğin, ' ldaps.contoso100.com') yönetilen etki alanının DNS adı bu dış IP adresine işaret eden dış DNS sağlayıcınız yapılandırın. Bizim örneğimizde aşağıdaki DNS girişini oluşturmak üzere ihtiyacımız var:

    ldaps.contoso100.com  -> 52.165.38.113

İşte bu kadar - güvenli LDAP internet üzerinden kullanarak yönetilen etki alanına bağlanmak artık hazırsınız.

> [!WARNING]
> İstemci bilgisayarları LDAPS kullanarak yönetilen etki alanı başarıyla bağlanabilmesi için LDAPS sertifikayı veren güvenmelidir unutmayın. Genel olarak güvenilir bir sertifika yetkilisi kullanıyorsanız, istemci bilgisayarlar bu sertifikayı verenler güven bu yana bir şey yapmanız gerekmez. Kendinden imzalı bir sertifika kullanıyorsanız, otomatik olarak imzalanan sertifika ortak parçasını istemci bilgisayarındaki güvenilen sertifika deposuna yükleyin.
>
>


## <a name="task-5---lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a>Görev 5 - internet üzerinden yönetilen etki alanınız için kilitleme LDAPS erişim
> [!NOTE]
> **İsteğe bağlı görev** - internet üzerinden yönetilen etki alanına LDAPS erişim etkinleştirmediyseniz, bu yapılandırma görevi atlayın.
>
>

Bu görev başlamadan önce özetlenen adımları tamamladığınızdan emin olun [görev 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Yönetilen etki alanınız LDAPS erişim için internet üzerinden kullanıma sunan bir güvenlik tehdidi temsil eder. Yönetilen etki alanı güvenli LDAP için kullanılan bağlantı noktası Internet'ten erişilebilir olduğundan (diğer bir deyişle, bağlantı noktası 636). Bu nedenle, belirli bilinen IP adreslerini yönetilen etki alanına erişimi kısıtlamak seçebilirsiniz. Gelişmiş güvenlik için bir ağ güvenlik grubu (NSG) oluşturun ve Azure AD Etki Alanı Hizmetleri'ni etkinleştirdiğiniz alt ağı ile ilişkilendirin.

Aşağıdaki tabloda bir örnek, internet üzerinden güvenli LDAP erişim kilitlemek için yapılandırabileceğiniz NSG gösterilmektedir. NSG gelen LDAPS erişim TCP bağlantı noktası IP adreslerinin üzerinden 636 belirtilen kümesinden yalnızca izin veren kurallar kümesini içerir. Varsayılan 'DenyAll' kural, internet'ten diğer gelen trafik için geçerlidir. Belirtilen IP adreslerini Internet üzerinden LDAPS erişime izin verecek şekilde NSG kuralı DenyAll NSG kural daha yüksek önceliğe sahip.

![Örnek internet üzerinden LDAPS erişimi güvenli hale getirmek için NSG](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Daha fazla bilgi** - [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>İlgili içerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Azure AD Domain Services tarafından yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md)
* [Grup İlkesi, bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-group-policy.md)
* [Ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md)
* [Bir ağ güvenlik grubu oluşturun](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
