---
title: "Akış analizi: oturum açma kimlik bilgilerini girişleri ve çıkışları döndürme | Microsoft Docs"
description: "Nasıl tooupdate hello Stream Analytics girişleri ve çıkışları için kimlik bilgileri öğrenin."
keywords: "oturum açma kimlik bilgileri"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Giriş ve çıkış akış analizi işleri, oturum açma kimlik bilgileri döndürün
## <a name="abstract"></a>Özet
Azure Stream Analytics, bugün hello iş çalışırken bir giriş/çıkış hello kimlik bilgilerini değiştirme izin vermez.

Azure Stream Analytics işi son çıktısından desteklerken, biz tooshare hello tüm işlem durdurma hello hello işi başlatılıyor ve hello oturum açma kimlik bilgilerini döndürme arasında hello gecikme en aza indirmek için istedik.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>Bölüm 1 - hello yeni kimlik bilgileri kümesi hazırlama:
Giriş/Çıkış izleyen geçerli toohello parçasıdır:

* Blob Depolama
* Event Hubs
* SQL Database
* Tablo Depolama

Diğer giriş/çıkış için bölüm 2 ile devam edin.

### <a name="blob-storagetable-storage"></a>BLOB Depolama/tablo depolama
1. Toohello depolama uzantı hello Azure yönetim portalında gidin:  
   ![graphic1][graphic1]
2. İş tarafından kullanılan hello depolama bulun ve uygulamasına gidin:  
   ![graphic2][graphic2]
3. Merhaba erişim anahtarlarını Yönet komutuna tıklayın:  
   ![graphic3][graphic3]
4. Merhaba birincil erişim anahtarını hello ikincil erişim anahtarını arasındaki **hello bir iş tarafından kullanılmayan çekme**.
5. İsabet yeniden:  
   ![graphic4][graphic4]
6. Yeni oluşturulan hello anahtarı kopyalayın:  
   ![graphic5][graphic5]
7. TooPart 2 devam edin.

### <a name="event-hubs"></a>Olay hub'ları
1. Toohello Service Bus uzantısı hello Azure yönetim portalında gidin:  
   ![graphic6][graphic6]
2. Hizmet veri yolu, iş tarafından kullanılan Namespace Hello bulun ve uygulamasına gidin:  
   ![graphic7][graphic7]
3. İşinizi Service Bus Namespace hello üzerinde bir paylaşılan erişim ilkesi kullanıyorsa, toostep 6 atlama  
4. Toohello olay hub'ları sekmesine gidin:  
   ![graphic8][graphic8]
5. Merhaba, iş tarafından kullanılan olay hub'ı bulun ve uygulamasına gidin:  
   ![graphic9][graphic9]
6. Toohello yapılandırma sekmesine gidin:  
   ![graphic10][graphic10]
7. Hello ilkesi adı açılan, iş tarafından kullanılan hello Paylaşılan Erişim İlkesi'ni bulun:  
   ![graphic11][graphic11]
8. Merhaba birincil anahtar ve ikincil anahtar hello arasında **hello bir iş tarafından kullanılmayan çekme**.  
9. İsabet yeniden:  
   ![graphic12][graphic12]
10. Yeni oluşturulan hello anahtarı kopyalayın:  
   ![graphic13][graphic13]
11. TooPart 2 devam edin.  

### <a name="sql-database"></a>SQL Database
> [!NOTE]
> Not: tooconnect toohello SQL veritabanı hizmeti gerekir. Biz tooshow kullanarak bu toodo hello nasıl yönetim deneyimi Azure Yönetim Portalı hello ancak SQL Server Management Studio gibi bazı istemci-tarafı aracı da toouse seçebilirsiniz adımıdır.
>
> 

1. Toohello SQL veritabanları uzantısı hello Azure yönetim portalında gidin:  
   ![graphic14][graphic14]
2. Merhaba, iş tarafından kullanılan SQL veritabanını bulun ve **hello sunucusunda** hello üzerinde aynı bağlantı satır:  
   ![graphic15][graphic15]
3. Merhaba Yönet komutuna tıklayın:  
   ![graphic16][graphic16]
4. Veritabanı Yöneticisi türü:  
   ![graphic17][graphic17]
5. Kullanıcı adınızı, parolanızı yazın ve günlük tıklayın:  
   ![graphic18][graphic18]
6. Yeni sorgu tıklatın:  
   ![graphic19][graphic19]
7. < Login_name > sorgu değiştirerek aşağıdaki kullanıcı adınızı ve değiştirme hello türü <enterStrongPasswordHere> yeni parolanızla:  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Çalıştır'ı tıklatın:  
   ![graphic20][graphic20]
9. Toostep 2 geri dönün ve bu süre, hello veritabanı'ı tıklatın:  
   ![graphic21][graphic21]
10. Merhaba Yönet komutuna tıklayın:  
   ![graphic22][graphic22]
11. Kullanıcı adınızı, parolanızı girin ve oturum açma'ı tıklatın:  
   ![graphic23][graphic23]
