---
title: "aaaLDAP kimlik doğrulaması ve Azure MFA sunucusu | Microsoft Docs"
description: "Bu, LDAP kimlik doğrulaması ve Azure multi-Factor Authentication Sunucusu'nu dağıtmada yardımcı olacak hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>LDAP kimlik doğrulaması ve Azure multi-Factor Authentication sunucusu
Varsayılan olarak, Azure multi-Factor Authentication sunucusu hello yapılandırılmış tooimport ya da Active Directory'den kullanıcıları eşitlemeye. Ancak, ADAM dizini veya belirli Active Directory etki alanı denetleyicisi gibi yapılandırılmış toobind toodifferent LDAP dizinleri olabilir. Ne zaman bağlı tooa directory LDAP aracılığıyla hello Azure multi-Factor Authentication sunucusu LDAP proxy tooperform doğrulamaları davranamaz. Merhaba kullanmak için LDAP bağlama'nın RADIUS hedefi olarak hello Azure MFA Kullanıcı Portalı'nda birincil kimlik doğrulaması ya da IIS kimlik doğrulaması kullanıcılarla ön kimlik doğrulaması için de sağlar.

Azure multi-Factor Authentication LDAP proxy'si olarak toouse hello Azure çok faktörlü kimlik doğrulama sunucusu arasında hello LDAP istemcisi (örneğin, VPN Gereci, uygulaması) ve hello LDAP dizin sunucusuna ekleyin. Hello Azure multi-Factor Authentication sunucusu, hem hello istemci sunucuları hem de hello LDAP dizini ile yapılandırılmış toocommunicate olması gerekir. Bu yapılandırmada, hello Azure multi-Factor Authentication sunucusu istemci sunucuları ve uygulamaları gelen LDAP isteklerini kabul eder ve bunları toohello hedef LDAP dizin sunucusu toovalidate hello birincil kimlik bilgileri iletir. Merhaba LDAP dizini hello birincil kimlik bilgilerini doğrular, Azure multi-Factor Authentication ikinci bir kimlik doğrulaması gerçekleştirir ve bir yanıtı geri toohello LDAP istemcisi gönderir. yalnızca hello LDAP sunucu kimlik doğrulaması ve hello ikinci adım doğrulama başarılı olursa hello tüm kimlik doğrulama başarılı olur.

## <a name="configure-ldap-authentication"></a>LDAP kimlik doğrulamasını yapılandırma
tooconfigure LDAP kimlik doğrulaması, Windows Server yükleme hello Azure çok faktörlü kimlik doğrulama sunucusu. Merhaba aşağıdaki yordamı kullanın:

### <a name="add-an-ldap-client"></a>LDAP istemcisi ekleme

