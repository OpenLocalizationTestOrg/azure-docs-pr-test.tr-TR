---
title: "dağıtılan bir StorSimple cihazı aaaTroubleshoot | Microsoft Docs"
description: "Açıklar nasıl şu anda dağıtılmış ve çalışır durumda bir StorSimple cihazında oluşan toodiagnose ve düzeltme hataları."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: b48433055e05e3fb27575b88dca9f6b23c649ca2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-operational-storsimple-device"></a>İşletimsel bir StorSimple cihazı sorun giderme
## <a name="overview"></a>Genel Bakış
Bu makalede yapılandırma sorunlarını çözmek için yararlı sorun giderme kılavuzu verilmiştir StorSimple Cihazınızı dağıtılmış ve çalışır durumda sonra hatalarla karşılaşabilirsiniz. Sık karşılaşılan sorunları, olası nedenler ve önerilen adımları toohelp Microsoft Azure StorSimple çalıştırdığınızda karşılaşabileceğiniz sorunları gidermek açıklar. Bu bilgiler tooboth hello StorSimple şirket içi fiziksel cihazı ve hello StorSimple sanal cihazı geçerlidir.

Bu makalede, Microsoft Azure StorSimple işlemi sırasında karşılaşabileceğiniz hata kodları listesini bulabilirsiniz Hello sonunda yanı sıra adımları tooresolve hello hataları alabilir. 

## <a name="setup-wizard-process-for-operational-devices"></a>Kurulum Sihirbazı işlemi işletimsel cihazlar için
Merhaba Kurulum Sihirbazı'nı kullanın ([Invoke-HcsSetupWizard][1]) toocheck hello aygıt yapılandırması ve gerekirse düzeltme eylemlerini gerçekleştirin.

Önceden yapılandırılmış ve işletimsel aygıtta hello Kurulum Sihirbazı'nı çalıştırdığınızda, hello işlem akışı farklıdır. Girdileri aşağıdaki yalnızca hello değiştirebilirsiniz:

* IP adresi, alt ağ maskesi ve ağ geçidi
* Birincil DNS sunucusu
* Birincil NTP sunucusu
* İsteğe bağlı web proxy yapılandırması

Merhaba Kurulum Sihirbazı'nı hello operations ilgili toopassword toplama ve cihaz kaydı gerçekleştirmez.

## <a name="errors-that-occur-during-subsequent-runs-of-hello-setup-wizard"></a>Merhaba Kurulum Sihirbazı'nın sonraki çalışmaları sırasında oluşan hataları
Merhaba hataları ve önerilen eylemler tooresolve için bunları olası nedenleri, aşağıdaki tablonun hello işletimsel bir aygıtta hello Kurulum Sihirbazı'nı çalıştırdığınızda, karşılaşabileceğiniz hello hatalar açıklanır. 

| Hayır. | Hata iletisi veya koşul | Olası nedenler | Önerilen eylem |
|:--- |:--- |:--- |:--- |
| 1 |Hata 350032: Bu aygıt zaten devre dışı bırakıldı. |Devre dışı bir aygıtta hello Kurulum sihirbazını çalıştırırsanız, bu hatayı görürsünüz. |[Microsoft Support başvurun](storsimple-contact-microsoft-support.md) sonraki adımlar için. Devre dışı bırakılmış bir aygıt hizmetinde konumuna geçiremezsiniz. Merhaba aygıt yeniden etkinleştirilmeden önce bir Fabrika sıfırlaması gerekebilir. |
| 2 |Invoke-HcsSetupWizard: ERROR_INVALID_FUNCTION (HRESULT özel durumu: 0x80070001) |Merhaba DNS sunucusu güncelleştirmesi başarısız oluyor. DNS ayarları genel ayarları ve tüm etkin hello ağ arabirimleri üzerinde uygulanır. |Merhaba arabirimi etkinleştirmek ve hello DNS ayarlarını yeniden uygulayın. Bu ayarlar geneldir çünkü bu diğer etkin arabirimleri için hello ağ bozabilir. |
| 3 |Merhaba aygıtı toobe çevrimiçi hello StorSimple Yöneticisi hizmet Portalı'nda görünür ancak toocomplete hello minimum kurulum deneyin ve hello yapılandırma kaydettiğinizde hello işlemi başarısız olur. |Oluştu olsa bile bir gerçek proxy sunucusu yerinde ilk kurulum sırasında hello web proxy, yapılandırılmadı. |Kullanım hello [Test HcsmConnection cmdlet] [ 2] toolocate hello hata. [Microsoft Support başvurun](storsimple-contact-microsoft-support.md) oluşturulamıyor toocorrect hello sorun olması durumunda. |
| 4 |Invoke-HcsSetupWizard: Değer beklenen hello aralığında değil. |Hatalı alt ağ maskesi, bu hata üretir. Olası nedenler şunlardır: <ul><li> Merhaba alt ağ maskesi eksik veya boş olamaz.</li><li>Merhaba IPv6 öneki biçimi doğru değil.</li><li>Merhaba arabirimi bulut etkindir, ancak eksik veya yanlış hello geçididir.</li></ul>Veri 0-hello Kurulumu Sihirbazı aracılığıyla yapılandırdıysanız, bulut otomatik olarak etkin olduğunu unutmayın. |toodetermine hello sorun 0.0.0.0 veya 256.256.256.256 alt ağını ve hello çıkışına bakın. Doğru değerleri gerektiği şekilde hello alt ağ maskesi, ağ geçidi ve IPv6 öneki girin. |

## <a name="error-codes"></a>Hata kodları
Hataları sayısal sırada listelenir.

| Hata sayısı | Hata metni ya da açıklaması | Önerilen kullanıcı eylemi |
|:--- |:--- |:--- |
| 10502 |Depolama hesabınız erişirken hatayla karşılaşıldı. |Birkaç dakika bekleyin ve yeniden deneyin. Merhaba hata devam ederse, Microsoft Destek'e başvurun sonraki adımlar için lütfen. |
| 40017 |Merhaba yedekleme İlkesi'nde belirtilen bir birim hello aygıtında bulunamadı gibi hello yedekleme işlemi başarısız oldu. |Merhaba yedekleme işlemi yeniden deneyin, hello hata devam ederse, Microsoft Support başvurun. Sonraki adımlar için. |
| 40018 |Merhaba yedekleme İlkesi'nde belirtilen hello birimlerden hiçbiri hello aygıtında bulunamadı gibi hello yedekleme işlemi başarısız oldu. |Merhaba yedekleme işlemi yeniden deneyin, hello hata devam ederse, Microsoft Support başvurun. Sonraki adımlar için. |
| 390061 |Merhaba sistem meşgul veya kullanılamaz durumda. |Birkaç dakika bekleyin ve yeniden deneyin. Merhaba hata devam ederse, Microsoft Destek'e başvurun sonraki adımlar için lütfen. |
| 390143 |Hata kodu 390143 ile bir hata oluştu. (Bilinmeyen hata.) |Merhaba hata devam ederse, Microsoft Support sonraki adımlar için temasa geçin. |

## <a name="next-steps"></a>Sonraki adımlar
Yüklenemiyor tooresolve hello sorun olup olmadığını [Microsoft Support başvurun](storsimple-contact-microsoft-support.md) Yardım için. 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx
