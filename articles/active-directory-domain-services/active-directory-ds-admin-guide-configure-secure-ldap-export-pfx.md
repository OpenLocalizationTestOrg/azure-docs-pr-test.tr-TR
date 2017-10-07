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
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Güvenli LDAP (LDAPS) Azure AD etki alanı Hizmetleri yönetilen etki alanı için yapılandırma

## <a name="before-you-begin"></a>Başlamadan önce
Tamamlandı olun [görev 1 - güvenli LDAP için bir sertifika edinin](active-directory-ds-admin-guide-configure-secure-ldap.md).


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>Görev 2 - hello güvenli LDAP sertifika tooa dışarı aktarma. PFX dosyası
Bu görev başlamadan önce bir ortak sertifika yetkilisinden hello güvenli LDAP sertifikayı aldıktan veya otomatik olarak imzalanan bir sertifika oluşturduysanız emin olun.

Aşağıdaki adımları hello gerçekleştirmek, tooexport hello LDAPS sertifika tooa. PFX dosyası.

1. Tuşuna hello **Başlat** düğmesi ve türü **R**. Merhaba, **çalıştırmak** iletişim, türü **mmc** tıklatıp **Tamam**.

    ![Merhaba MMC konsolunu başlatın](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. Merhaba üzerinde **kullanıcı hesabı denetimi** İste'ye tıklayın **Evet** toolaunch MMC (Microsoft Yönetim Konsolu) yönetici olarak.
3. Merhaba gelen **dosya** menüsünde tıklatın **Ekle/Kaldır ek bileşenini...** .

    ![Ek bileşenini tooMMC konsoluna ekleyin](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. Merhaba, **Ekle veya Kaldır ek bileşenler** iletişim, select hello **sertifikaları** ek bileşenini hello tıklatıp **Ekle >** düğmesi.

    ![Sertifikalar ek bileşenini tooMMC konsoluna ekleyin](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. Merhaba, **Sertifikalar ek bileşenini** seçin **bilgisayar hesabı** tıklatıp **sonraki**.

    ![Sertifikalar ek bileşenini bilgisayar hesabı ekleme](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. Merhaba üzerinde **Bilgisayar Seç** sayfasında **yerel bilgisayar: (Merhaba bilgisayar bu konsolu çalışıyor)** tıklatıp **son**.

    ![Sertifikalar ek bileşenini - select bilgisayar ekleme](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. Merhaba, **Ekle veya Kaldır ek bileşenler** iletişim kutusunda, tıklatın **Tamam** tooadd hello Sertifikalar ek bileşenini tooMMC.

    ![Bitti Sertifikalar ek bileşenini tooMMC - Ekle](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. Merhaba MMC tooexpand penceresinde **konsol kökü**. Sertifikalar ek bileşenini hello yüklenen görmeniz gerekir. Tıklatın **sertifikalar (yerel bilgisayar)** tooexpand. Tooexpand hello tıklatın **kişisel** hello tarafından izlenen düğümü **sertifikaları** düğümü.

    ![Açık kişisel sertifikalar deposuna](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. Merhaba otomatik olarak imzalanan sertifika oluşturduğumuz görmeniz gerekir. Merhaba sertifika oluşturduğunuzda, bildirilen hello PowerShell windows hello tooensure hello parmak izi sertifikasındaki hello özelliklerini inceleyebilirsiniz.
10. Merhaba kendinden imzalı bir sertifika seçin ve **sağ tıklatın**. Merhaba sağ tıklatma menüsünden seçin **tüm görevler** seçip **dışarı aktar...** .

    ![Sertifika verme](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. Merhaba, **Sertifika Verme Sihirbazı**, tıklatın **sonraki**.

    ![Dışarı aktarma Sertifika Sihirbazı](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. Merhaba üzerinde **özel anahtarı dışarı** sayfasında, **Evet, hello özel anahtarı dışarı aktar**, tıklatıp **sonraki**.

    ![Sertifika özel anahtarı dışarı aktar](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > Merhaba sertifika birlikte hello özel anahtarın dışarı aktarmanız gerekir. Merhaba hello sertifikanın özel anahtarı içermiyor bir PFX sağlarsanız, yönetilen etki alanınız için güvenli LDAP etkinleştirme başarısız olur.
    >
    >
13. Merhaba üzerinde **dışarı aktarma dosyası biçimi** sayfasında, **kişisel bilgi alış verişi - PKCS #12 (. PFX)** hello dosya biçimi hello için sertifika dışarı gibi.

    ![Sertifika dosya biçimini Dışarı Aktar](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Yalnızca hello. PFX dosyasının biçimi desteklenmiyor. Merhaba sertifika toohello vermeyin. CER dosya biçimi.
    >
    >
14. Merhaba üzerinde **güvenlik** sayfası, select hello **parola** seçeneği ve parola tooprotect hello yazın. PFX dosyası. Merhaba sonraki görev gerekecek beri bu parolayı unutmayın. Tıklatın **sonraki** tooproceed.

    ![Sertifika dışarı aktarma için parola ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > Bu parolayı not edin. Bu yönetilen etki alanı için güvenli LDAP etkinleştirirken gereken [görev 3 - güvenli LDAP hello yönetilen etki alanı için etkinleştirme](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. Merhaba üzerinde **dosya tooExport** sayfasında, hello dosya adı ve olduğu gibi tooexport hello sertifika konumu belirtin.

    ![Sertifika dışa aktarma yolu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. Sayfasında, aşağıdaki Hello üzerinde tıklatın **son** tooexport hello tooa sertifika.pfx dosyası. Merhaba sertifika verildiğinde onay iletişim kutusu görmeniz gerekir.

    ![Bitti sertifikasını dışarı aktarma](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>Sonraki adım
[Görev 3 - güvenli LDAP hello yönetilen etki alanı için etkinleştirme](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
