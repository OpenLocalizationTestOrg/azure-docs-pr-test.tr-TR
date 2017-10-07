---
Başlık: aaa "Azure Analysis Services öğretici Ders 3: tarih tablosu olarak işaretle | Microsoft Docs"Açıklama: nasıl toomark bir tarih tablosu hello Azure Analysis Services öğretici projesinde açıklar. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-3-mark-as-date-table"></a>3. Ders: Tarih Tablosu olarak işaretleme

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

2. Ders: Verileri alma sırasında DimDate adlı bir boyut tablosunu içeri aktardınız. Modelinizde bu tablo DimDate olarak adlandırılsa da, tarih ve saat verilerini içermesi bakımından *Tarih tablosu* olarak da bilinir.  
  
Daha sonra ölçü oluştururken yapacağınız gibi DAX akıllı zaman gösterimi işlevlerini her kullandığınızda, bir *Tarih tablosu* ve bu tabloda *Tarih sütunu* benzersiz tanımlayıcısını içeren özellikler belirtmeniz gerekir.
  
Bu alıştırmanın ilerisinde hello DimDate'i tablo hello olarak işaretlemek *tarih tablosu* ve hello tarih sütununun (Merhaba tarih tablosu) hello olarak *tarih sütunu* (benzersiz tanıtıcı).  

Başlangıç tarihi tablo ve tarih sütunu işaretlemeden önce biraz toomake, model daha kolay toounderstand housekeeping iyi zaman toodo var. Adlı bir sütun Hello DimDate'i tabloda fark **FullDateAlternateKey**. Bu sütun, hello tablosuna dahil her takvim yılın her günü için bir satır içerir. Bu sütunu ölçü formüllerinde ve raporlarda çok fazla kullanırsınız. Ancak, FullDateAlternateKey bu sütun için çok iyi bir tanımlayıcı değildir. Çok adlandırmadan**tarih**, daha kolay tooidentify yapma ve formüller içerir. Mümkün olduğunda, iyi bir fikir toorename olduğu gibi tablolar ve sütunlar toomake bunları SSDT ve uygulamaları Power BI ve Excel gibi raporlama istemcisi daha kolay tooidentify nesneleri. 
  
Bu ders zaman toocomplete tahmini: **üç dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 2: veri alma](../tutorials/aas-lesson-2-get-data.md). 

### <a name="toorename-hello-fulldatealternatekey-column"></a>toorename hello FullDateAlternateKey sütun

1.  Merhaba modeli Tasarımcısı'nda hello tıklayın **DimDate'i** tablo.

2.  Hello başlığı hello için çift **FullDateAlternateKey** sütun ve çok yeniden adlandırma**tarih**.

  
### <a name="tooset-mark-as-date-table"></a>tooset tarih tablosu olarak işaretle  
  
1.  Select hello **tarih** sütun ve ardından hello **özellikleri** penceresi altında **veri türü**, emin olun **tarih** seçilir.  
  
2.  Merhaba tıklatın **tablo** menüsünde, ardından **tarih**ve ardından **tarih tablosu olarak işaretle**.  
  
3.  Merhaba, **tarih tablosu olarak işaretle** iletişim kutusunda hello **tarih** listbox, select hello **tarih** benzersiz tanımlayıcı hello gibi sütun. Bu sütun genellikle varsayılan olarak seçilidir. **Tamam** düğmesine tıklayın. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>Sırada ne var?
[4. Ders: İlişki oluşturma](../tutorials/aas-lesson-4-create-relationships.md).
  