1. Hello Azure multi-Factor Authentication sunucusu, hello hello soldaki menüde LDAP kimlik doğrulaması simgesine seçin.
2. Merhaba denetleyin **LDAP kimlik doğrulamasını etkinleştir** onay kutusu.

   ![LDAP Kimlik Doğrulaması](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. Hello Azure multi-Factor Authentication LDAP hizmetinin LDAP isteklerini toonon standart bağlantı noktaları toolisten bağlanması gerekliyse hello istemciler sekmesinde hello TCP bağlantı noktasını ve SSL bağlantı noktasını değiştirin.
4. Merhaba istemci toohello Azure çok faktörlü kimlik doğrulama sunucusu gelen LDAPS toouse planlıyorsanız, hello üzerinde bir SSL sertifikası yüklenmelidir MFA sunucusu aynı sunucuya. Tıklatın **Gözat** sonraki toohello SSL sertifika kutusunu ve hello güvenli bağlantı için sertifika toouse seçin.
5. **Ekle**'ye tıklayın.
6. Merhaba LDAP istemcisi Ekle iletişim kutusunda hello gereç, sunucu ya da toohello sunucu ve bir uygulama adı (isteğe bağlı) kimliğini doğrulayan uygulama hello IP adresini girin. Merhaba uygulama adı Azure multi-Factor Authentication raporlarında görünür ve SMS veya mobil uygulama kimlik doğrulama iletilerinde görüntülenebilir.
7. Merhaba denetleyin **Azure multi-Factor Authentication iste kullanıcı eşleşme** tüm kullanıcılar Sunucu'ya aktarılmışsa ya da hello sunucu ve konu tootwo adım doğrulama aktarılır, kutu. Çok sayıda kullanıcı sunucu hello henüz içeri aktarılmadı ve/veya iki aşamalı doğrulamayı muaf tutulacaksa hello kutunun işaretini kaldırın. Merhaba MFA sunucusu Yardım dosyasına ek bilgi için bu özelliği bakın.

Bu adımları tooadd ek LDAP istemcileri yineleyin.

### <a name="configure-hello-ldap-directory-connection"></a>Merhaba LDAP dizini bağlantısını yapılandırmak

Hello Azure çok faktörlü kimlik doğrulaması yapılandırılan tooreceive LDAP kimlik doğrulamaları olduğunda, bu kimlik doğrulamaları toohello LDAP dizini proxy gerekir. Merhaba hedef sekmesi yalnızca tek bir görüntüler bu nedenle, LDAP hedefi seçeneği toouse gri.

1. tooconfigure hello LDAP dizini bağlantısını tıklatın hello **dizin tümleştirme** simgesi.
2. Merhaba Ayarlar sekmesinde hello seçin **belirli LDAP yapılandırması kullan** radyo düğmesi.
3. **Düzenle…** seçeneğini belirleyin.
4. Merhaba LDAP yapılandırmasını Düzenle iletişim kutusunda hello gerekli bilgileri tooconnect toohello LDAP dizini ile Merhaba alanları doldurun. Merhaba alanların açıklamaları hello Azure multi-Factor Authentication sunucusu Yardım dosyasına dahil edilir.

    ![Dizin Tümleştirme](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Merhaba tıklayarak hello LDAP bağlantısı testi **Test** düğmesi.
6. Merhaba LDAP bağlantısı testi başarılı olursa hello tıklatın **Tamam** düğmesi.
7. Merhaba tıklatın **filtreleri** sekmesini hello sunucu olan önceden yapılandırılmış tooload kapsayıcıları, güvenlik grupları ve Active Directory'den kullanıcıları. Tooa farklı LDAP dizinine bağlanıyorsanız, büyük olasılıkla görüntülenen tooedit hello filtreleri gerekir. Merhaba tıklatın **yardımcı** filtreleri hakkında daha fazla bilgi için bağlantı.
8. Merhaba tıklatın **öznitelikleri** sekmesini hello sunucu olduğu Active Directory'den önceden yapılandırılmış toomap öznitelikleri.
9. Tooa farklı LDAP dizini ya da toochange hello önceden yapılandırılmış öznitelik eşlemelerini bağlama tıklatmak **Düzenle...**
10. Merhaba öznitelikleri Düzenle iletişim kutusunda, dizininizin hello LDAP öznitelik eşlemelerini değiştirin. Öznitelik adları yazılabilir veya hello tıklayarak seçili **...** Düğme sonraki tooeach alanını. Merhaba tıklatın **yardımcı** öznitelikleri hakkında daha fazla bilgi için bağlantı.
11. Merhaba tıklatın **Tamam** düğmesi.
12. Merhaba tıklatın **şirket ayarları** simgesi ve select hello **kullanıcı adı çözümlemesi** sekmesi.
13. Etki alanına katılmış bir sunucudan tooActive dizinine bağlanıyorsanız hello bırakın **kullanım Windows Güvenlik tanımlayıcılarını (SID'ler) kullanıcı adlarını eşleştirmek için** seçili radyo düğmesi. Aksi takdirde, select hello **kullanıcı adlarını eşleştirmek için LDAP benzersiz tanımlayıcı özniteliği kullanın** radyo düğmesi. 

Ne zaman hello **kullanıcı adlarını eşleştirmek için LDAP benzersiz tanımlayıcı özniteliği kullanın** radyo düğmesi seçildiğinde, hello Azure multi-Factor Authentication sunucusu kullanıcı adı her tooa benzersiz tanımlayıcı hello LDAP dizinindeki tooresolve çalışır. Bir LDAP araması gerçekleştirilir kullanıcıadı hello üzerinde tanımlı hello dizin tümleştirme -> öznitelikler sekmesinde. Bir kullanıcı kimliği doğruladığında hello kullanıcıadı hello LDAP dizinindeki benzersiz tanımlayıcıya çözümlenmiş toohello'dır. Merhaba benzersiz tanımlayıcı hello Azure multi-Factor Authentication veri dosyasındaki eşleşen hello kullanıcı için kullanılır. Bu, büyük küçük harf duyarsız karşılaştırmalarına ve uzun kısa kullanıcı adı biçimlerine sağlar.

Bu adımları tamamladıktan sonra olanlar için proxy kimlik doğrulaması için toohello LDAP dizini istekleri gibi hello MFA sunucunun dinlediği hello gelen LDAP erişimi istekleri için yapılandırılan hello noktalarındaki istemciler ve davranır yapılandırılmış.

## <a name="configure-ldap-client"></a>LDAP istemcisi yapılandırma
tooconfigure hello LDAP istemcisi hello yönergeleri kullanın:

* Dizinindeymiş gibi LDAP dizininize gereç, sunucu veya LDAP toohello Azure çok faktörlü kimlik doğrulama sunucusu üzerinden uygulama tooauthenticate yapılandırın. Kullanım hello aynı ayarları tooconnect normalde kullanırsınız doğrudan tooyour LDAP dizini, hello sunucu adı veya, hello Azure çok faktörlü kimlik doğrulama sunucusu olacak IP adresini dışında.
* Zaman toovalidate hello kullanıcının kimlik bilgileriyle hello LDAP dizini olmasını sağlamak hello LDAP zaman aşımı too30-60 saniye yapılandırmak, hello ikinci adım doğrulamayı gerçekleştirmek, bunların yanıtını alma ve toohello LDAP erişim isteğine yanıt.
* LDAPS kullanıyorsanız hello gereç ya da hello LDAP sorgularını yapan sunucu hello Azure çok faktörlü kimlik doğrulama sunucusu üzerinde yüklü hello SSL sertifikasına güvenmesi gerekir.

