---
Başlık: aaa "Azure Analysis Services öğretici Ders 13: dağıtma | Microsoft Docs"Açıklama: nasıl toodeploy hello öğretici proje tooAzure Analysis Services açıklar.
Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend
---
# <a name="lesson-13-deploy"></a>13. Ders: Dağıtma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu alıştırmanın ilerisinde dağıtım özelliklerini yapılandırın; bir Azure Analysis Services sunucusu toodeploy tooand hello modeli için bir ad belirtme. Merhaba model toothat örneğini dağıtırsınız. Model dağıtıldıktan sonra kullanıcılar bir raporlama istemci uygulaması kullanarak tooit bağlanabilir. toolearn daha, fazla [tooAzure Analysis Services dağıtma](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Bu ders zaman toocomplete tahmini: **5 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 12: Excel'de Çözümle özelliğini](../tutorials/aas-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Bilmeniz gereken [yönetici izinleri](../analysis-services-server-admins.md) üzerinde hello uzak Analysis Services sunucusu sıralı toodeploy tooit.  

> [!IMPORTANT]  
> Bir şirket içi SQL sunucusunda hello AdventureWorksDW2014 örnek veritabanı yüklediyseniz ve model tooan Azure Analysis Services sunucusuna dağıtıyorsunuz bir [şirket içi veri ağ geçidi](../analysis-services-gateway.md) gereklidir.
  
## <a name="deploy-hello-model"></a>Merhaba model dağıtma  
  
#### <a name="tooconfigure-deployment-properties"></a>tooconfigure dağıtım özellikleri  

  
1.  İçinde **Çözüm Gezgini**, sağ hello **AW Internet satış** proje ve ardından **özellikleri**.  
  
2.  Merhaba, **AW Internet satış özellik sayfaları** iletişim kutusunda **dağıtım sunucusu**, hello içinde **Server** özelliği, hello tam sunucu girin.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  Merhaba, **veritabanı** özelliği, türü **Adventure Works Internet satış**.  
  
4.  Merhaba, **Model adı** özelliği, türü **Adventure Works Internet satış modeli**.  
  
5.  Seçimlerinizi doğrulayıp **Tamam**’a tıklayın.  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>toodeploy hello Adventure Works Internet satış
  
1.  İçinde **Çözüm Gezgini**, sağ hello **AW Internet satış** Proje > **yapı**.  

2.  Sağ hello **AW Internet satış** Proje > **dağıtma**.

    TooAzure Analysis Services dağıtırken, olabilir istendiğinde tooenter hesabınızın olması. Kuruluş hesabınızı ve parolanızı girin, örneğin nancy@adventureworks.com. Bu hesap Admins hello sunucuda olmalıdır.
  
    Merhaba Dağıt iletişim kutusu görünür ve başlangıç dağıtım durumu hello meta verilerin ve hello modele dahil her bir tablo görüntüler.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. Dağıtım başarıyla tamamlandığında devam edin ve **Kapat**’a tıklayın.  
  
## <a name="conclusion"></a>Sonuç  
Tebrikler! İlk Analysis Services Tablo modelinizi yazma ve dağıtma işlemini tamamladınız. Bu öğretici, tablolu model oluşturma hello en yaygın görevleri tamamlama aracılığıyla Kılavuzu Yardım. Adventure Works Internet satış modelinizi dağıtılır, SQL Server Management Studio toomanage hello modelini kullanabilirsiniz; işlem komut dosyaları ve bir yedekleme planı oluşturun. Kullanıcılar artık Microsoft Excel veya Power BI gibi bir raporlama istemci uygulaması kullanarak toohello modeli bağlanabilir.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Sırada ne var?
[Power BI Desktop ile bağlanma](../analysis-services-connect-pbi.md)   
[Ek Ders - Dinamik güvenlik](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Ek Ders - Ayrıntı satırları](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[Ek Ders - Düzensiz hiyerarşiler](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
