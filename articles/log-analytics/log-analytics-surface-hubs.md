---
title: "Surface Hubs Azure günlük analizi ile aaaMonitor | Microsoft Docs"
description: "Merhaba Surface Hub çözüm tootrack hello durumunu, Surface hub'larınız kullanın ve nasıl kullanıldıkları anlayın."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>Surface hub'ları ile günlük analizi tootrack durumlarını izleyin.

![Yüzey Hub simgesi](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

Bu makalede, günlük analizi toomonitor Microsoft Surface Hub cihazları hello Microsoft Operations Management Suite (OMS) ile Merhaba Surface Hub çözümü nasıl kullanabileceğiniz açıklanır. Oturum yanı sıra bunların nasıl kullanıldığını anlamak, Surface hub'larınız hello sağlığını izlemek Analytics yardımcı olur.

Her Surface Hub Microsoft izleme aracısı yüklü hello sahiptir. Kendi aracılığıyla hello Aracısı, Surface Hub tooOMS veri gönderebilir. Günlük dosyaları, Surface hub'ları ve misiniz okuma sonra toohello OMS hizmetine gönderilir. Sorunları çevrimdışı olan sunucuları hello gibi takvim değil eşitleniyor veya Skype içine oluşturulamıyor toolog hello cihaz hesabı ise, OMS içinde hello Surface Hub panosunda gösterilir. Merhaba panosunda Hello verileri kullanarak, çalışmıyor veya başka sorunlara sahip olduğunu ve potansiyel olarak algılanan hello sorunlarını giderir uygulamak aygıtlar tanımlayabilirsiniz.

## <a name="installing-and-configuring-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın. Sipariş toomanage, Surface hub'larından hello Microsoft Operations Management Suite (OMS) aşağıdaki hello gerekir:

* Geçerli bir abonelik çok[OMS](http://www.microsoft.com/oms).
* Bir [OMS abonelik](https://azure.microsoft.com/pricing/details/log-analytics/) hello numarası destekleyecek düzeyi aygıtların toomonitor istiyor. OMS fiyatlandırma kaç aygıtlar kaydedilir ve ne kadar veri bağlı olarak bu işlemlerin değişir. Tootake bu dikkate, Surface Hub dağıtımı planlarken isteyeceksiniz.

Ardından, bir OMS abonelik tooyour mevcut Microsoft Azure aboneliği ekleme ya da hello OMS Portalı aracılığıyla doğrudan yeni bir çalışma alanı oluşturun. Her iki yöntemi kullanarak altındadır için ayrıntılı yönergeler [günlük Analytics ile çalışmaya başlama](log-analytics-get-started.md). Merhaba OMS abonelik ayarlandıktan sonra Surface Hub cihazları iki yolu tooenroll vardır:

* Otomatik olarak Intune aracılığıyla
* El ile **ayarları** , Surface Hub Cihazınızda.

## <a name="set-up-monitoring"></a>İlkenin trafiği çevrimdışı durumdaki barındırılan hizmetlere
Merhaba durumu ve etkinliği, Surface Hub içinde OMS günlük analizi kullanarak izleyebilirsiniz. Merhaba OMS Surface Hub Intune kullanarak veya kullanarak yerel olarak kaydedebilir **ayarları** hello Surface Hub üzerinde.

## <a name="connect-surface-hubs-toooms-through-intune"></a>Surface Hubs tooOMS Intune aracılığıyla bağlanma
Çalışma alanı kimliği ve çalışma alanı anahtarınız, Surface hub'larınız yönetecek hello OMS çalışma alanı için hello. Bu hello OMS Portalı'ndan elde edebilirsiniz.

Intune toocentrally sağlayan bir Microsoft ürünü uygulanan tooone veya daha fazla aygıtlarınızı hello OMS yapılandırma ayarlarını yönetmek olan. Bu adımları tooconfigure cihazlarınızı Intune aracılığıyla izleyin:

1. TooIntune oturum açın.
2. Çok gidin**ayarları** > **bağlı kaynakları**.
3. Oluşturabilir veya hello Surface Hub şablona dayalı bir ilke düzenleyebilirsiniz.
4. Hello İlkesi toohello OMS (Azure operasyonel Öngörüler) bölümüne gidin ve hello eklemek *çalışma alanı kimliği* ve *çalışma alanı anahtarı* toohello ilkesi.
5. Hello İlkesi kaydedin.
6. Hello İlkesi hello uygun aygıtları grubuyla ilişkilendirin.

   ![Intune İlkesi](./media/log-analytics-surface-hubs/intune.png)

Intune hello OMS ayarları hello hedef grubu, OMS çalışma alanınızda kaydetme hello aygıtlarla sonra eşitlenir.

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>Surface Hubs tooOMS Hello ayarları uygulamasını kullanarak bağlan
Çalışma alanı kimliği ve çalışma alanı anahtarınız, Surface hub'larınız yönetecek hello OMS çalışma alanı için hello. Bu hello OMS Portalı'ndan elde edebilirsiniz.

Ortamınızı Intune toomanage kullanmıyorsanız, cihazları el ile kaydedebilirsiniz **ayarları** her Surface Hub üzerinde:

1. Surface Hub'açmak **ayarları**.
2. İstendiğinde hello aygıt yönetici kimlik bilgilerini girin.
3. Tıklatın **bu aygıt**ve altında hello **izleme**, tıklatın **OMS ayarlarını yapılandır**.
4. Seçin **izlemeyi etkinleştir**.
5. Merhaba OMS Ayarları iletişim kutusunda, hello yazın **çalışma alanı kimliği** ve türü hello **çalışma alanı anahtarı**.  
   ![Ayarlar](./media/log-analytics-surface-hubs/settings.png)
6. Tıklatın **Tamam** toocomplete hello yapılandırma.

Bir onay olsun veya olmasın OMS yapılandırması başarıyla hello toohello aygıt uygulanan söyleyen görüntülenir. İse, bu hello aracı toohello OMS hizmetine başarıyla bağlandı belirten bir ileti görüntülenir. Merhaba cihaz ardından burada görüntüleyebilir ve onun üzerinde işlem veri tooOMS göndermeye başlar.

## <a name="monitor-surface-hubs"></a>Surface Hubs İzleyicisi
Surface hub'larınız izleme OMS çok diğer kaydedilen cihazların izleme gibi kullanmaktır.

1. İçinde toohello OMS portalında oturum açın.
2. Toohello Surface Hub çözüm paketi Panosu gidin.
3. Cihazınızın sistem durumu görüntülenir.

   ![Yüzey Hub Panosu](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

Oluşturabileceğiniz [uyarıları](log-analytics-alerts.md) mevcut veya özel günlük aramaları tabanlı. Surface hub'larından OMS toplar hello veri hello kullanarak, sorunları ve uyarı aygıtlarınız için tanımladığınız hello koşullara için arama yapabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı Surface Hub veri.
* Oluşturma [uyarıları](log-analytics-alerts.md) toonotify, Surface hub'larıyla sorunları ortaya çıktığında.
