---
Başlık: aaa "Azure Analysis Services öğretici Ders 11: roller oluşturma | Microsoft Docs"Açıklama: Azure Analysis Services öğretici proje toocreate rollerinde nasıl hello açıklar. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-11-create-roles"></a>11. Ders: Rol oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu derste rol oluşturacaksınız. Rolleri model veritabanı nesnesi ve veri güvenliği erişim tooonly sınırlayarak Rol üyeleri olan kullanıcılarla sağlar. Her rol tek bir izinle tanımlanır: Hiçbiri, Okuma, Okuma ve İşlem, İşlem veya Yönetici. Roller, Rol Yöneticisi kullanılarak model yazma sırasında tanımlanabilir. Bir model dağıtıldıktan sonra SQL Server Management Studio’yu (SSMS) kullanarak rolleri yönetebilirsiniz. toolearn daha, fazla [rolleri](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).
  
> [!NOTE]  
> Roller oluşturma gerekli toocomplete bu öğreticidir. Varsayılan olarak, hello hesabı ile oturum açmış olduğunuz hello model üzerinde yönetici ayrıcalıklarına sahip. Ancak, raporlama istemcisi kullanarak, kuruluş toobrowse diğer kullanıcılar için en az bir rol ile Okuma izinleri oluşturun ve bu kullanıcıların üye olarak eklemeniz gerekir.  
  
Üç rol oluşturursunuz:  
  
-   **Satış Yöneticisi** – bu rol, istediğiniz toohave okuma izni tooall model nesneleri ve veri, kuruluşunuzdaki kullanıcılar içerebilir.  
  
-   **Satış analist ABD** – bu rol yalnızca toobe mümkün toobrowse verileri istediğiniz, kuruluşunuzdaki kullanıcılar içerebilir ilgili hello Amerika Birleşik Devletleri toosales. Bu rol için bir DAX formülü toodefine kullanmak bir *satır filtresi*, üyeleri yalnızca hello Amerika Birleşik Devletleri toobrowse verilerini kısıtlar.  
  
-   **Yönetici** – bu rol, sınırsız erişim ve izinleri tooperform yönetim görevlerini hello model veritabanını verir toohave yönetici izni istediğiniz kullanıcıları içerebilir.  
  
Kuruluşunuzdaki Windows kullanıcı ve grup hesaplarını benzersiz olduğundan, belirli kuruluş toomembers hesapları ekleyebilirsiniz. Ancak, Bu öğretici için aynı zamanda hello üyeleri boş bırakabilirsiniz. Daha sonra Ders 12'de her rol hello etkisini test edin: Excel'de Çözümle.  
  
Bu ders zaman toocomplete tahmini: **15 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 10: bölümleri oluşturma](../tutorials/aas-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Rol oluşturma  
  
#### <a name="toocreate-a-sales-manager-user-role"></a>toocreate satış yöneticisi kullanıcı rolü  
  
1.  Tablo Model Gezgini'nde **Roller** > **Roller**’e sağ tıklayın.  
  
2.  Rol Yöneticisi'nde **Yeni**’ye tıklayın.  
  
3.  Merhaba yeni rolüne tıklayın ve ardından hello **adı** sütun hello rol çok yeniden adlandırma**Satış Yöneticisi**.  
  
4.  Merhaba, **izinleri** sütunu hello açılır listeye tıklayın ve ardından hello seçin **okuma** izni. 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  İsteğe bağlı: Tıklatın hello **üyeleri** sekmesini ve ardından **Ekle**. Merhaba, **kullanıcıları veya Grupları Seç** iletişim kutusunda, hello Windows kullanıcıları veya grupları girin kuruluşunuzdan hello rolündeki tooinclude istiyor.  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a>toocreate satış analisti ABD kullanıcı rolü  
  
1.  Rol Yöneticisi'nde **Yeni**’ye tıklayın.    
  
2.  Merhaba rol çok yeniden adlandırma**satış analist ABD**.  
  
3.  Bu role **Okuma** izni verin.  
  
4.  Merhaba satır filtreler sekmesine tıklayın ve ardından hello **DimGeography** hello DAX filtre sütununda formülü aşağıdaki türü hello yalnızca, tablo:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Bir satır Filtresi Formülü tooa Boole (TRUE/FALSE) değeri çözmeniz gerekir. Bu formülü ile yalnızca "ABD" Merhaba ülke/bölge kodu değeri ile satırları görünür toohello kullanıcı olduğunu belirtiyorsanız.  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  İsteğe bağlı: Tıklatın hello **üyeleri** sekmesini ve ardından **Ekle**. Merhaba, **kullanıcıları veya Grupları Seç** iletişim kutusunda, hello Windows kullanıcıları veya grupları girin kuruluşunuzdan hello rolündeki tooinclude istiyor.  
  
#### <a name="toocreate-an-administrator-user-role"></a>toocreate bir yönetici kullanıcı rolü  
  
1.  **Yeni**’ye tıklayın.  
  
2.  Merhaba rol çok yeniden adlandırma**yönetici**.  
  
3.  Bu role **Yönetici** izni verin.  
  
4.  İsteğe bağlı: Tıklatın hello **üyeleri** sekmesini ve ardından **Ekle**. Merhaba, **kullanıcıları veya Grupları Seç** iletişim kutusunda, hello Windows kullanıcıları veya grupları girin kuruluşunuzdan hello rolündeki tooinclude istiyor. 
  
  
## <a name="whats-next"></a>Sırada ne var?
[12. Ders: Excel’de çözümleme](../tutorials/aas-lesson-12-analyze-in-excel.md).

  
  
