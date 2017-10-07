---
title: aaaRDG ve RADIUS kullanan Azure MFA sunucusu | Microsoft Docs
description: "Bu, Uzak Masaüstü (RD) ağ geçidi ve RADIUS kullanan Azure multi-Factor Authentication Sunucusu'nu dağıtmada yardımcı olacak hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>RADIUS kullanan Uzak Masaüstü Ağ Geçidi ve Azure Multi-Factor Authentication Sunucusu
Genellikle, Uzak Masaüstü (RD) ağ geçidi hello yerel ağ ilkesi Hizmetleri (NPS) tooauthenticate kullanıcılar kullanır. Bu makalede nasıl tooroute RADIUS çıkışı Uzak Masaüstü Ağ Geçidi hello istekleri açıklar (aracılığıyla yerel NPS hello) toohello çok faktörlü kimlik doğrulama sunucusu. Hello Azure MFA ve RD Ağ Geçidi birleşimi kullanıcılarınız kendi iş ortamlarında yerden erişebileceğiniz anlamına gelir güçlü kimlik doğrulaması gerçekleştirirken. 

Terminal hizmetleri için Windows kimlik doğrulaması Server 2012 R2 için desteklenmeyen olduğundan, RD Ağ geçidi ve RADIUS toointegrate MFA sunucusu ile kullanın. 

Hello Azure çok faktörlü kimlik doğrulama sunucusu hello RADIUS isteği hangi proxy'leri toohello NPS hello Uzak Masaüstü Ağ Geçidi sunucusu üzerinde geri ayrı bir sunucuya yükleyin. NPS hello kullanıcı adı ve parolayı doğruladıktan sonra yanıt toohello çok faktörlü kimlik doğrulama sunucusu döndürür. Ardından, hello MFA sunucusu hello ikinci faktörlü kimlik doğrulaması gerçekleştirir ve bir sonuç toohello ağ geçidi döndürür.

## <a name="prerequisites"></a>Ön koşullar

- Etki alanına katılmış bir Azure MFA Sunucusu. Zaten yüklüyse yoksa, hello adımları [hello Azure multi-Factor Authentication sunucusu ile çalışmaya başlama](multi-factor-authentication-get-started-server.md).
- Ağ İlkesi Hizmetleri’nde kimlik doğrulaması yapan bir Uzak Masaüstü Ağ Geçidi.

## <a name="configure-hello-remote-desktop-gateway"></a>Merhaba Uzak Masaüstü Ağ Geçidi yapılandırma
Merhaba RD Ağ Geçidi toosend RADIUS kimlik doğrulaması tooan Azure multi-Factor Authentication Sunucusu'nu yapılandırın. 

1. RD Ağ Geçidi Yöneticisi ' nde hello sunucu adına sağ tıklayın ve seçin **özellikleri**.
2. Toohello Git **RD CAP Deposu** sekmesinde ve seçin **NPS çalıştıran merkez sunucusu**. 
3. Bir veya daha fazla Azure multi-Factor Authentication sunucusu RADIUS sunucuları olarak hello adı ya da her sunucunun IP adresini girerek ekleyin. 
4. Her sunucu için paylaşılan gizlilik oluşturun.

## <a name="configure-nps"></a>NPS yapılandırma
Merhaba RD Ağ Geçidi NPS toosend hello RADIUS isteği tooAzure çok faktörlü kimlik doğrulaması kullanır. NPS tooconfigure, ilk tooprevent hello iki aşamalı doğrulamayı tamamlanmadan önce RD Ağ Geçidi zaman aşımına uğramadan hello hello zaman aşımı ayarlarını değiştirin. Ardından, MFA sunucunuzdan NPS tooreceive RADIUS kimlik doğrulamalarını güncelleştirin. Aşağıdaki yordam tooconfigure NPS hello kullan:

### <a name="modify-hello-timeout-policy"></a>Merhaba zaman aşımı ilkesini değiştirme

1. NPS'de, hello açmak **RADIUS istemcisi ve sunucusu** sol sütun ve select hello menüde **uzak RADIUS sunucu grupları**. 
2. Select hello **TH Ağ Geçidi sunucusu GRUBUNU**. 
3. Toohello Git **Yük Dengeleme** sekmesi. 
4. Her iki hello değiştirme **bırakılan isteği kabul edilmeden önce yanıt olmadan saniye sayısı** ve hello **sunucu olarak kullanılamaz olduğu belirlendiğinde isteklerinin arasındaki saniye sayısını** toobetween 30 ve 60 saniye sayısı. (Bu hello sunucu hala kimlik doğrulaması sırasında zaman aşımına fark ederseniz, tekrar buraya gelin ve hello saniye sayısını artırın.)
5. Toohello Git **kimlik doğrulama/hesap** sekmesinde ve hello RADIUS bağlantı noktalarının eşleşme hello bağlantı noktaları, çok faktörlü kimlik doğrulama sunucu dinliyor bu hello belirtilen denetleyin.

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a>NPS tooreceive kimlik doğrulamaları hello MFA sunucusu gelen hazırlama

