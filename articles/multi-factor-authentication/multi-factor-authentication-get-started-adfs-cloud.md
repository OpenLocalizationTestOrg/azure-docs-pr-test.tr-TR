---
title: "Azure MFA ve AD FS ile aaaSecure bulut kaynaklarına | Microsoft Docs"
description: "Bu Azure MFA ve AD FS hello bulutta tooget nasıl kullanmaya açıklayan hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Azure Multi-Factor Authentication ve AD FS ile bulut kaynaklarını güvenli hale getirme
Kuruluşunuz Azure Active Directory ile birleştirildiyse Azure çok faktörlü kimlik doğrulaması veya Azure AD tarafından erişilen Active Directory Federasyon Hizmetleri (AD FS) toosecure kaynakları kullanın. Aşağıdaki yordamlar toosecure Azure Active Directory kaynaklarını Azure multi-Factor Authentication veya Active Directory Federasyon Hizmetleri ile Merhaba kullanın.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>AD FS kullanarak Azure AD kaynaklarını güvenli hale getirme
toosecure, bulut kaynak kümesi bir talep kuralı böylece bir kullanıcı iki aşamalı doğrulamayı başarıyla gerçekleştirdiğinde, Active Directory Federasyon Hizmetleri hello multipleauthn talebi gösterir. Bu talep AD tooAzure üzerinde geçirilir. Bu yordam toowalk hello adımları izleyin:


1. AD FS Yönetimi'ni açın.
2. Merhaba solda seçin **bağlı olan taraf güvenleri**.
3. **Microsoft Office 365 Kimlik Platformu**'na sağ tıklayın ve **Talep Kurallarını Düzenle**'yi seçin.

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. Açık dönüştürme talep Kuralı Ekleme Sihirbazı Merhaba, seçin **geçir veya Filtrele bir gelen talep** açılan hello ve'ı tıklatın **sonraki**.

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Kuralınıza bir ad verin. 
7. Seçin **kimlik doğrulama yöntemleri başvuruları** hello gelen talep türü.
8. **Tüm talep değerlerini geçir**’i seçin.
    ![Dönüşüm Talep Kuralı Ekleme Sihirbazı](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. **Son**'a tıklayın. Merhaba AD FS Yönetim Konsolu'nu kapatın.

## <a name="trusted-ips-for-federated-users"></a>Federasyon kullanıcıları için Güvenilen IP'ler
Güvenilen IP'ler yöneticilerin tooby geçişi iki aşamalı doğrulamayı belirli IP adresleri için ya da kendi intranetlerinden kaynaklanan taleplere sahip Federasyon kullanıcıları için izin verir. Merhaba aşağıdaki nasıl tooconfigure Azure multi-Factor Authentication güvenilen bölümlerde IP'leri Federasyon kullanıcıları ve bir Federasyon kullanıcıları intranet içinde bir isteğin kaynaklandığı zaman atlama iki aşamalı doğrulama. Bu, AD FS toouse bir geçiş veya filtre gelen talep şablonu hello Kurumsal ağın içinden talep türü ile yapılandırarak sağlanır.

Bu örnekte Güvenilen Taraf Güvenlerimiz için Office 365 kullanılmıştır.

### <a name="configure-hello-ad-fs-claims-rules"></a>Merhaba AD FS talep kurallarını yapılandırma
toodo ihtiyacımız hello ilk tooconfigure hello AD FS talep şeydir. Biri hello Kurumsal ağın içinden talep türü ve ek bir oturum açık tutmak için iki talep kurallarını oluşturun.

1. AD FS Yönetimi'ni açın.
2. Merhaba solda seçin **bağlı olan taraf güvenleri**.
3. **Microsoft Office 365 Kimlik Platformu**’na sağ tıklayın ve **Talep Kurallarını Düzenle…** seçeneğini belirleyin.
   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.
   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. Açık dönüştürme talep Kuralı Ekleme Sihirbazı Merhaba, seçin **geçir veya Filtrele bir gelen talep** açılan hello ve'ı tıklatın **sonraki**.
   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. Merhaba kutusunu sonraki tooClaim kural adı kuralınıza bir ad verin. Örneğin: InsideCorpNet.
7. Sonraki tooIncoming hello açılır, gelen talep türü, seçin **Kurumsal ağın içinden**.
   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. **Son**'a tıklayın.
9. Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.
10. Açık dönüştürme talep Kuralı Ekleme Sihirbazı Merhaba, seçin **talepleri özel kural kullanarak Gönder** açılan hello ve'ı tıklatın **sonraki**.
11. Talep kuralı adı altındaki hello kutusuna: girin *tutmak kullanıcılar imzalı içinde*.
12. Merhaba özel kural kutusuna şunu girin:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. **Finish (Son)** düğmesine tıklayın.
14. **Uygula**'ya tıklayın.
15. **Tamam**’a tıklayın.
16. AD FS Yönetimi'ni kapatın.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Azure Multi-Factor Authentication Güvenilen IP’leri Federasyon Kullanıcıları ile Yapılandırma
Merhaba talepler, biz güvenilen IP'leri yapılandırabilirsiniz.

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Hello solda tıklatın **Active Directory**.
3. Dizini altında hello dizini tooset güvenilen IP'leri ayarlamak istediğiniz yeri seçin.
4. Hello seçtiğiniz dizin, tıklatın **yapılandırma**.
5. Merhaba çok faktörlü kimlik doğrulaması bölümünde tıklayın **hizmet ayarlarını Yönet**.
6. Merhaba hizmet ayarları sayfasında, güvenilen IP'ler altında seçin **Atla çok / multi-Factor-authentication istekleri için Federasyon kullanıcıları intranetimde bulunan**.  

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. **Kaydet**’e tıklayın.
8. Merhaba güncelleştirmeler uygulandıktan sonra tıklayın **kapatmak**.

Bu kadar! Bir talep dış hello Kurumsal intranet bağlantısı kaynaklandığı bu noktada, birleştirilmiş Office 365 kullanıcıları yalnızca toouse MFA olması gerekir.
