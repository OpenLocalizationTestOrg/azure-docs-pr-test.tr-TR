---
title: "Yeniden çalıştırarak hello Azure AD Connect Yükleme Sihirbazı'nı | Microsoft Docs"
description: "Merhaba Yükleme Sihirbazı'nı hello ikinci çalıştırdığınızda nasıl çalıştığını açıklar."
keywords: "Hello Azure AD Connect Yükleme Sihirbazı, ikinci çalıştırdığınızda bakım ayarlarını hello yapılandırmanıza olanak sağlar"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Azure AD Connect eşitleme: ikinci kez hello yükleme sihirbazını çalıştırma
Merhaba hello Azure AD Connect Yükleme Sihirbazı, çalıştırdığınız ilk kez onu, nasıl anlatan tooconfigure yüklemenizi. Merhaba Yükleme Sihirbazı'nı yeniden çalıştırın, Bakım seçenekleri sunar.

Merhaba Yükleme Sihirbazı'nı adlı hello Başlat menüsünde bulabilirsiniz **Azure AD Connect**.

![Başlat menüsü](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

Merhaba Yükleme Sihirbazı'nı başlattığınızda, bu seçenekleri içeren bir sayfa görürsünüz:

![Ek görevler listesi sayfası](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

Azure AD Connect ile ADFS yüklediyseniz daha da fazla seçeneğiniz vardır. Merhaba sahip ADFS belgelenmiştir için ek seçenekler [ADFS Yönetim](active-directory-aadconnect-federation-management.md#manage-ad-fs).

Merhaba görevlerinden birini seçin ve tıklatın **sonraki** toocontinue.

> [!IMPORTANT]
> Merhaba Yükleme Sihirbazı'nı açın sahip olsa da, hello eşitleme Altyapısı'ndaki tüm işlemleri askıya alınır. Yapılandırma değişiklikleri tamamladıktan hemen sonra hello yükleme sihirbazını kapatın emin olun.
>
>

## <a name="view-current-configuration"></a>Geçerli yapılandırmayı görüntüle
Bu seçenek şu anda yapılandırılmış seçeneklerinizi hızlı bir görünümünü sağlar.

![Tüm seçenekler ve durumlarına Listesi Sayfası](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

Tıklatın **önceki** toogo geri. Seçerseniz **çıkış**, hello Yükleme Sihirbazı'nı kapatın.

## <a name="customize-synchronization-options"></a>Eşitleme seçeneklerini özelleştirme
Bu seçenek kullanılan toomake değişiklikleri toohello eşitleme yapılandırmadır. Bir alt kümesini hello özel yapılandırma yükleme yolu seçeneklerinden bakın. Hızlı yükleme başlangıçta kullanılan olsa bile, bu seçenek görürsünüz.

* [Daha fazla dizinler eklemek](active-directory-aadconnect-get-started-custom.md#connect-your-directories). Bir dizin kaldırmak için bkz: [bir bağlayıcıyı silmek](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).
* [Değişiklik etki alanı ve OU filtreleme](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).
* Grup filtresini kaldırın.
* [İsteğe bağlı özellikler değiştirmek](active-directory-aadconnect-get-started-custom.md#optional-features).

Merhaba diğer seçenekler hello ilk yüklemesinden değiştirilemez ve kullanılabilir değil. Bu seçenekler şunlardır:

* Merhaba özniteliği toouse userPrincipalName ve sourceAnchor için değiştirin.
* Farklı ormandaki nesneleri için yöntem birleştirme hello değiştirin.
* Grup tabanlı filtreleme etkinleştirin.

## <a name="refresh-directory-schema"></a>Dizin şemasını Yenile
Merhaba şema şirket içi birini değiştirdiyseniz, bu seçenek kullanılır AD DS orman. Örneğin, Exchange yüklenmemiş olabilir veya tooa Windows Server 2012 şema aygıt nesneler ile yükseltme. Bu durumda, tooinstruct Azure AD Connect tooread hello şema AD DS'den yeniden gerekir ve önbelleğini güncelleştirin. Bu eylem ayrıca hello eşitleme kuralları yeniden oluşturur. Örnek olarak hello Exchange şema eklerseniz, Exchange için hello eşitleme kuralları toohello yapılandırma eklenir.

Bu seçeneği belirlediğinizde, yapılandırmanızda tüm hello dizinleri listelenir. Hello varsayılan ayar tutun ve tüm ormanlarda yenileyin veya bunlardan bazıları seçimini kaldırın.

![Merhaba ortamında tüm dizinlerin listesini sayfası](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>Hazırlama modunu yapılandırma
Bu seçenek tooenable sağlar ve hello sunucuda hazırlama modunu devre dışı bırakın. Hazırlama modu ve nasıl kullanıldığı hakkında daha fazla bilgi bulunabilir [Operations](active-directory-aadconnectsync-operations.md#staging-mode).

Merhaba seçeneği hazırlama şu anda etkin veya devre dışı olmadığını gösterir:  
![Ayrıca hazırlama modunu hello geçerli durumunu gösteren seçeneği](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange Merhaba durumu, bu seçeneği ve seçimi kaldır veya seçin hello onay kutusunu seçin.  
![Ayrıca hazırlama modunu hello geçerli durumunu gösteren seçeneği](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>Kullanıcı oturum açma değiştirme
Bu seçenek parola eşitleme toofederation veya hello diğer yönden toochange sağlar. Çok değiştiremezsiniz**yapılandırmayın**.

Bu seçenek hakkında daha fazla bilgi için bkz: [kullanıcı oturum açma](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).

## <a name="next-steps"></a>Sonraki adımlar
* Azure AD Connect eşitleme tarafından kullanılan hello yapılandırma modeli hakkında daha fazla bilgi [anlama bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