1. Sağ **RADIUS istemcileri** RADIUS istemcileri ve sunucuları sol sütun ve select hello altında **yeni**.
2. Hello Azure multi-Factor Authentication sunucusu RADIUS istemcisi olarak ekleyin. Kolay bir ad seçin ve paylaşılan gizlilik belirtin.
3. Açık hello **ilkeleri** sol sütun ve select hello menüde **bağlantı isteği ilkeleri**. RD Ağ Geçidi yapılandırıldığında oluşturulan TS AĞ GEÇİDİ KİMLİK DOĞRULAMA İLKESİ adlı bir ilke görürsünüz. Bu ilke RADIUS isteklerini toohello çok faktörlü kimlik doğrulama sunucusu iletir.
4. **TS AĞ GEÇİDİ KİMLİK DOĞRULAMA İLKESİ**’ne sağ tıklayıp **İlkeyi Yinele**’yi seçin. 
5. Açık hello yeni ilke ve Git toohello **koşullar** sekmesi.
6. Merhaba istemci kolay adı hello Azure multi-Factor Authentication sunucusu RADIUS istemcisi için 2. adımda ayarlanan hello kolay adı ile eşleşen bir koşulu ekleyin. 
7. Toohello Git **ayarları** sekmesinde ve seçin **kimlik doğrulama**.
8. Merhaba kimlik doğrulama sağlayıcısı çok değiştirme**bu sunucuda istekler için kimlik doğrulaması**. Bu ilke, NPS Azure MFA sunucusu hello RADIUS isteği aldığında, hello kimlik doğrulamasını bir RADIUS isteği geri toohello bir döngü koşuluna neden olacak Azure multi-Factor Authentication Sunucusu'nu yerel olarak göndermek yerine oluşur sağlar. 
9. tooprevent Döngü koşulu hello yeni ilke hello özgün hello ilkesinde YUKARIDA sıralanır emin olun **bağlantı isteği ilkeleri** bölmesi.

## <a name="configure-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication’ı yapılandırma

Hello Azure multi-Factor Authentication sunucusu, RD Ağ geçidi ile NPS arasında bir RADIUS proxy olarak yapılandırılır.  Merhaba RD Ağ Geçidi sunucusundan ayrı bir etki alanına katılmış bir sunucuya yüklenmesi gerekir. Aşağıdaki yordam tooconfigure hello Azure çok faktörlü kimlik doğrulama sunucusu hello kullanın.

1. Hello Azure multi-Factor Authentication Sunucusu'nu açın ve hello RADIUS kimlik doğrulaması simgesini seçin. 
2. Merhaba denetleyin **RADIUS kimlik doğrulamasını etkinleştir** onay kutusu.
3. Merhaba istemciler sekmesinde hello bağlantı noktalarını eşleşen NPS'de yapılandırılanlarla emin olun sonra seçin **Ekle**.
4. Merhaba RD Ağ Geçidi sunucusu IP adresi, uygulama adı (isteğe bağlı) ve paylaşılan gizlilik ekleyin. Merhaba paylaşılan gizli gereksinimlerini toobe Merhaba, aynı, hem hello Azure multi-Factor Authentication sunucusu hem de RD Ağ geçidi.
3. Toohello Git **hedef** sekmesi ve select hello **RADIUS sunucularını** radyo düğmesi.
4. Seçin **Ekle** başlangıç IP adresi, paylaşılan gizliliği ve bağlantı noktaları hello NPS sunucusunun girin. Merkezi NPS kullanmadığınız sürece, hello RADIUS istemcisi ve RADIUS hedefi olan hello aynı. Merhaba paylaşılan gizliliği hello hello NPS sunucusunun RADIUS istemci bölümünde bir kurulumunda hello eşleşmesi gerekir.

![Radius Kimlik Doğrulaması](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>Sonraki adımlar

- Azure MFA ve [IIS web uygulamalarını](multi-factor-authentication-get-started-server-iis.md) tümleştirme

- Hello cevaplar [Azure çok faktörlü kimlik doğrulaması ile ilgili SSS](multi-factor-authentication-faq.md)