12. Yeni sorgu tıklatın:  
   ![graphic24][graphic24]
13. Merhaba < Kullanıcı_adı > sorgu değiştirerek aşağıdaki tooidentify tarafından istediğiniz bir adla hello bağlamında bu veritabanı bu oturum açma yazın (size sağlayabilir hello verdiğiniz < login_name için >, örneğin aynı değere) ve < login_name > ile değiştirme Yeni kullanıcı adı:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Çalıştır'ı tıklatın:  
   ![graphic25][graphic25]
15. Şimdi yeni kullanıcı ile Merhaba sağlamalıdır aynı rolleri ve ayrıcalıkları, özgün kullanıcıya vardı.
16. TooPart 2 devam edin.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>2. Kısım: Durdurma hello akış analizi işi
1. Toohello Stream Analytics uzantısı hello Azure yönetim portalında gidin:  
   ![graphic26][graphic26]
2. İşinizi bulun ve uygulamasına gidin:  
   ![graphic27][graphic27]
3. Toohello girişleri veya olup bir giriş veya çıkış hello kimlik bilgileri döndürme dayalı hello çıkışları sekmesinde gidin.  
   ![graphic28][graphic28]
4. Merhaba Durdur komutu tıklatın ve hello işi durduruldu doğrulayın:  
   ![graphic29][graphic29] hello iş toostop için bekleyin.
5. Bulun hello giriş/çıkış istediğiniz toorotate kimlik bilgileri açık ve Git içine:  
   ![graphic30][graphic30]
6. TooPart 3 devam edin.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>3. Kısım: Hello akış analizi işi hello kimlik düzenleme
### <a name="blob-storagetable-storage"></a>BLOB Depolama/tablo depolama
1. Merhaba depolama hesabı anahtarı alanını bulun ve yeni oluşturulan anahtarınızı yapıştırın:  
   ![graphic31][graphic31]
2. Merhaba Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:  
   ![graphic32][graphic32]
3. Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatacak olan emin olun başarıyla geçti.
4. TooPart 4 devam edin.

### <a name="event-hubs"></a>Olay hub'ları
1. Merhaba olay hub'ı İlkesi anahtarı alanını bulun ve yeni oluşturulan anahtarınızı yapıştırın:  
   ![graphic33][graphic33]
2. Merhaba Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:  
   ![graphic34][graphic34]
3. Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatılacak başarıyla geçti emin olun.
4. TooPart 4 devam edin.

### <a name="power-bi"></a>Power BI
1. Merhaba yenileme yetkilendirme tıklatın:  

   ![graphic35][graphic35]
2. Hello aşağıdaki onay iletisini alırsınız:  

   ![graphic36][graphic36]
3. Merhaba Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:  
   ![graphic37][graphic37]
4. Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatılacak, emin olun, başarıyla geçti.
5. TooPart 4 devam edin.

### <a name="sql-database"></a>SQL Database
1. Kullanıcı adı ve parola alanlarına Hello bulur ve yeni oluşturulan kimlik bilgileri kümesini kopyalayıp yapıştırın:  
   ![graphic38][graphic38]
2. Merhaba Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:  
   ![graphic39][graphic39]
3. Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatılacak başarıyla geçti emin olun.  
4. TooPart 4 devam edin.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>4. Kısım: işinizi son durdurulma saatten başlayarak
1. Giriş/Çıkış Hello uzağa doğru gidin:  
   ![graphic40][graphic40]
2. Merhaba Başlat komutu tıklatın:  
   ![graphic41][graphic41]
3. Merhaba son durdurulma zamanı seçin ve Tamam'ı tıklatın:  
   ![graphic42][graphic42]
4. TooPart 5 devam edin.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>5. Kısım: Kaldırma hello eski kimlik bilgileri kümesi
Giriş/Çıkış izleyen geçerli toohello parçasıdır:

* Blob Depolama
* Event Hubs
* SQL Database
* Tablo Depolama

### <a name="blob-storagetable-storage"></a>BLOB Depolama/tablo depolama
1. Bölüm hello işinizi tarafından daha önce kullanılmış erişim anahtarı için yineleyin toorenew hello artık kullanılmayan erişim anahtarı.

### <a name="event-hubs"></a>Olay hub'ları
1. Bölüm hello işinizi tarafından daha önce kullanılmış anahtarı için yineleyin toorenew hello artık kullanılmayan anahtarı.

### <a name="sql-database"></a>SQL Database
1. Bölümü 1 adım 7 ve sorgu aşağıdaki, < previous_login_name > Merhaba, iş tarafından daha önce kullanılmış bir kullanıcı adı ile değiştirerek hello türü toohello sorgu penceresine dönün:  
   `DROP LOGIN <previous_login_name>`  
2. Çalıştır'ı tıklatın:  
   ![graphic43][graphic43]  

Onay aşağıdaki hello almanız gerekir: 

    Command(s) completed successfully.

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

