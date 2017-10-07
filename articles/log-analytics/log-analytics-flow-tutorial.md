---
title: "aaaAutomate Azure günlük analizi Microsoft Flow işler."
description: "Microsoft Flow nasıl kullanabileceğinizi öğrenin tooquickly hello Azure günlük analizi Bağlayıcısı'nı kullanarak yinelenebilir işlemleri otomatikleştirme."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>İçin Microsoft Flow hello bağlayıcı ile günlük analizi işlemlerini otomatikleştirmeyi
[Microsoft Flow](https://ms.flow.microsoft.com) Eylemler yüzlerce çok çeşitli hizmetlerini kullanarak otomatik toocreate iş akışları sağlar. Bir eylem çıktısını farklı hizmetler arasında toocreate tümleştirme izin vererek giriş tooanother olarak kullanılabilir.  Hello Azure günlük analizi Bağlayıcısı Microsoft Flow için günlük analizi günlük aramalarda tarafından alınan veri dahil toobuild iş akışları sağlar.

Örneğin, Office 365'ten bir e-posta bildiriminin Microsoft Flow toouse günlük analizi veri kullanın, Visual Studio Team Services içinde oluşturma veya Slack iletisi.  Bir iş akışı, bir basit zamanlama veya bağlantılı hizmetindeki bir posta ya da bir tweet alındığında gibi bazı eylemleri tetikleyebilirsiniz.  


> [!NOTE]
> Microsoft Flow Hello Azure günlük analizi bağlayıcı çalışma yükseltilmiş toobe toohello yeni günlük analizi sorgu dilini gerektirir. Merhaba yeni dil hakkında daha fazla bilgi ve çalışma alanı hello yordamı tooupgrade almak [Azure günlük analizi çalışma alanı toonew günlük aramanızı yükseltme](log-analytics-log-search-upgrade.md).  

Bu makalede Hello öğretici nasıl toocreate otomatik olarak gönderir bir akış hello günlük analizi günlük arama sonuçlarını e-posta, günlük analizi Microsoft Flow nasıl kullanabileceğiniz yalnızca bir örneği gösterir. 


## <a name="step-1-create-a-flow"></a>1. adım: bir akışı oluşturma
1. Çok oturum[Microsoft Flow](http://flow.microsoft.com)seçip **My akar**.
2. Tıklatın **+ Oluştur boş**.

## <a name="step-2-create-a-trigger-for-your-flow"></a>2. adım: akışınız için bir Tetikleyici oluşturma
1. Tıklatın **arama bağlayıcılar ve Tetikleyicileri yüzlerce**.
2. Tür **zamanlama** hello arama kutusuna.
3. Seçin **zamanlama**ve ardından **çizelgesi - yinelenme**.
4. Merhaba, **sıklığı** kutusunda seçin **gün** ve hello **aralığı** kutusuna **1**.<br><br>![Microsoft Flow tetikleyici iletişim kutusu](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>3. adım: bir günlük analizi eylem ekleme
1. Tıklatın **+ yeni adım**ve ardından **Eylem Ekle**.
2. Arama **oturum Analytics**.
3. Tıklatın **Azure günlük analizi – sorgu çalıştırmak ve sonuçlarını görselleştirme**.<br><br>![Günlük analizi sorgu penceresi](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>4. adım: hello günlük analizi eylemi yapılandırın

1. Merhaba abonelik kimliği, kaynak grubu ve çalışma alanı adı dahil olmak üzere çalışma alanınızı Hello ayrıntılarını belirtin.
2. Günlük analizi sorgu toohello aşağıdaki hello eklemek **sorgu** penceresi.  Bu yalnızca bir örnek sorgu ve veri veren diğer tüm değiştirin.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. Seçin **HTML tablosu** hello için **grafik türü**.<br><br>![Günlük analizi eylemi](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>Adım 5: hello akış toosend e-posta yapılandırma

1. Tıklatın **yeni adım**ve ardından **+ Eylem Ekle**.
2. Arama **Office 365 Outlook**.
3. Tıklatın **Office 365 Outlook – bir e-posta Gönder**.<br><br>![Office 365 Outlook seçim penceresi](media/log-analytics-flow-tutorial/flow04.png)

4. Bir alıcı Hello e-posta adresini hello belirtin **için** penceresi ve hello e-posta için bir konu **konu**.
5. Hello herhangi bir yere tıklayın **gövde** kutusu.  A **dinamik içerik** önceki Eylemler değerlerle penceresi açılır.  
6. Seçin **gövde**.  Merhaba hello günlük analizi eylemin hello sorgu sonuçlarını budur.
6. Tıklatın **Gelişmiş Seçenekleri Göster**.
7. Merhaba, **HTML'dir** kutusunda **Evet**.<br><br>![Office 365 e-posta yapılandırma penceresi](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>6. adım: Kaydetmek ve akışınız test
1. Merhaba, **Akış adı** kutusuna akışınız için bir ad ekleyin ve ardından **akışı oluşturmak**.<br><br>![Akış Kaydet](media/log-analytics-flow-tutorial/flow06.png)
2. Merhaba akış şimdi oluşturulur ve belirttiğiniz hello zamanlaması olan bir gün sonra çalıştırılır. 
3. tooimmediately test hello akış tıklatın **Şimdi Çalıştır** ve ardından **akışı çalıştırmak**.<br><br>![Akış çalıştırın](media/log-analytics-flow-tutorial/flow07.png)
3. Merhaba akışı tamamlandığında, belirttiğiniz hello alıcının hello posta denetleyin.  Gövde benzer toohello aşağıdakileri içeren bir posta almış olmanız gerekir:<br><br>![Örnek e-posta](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla bilgi edinmek [günlük analizi aramaları oturum](log-analytics-log-search-new.md).
- Daha fazla bilgi edinmek [Microsoft Flow](https://ms.flow.microsoft.com).



