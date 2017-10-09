---
title: "aaaTroubleshoot Azure kaydolma sorunlarını | Microsoft Docs"
description: "Nasıl tootroubleshoot bazı ortak Azure oturum sorunları açıklar."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Azure için kaydolma sorunlarını giderme
Azure için kaydolamazsınız, bu makale tootroubleshoot ortak sorunları hello ipuçları kullanın. Kredi kartınız sırasında ile ilgili bir sorun varsa, kaydolma, bkz: [Azure kaydolma ATM kartı veya kredi kartı reddedildi](billing-credit-card-fails-during-azure-sign-up.md). Bir Azure hesabı varsa, ancak oturum açamıyorum yoksa bkz [toomanage içinde Azure Aboneliğim imzalayamazsınız](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>İlerleme çubuğu "Kartı tarafından kimlik doğrulaması" bölümünde askıda kalır

Kart tarafından toocomplete hello kimlik doğrulama, üçüncü taraf tanımlama bilgileri için tarayıcınızın izin verilmelidir.

![Merhaba kayıt sırasında asılı kartı bölüme göre kimlik doğrulama ekran görüntüsü](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Aşağıdaki adımları tooupdate hello tarayıcınızın tanımlama bilgisi ayarları kullanın.

1. Chrome kullanıyorsanız, çok Git**ayarları** > **Göster Gelişmiş ayarları** > **gizlilik** > **içeriği ayarları**. İşaretini **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri**.
2. Edge kullanıyorsanız, çok Git**ayarları** > **görünüm Gelişmiş ayarları** > **tanımlama bilgilerini**. Seçin **tanımlama bilgilerini engelleme**.
3. Hello Azure kaydolma sayfayı yenileyin ve hello sorunun giderilip giderilmediğini denetle.
4. Merhaba yenileme hello sorunu çözmek alamadık, çıkın ve tarayıcınızı yeniden başlatın ardından yeniden deneyin.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Kredi kartı form fatura adresimi desteklemiyor
Fatura adresini hello seçili hello ülkede toobe gereken **ilgili** bölümü. Merhaba doğru ülke seçtiğinizden emin olun.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Hiçbir metin iletileri veya kaydolma Hesap doğrulama sırasında çağrıları
Genellikle çok daha hızlı olsa da, bu doğrulama kodu toobe teslim toofour dakika sürebilir. doğrulama için girdiğiniz hello telefon numarası hello hesabı için kişi bir sayı olarak saklanmaz.

Bazı ipuçları şunlardır:
* Bir VoIP telefon numarası için hello telefon doğrulama işlemi kullanılamaz.
* Çift onay hello telefon numarası dahil hello açılır menüde seçilen hello ülke kodu girin.
* Telefonunuza kısa mesaj (SMS) almazsa hello deneyin **beni** seçeneği.
* Telefonunuz çağrıları veya SMS iletileri dayalı ABD numarasından alabileceğinizden emin olun.

Merhaba metin iletisi ya da telefon araması aldığınızda, hello metin kutusuna aldığınız kodu girin.

## <a name="credit-card-declined-or-not-accepted"></a>Kredi kartı reddedildi veya kabul edilmedi
Sanal veya ön ödemeli kredi veya ATM kartı Azure abonelikleri için ödeme olarak kabul değil. başka ne reddetti, kart toobe neden olabilir toosee bkz [Azure kaydolma ATM kartı veya kredi kartı reddedildi](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>"Ücretsiz deneme sürümü kullanılabilir değil"
Bir Azure aboneliği hello geçmiş kullandınız mı? Hello Azure kullanım koşulları sözleşmesini yeni tooAzure olan bir kullanıcı için ücretsiz deneme etkinleştirme sınırlar. Başka türde bir Azure aboneliğiniz varsa, ücretsiz deneme etkinleştirilemiyor. Olmayı göz önünde bulundurun bir [Kullandıkça Öde aboneliğine](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>Ücretsiz deneme hesabımdaki ı bir ücret gördüğünüz
Küçük bir görebilirsiniz doğrulama 3 too5 gün içinde kaldırıldı, oturumu sonra kredi kartı hesabınızdaki basılı tutun. Maliyetleri yönetme hakkında kaygılı varsa, daha fazla bilgi edinin [beklenmeyen maliyetleri önleme](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>MSDN, BizSpark, BizSparkPlus veya MPN gibi Azure avantajı planı etkinleştirilemiyor
Merhaba doğru oturum açma kullandığınızdan emin olun kimlik bilgileri. Ardından hello avantajı programı toomake uygun emin denetleyin. 

* MSDN
  * Uygunluk durumunuzu doğrulayın, [MSDN hesap sayfası](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Durumunuzu doğrulayamıyorsanız hello başvurun [MSDN Abonelikleri müşteri hizmetleri merkezleri](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * İçinde toohello oturum [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) ve BizSpark ve BizSpark artı için uygunluk durumunuzu doğrulayın.
  * Durumunuzu doğrulayamıyorsanız yapabilecekleriniz [hello BizSpark forumlarına Yardım](http://aka.ms/bzforums).
* MPN
  * İçinde toohello oturum [MPN portal](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) ve uygunluk durumunuzu doğrulayın. Merhaba uygun varsa [bulut platformu yetkinlikleri](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), ek faydalar uygun olabilir.
  * Durumunuzu doğrulayamıyorsanız başvurun [MPN Destek](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Yeni açık olarak Azure Abonelik etkinleştirilemiyor
toocreate bir açık olarak Azure abonelik, en az bir açık olarak Azure belirteci ilişkili tooit ile geçerli bir çevrimiçi hizmet etkinleştirme (OSA) anahtarı olması gerekir. Kişi Microsoft Partners birini OSA anahtar yoksa, listelenen [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.
