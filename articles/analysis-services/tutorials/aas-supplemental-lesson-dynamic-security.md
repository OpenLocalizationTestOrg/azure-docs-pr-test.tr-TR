---
Başlık: aaa "Azure Analysis Services öğretici ek Ders: dinamik güvenlik | Microsoft Docs"Açıklama: satır kullanarak dinamik güvenlik toouse hello Azure Analysis Services öğreticide nasıl filtreler açıklar.
Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>Ek ders - Dinamik güvenlik

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu ek derste dinamik güvenlik uygulayan bir ek rol oluşturacaksınız. Dinamik güvenlik hello kullanıcının adını veya oturum açma kimliği şu anda oturum açmış hello göre satır düzeyi güvenlik sağlar. 
  
tooimplement dinamik güvenlik toohello modeli bağlanabilir ve model nesneleri ve veri Gözat kullanıcılarla hello kullanıcı adlarını içeren bir tablo tooyour model ekleyin. Bu öğretici kullanarak oluşturduğunuz hello hello Adventure Works bağlamında modeldir; Ancak, toocomplete bu ders, kendi etki alanındaki kullanıcıları içeren bir tablo eklemeniz gerekir. Eklenen hello kullanıcı adları için hello parolaları gerekmez. toocreate bir EmployeeSecurity tablosuyla kendi etki alanındaki kullanıcıların küçük bir örnek Excel elektronik tablosu çalışan verilerini yapıştırma hello Yapıştır özelliğini kullanın. Gerçek hayattaki bir senaryoda, kullanıcı adlarını içeren hello tablo genelde bir veri kaynağı olarak bir asıl veritabanını tablosundan olacaktır; Örneğin, gerçek DimEmployee tablo.  
  
tooimplement dinamik güvenlik, iki DAX işlevleri kullanın: [kullanıcıadı işlevi (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) ve [LOOKUPVALUE işlevi (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Bu işlevler bir satır filtresi formülüne uygulanır ve yeni bir rolde tanımlanır. Merhaba LOOKUPVALUE işlevinde kullanarak hello formülü hello EmployeeSecurity tablosundan bir değer belirtir. Merhaba formülü sonra hello kullanıcının oturum açmış hello kullanıcı adını belirtir değeri toohello kullanıcıadı işlevi toothis role ait geçirir. Merhaba kullanıcı ardından hello rolün satır filtreler tarafından belirtilen veri göz atabilirsiniz. Bu senaryoda, satış Çalışanlar yalnızca Internet satış verileri hello satış bölgeleri üyesi olduğu için Gözat belirtin.  
  
Benzersiz toothis Adventure Works tablolu model senaryo ancak mutlaka tooa gerçek dünya senaryoları uygulanacak değil, bu görevleri şekilde tanımlanır. Her görev hello görev hello amacını açıklayan ek bilgiler içerir.  
  
Bu ders zaman toocomplete tahmini: **30 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu ek ders konusu, sırayla tamamlanması gereken bir tablosal modelleme öğreticisinin bir parçasıdır. Bu ek Ders Hello görevleri gerçekleştirmeden önce tüm önceki dersleri tamamlandı.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Merhaba DimSalesTerritory tablo toohello AW Internet satış tablolu modeli projesi ekleme  
tooimplement dinamik güvenlik bu Adventure Works senaryo için iki ek tablolar tooyour modeli eklemeniz gerekir. ' den (olarak, satış bölgeleri) DimSalesTerritory olan ekleyin hello ilk tablonun aynı AdventureWorksDW veritabanına hello. Daha sonra hello belirli verileri tanımlayan bir satır filtresi toohello SalesTerritory tablosu uygulamak oturum açan kullanıcı hello göz atın.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>tooadd hello DimSalesTerritory tablosu  
  
1.  Tablosal Model Gezgini'nde > **Veri Kaynakları**, bağlantınıza sağ tıklayın ve ardından **Yeni Tabloları İçeri Aktar**'a tıklayın.  

    Merhaba kimliğe bürünme kimlik bilgileri iletişim kutusu görüntülenirse, Ders 2'de, kullanılan hello kimliğe bürünme kimlik bilgileri yazın: veri ekleyin.
  
2.  Merhaba Gezgini içinde seçin **DimSalesTerritory** tablo ve ardından **Tamam**.    
  
3.  Sorgu Düzenleyicisi'nde hello tıklatın **DimSalesTerritory** sorgulamak ve Kaldır'ı **SalesTerritoryAlternateKey** sütun.  
  
7.  **İçeri Aktar**’a tıklayın.  
  
    Merhaba yeni tablo toohello modeli çalışma eklenir. Nesneleri ve hello kaynak DimSalesTerritory tablodan veri AW Internet satış tablo modelinizi alınır.  
  
9. Merhaba tablo başarıyla içeri aktarıldı sonra tıklayın **Kapat**.  

## <a name="add-a-table-with-user-name-data"></a>Kullanıcı adı verilerinin bulunduğu bir tablo ekleme  
Merhaba DimEmployee hello AdventureWorksDW örnek veritabanı tablosunda hello AdventureWorks etki alanındaki kullanıcıları içerir. Bu kullanıcı adları kendi ortamınızda mevcut değildir. Modelinizde kuruluşunuzdan birkaç kişiyi (en az üç) içeren bir tablo oluşturmanız gerekir. Bu kullanıcılar sonra üyeleri toohello yeni rolü olarak ekleyin. Merhaba örnek kullanıcı adları için hello parolaları gerekmez, ancak kendi etki alanından gerçek Windows kullanıcı adı gerekir.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>tooadd bir EmployeeSecurity tablosu  
  
1.  Microsoft Excel'i açıp bir çalışma sayfası oluşturun.  
  
2.  Aşağıdaki tablonun Hello başlık satırındaki dahil olmak üzere, hello kopyalayın ve hello çalışma sayfasına yapıştırın.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Merhaba ad, Soyadı ve etkialanı\kullanıcıadı hello adlarını ve kuruluşunuzdaki üç kullanıcılar oturum açma kimliklerini değiştirin. Merhaba put EmployeeID 1, bu kullanıcının ait olduğu tek bir satış bölge'den toomore gösteren hello ilk iki satırını aynı kullanıcı. Oldukları gibi hello EmployeeID ve SalesTerritoryId alanları bırakın.  
  
4.  Merhaba çalışma sayfası olarak Kaydet **SampleEmployee**.  
  
5.  Çalışan verilerini, hello üstbilgileri dahil olmak üzere tüm hello hücrelerle Hello çalışma sayfasında, seçin sonra seçili hello veri sağ tıklatın ve ardından **kopya**.  
  
6.  Merhaba SSDT içinde tıklatın **Düzenle** menüsüne ve ardından **Yapıştır**.  
  
    Yapıştır gri, hiçbir sütun hello modeli Tasarımcısı penceresinde herhangi bir tablodaki'ı tıklatın ve yeniden deneyin.  
  
7.  Merhaba, **Yapıştır Önizleme** iletişim kutusunda **tablo adı**, türü **EmployeeSecurity**.  
  
8.  İçinde **yapıştırılan veri toobe**, hello verileri içeren tüm hello kullanıcı verileri ve üstbilgileri hello SampleEmployee çalışma sayfasından doğrulayın.  
  
9. **İlk satırı sütun başlığı olarak kullan** seçeneğinin işaretli olduğundan emin olun ve **Tamam**'a tıklayın.  
  
    Merhaba SampleEmployee çalışma sayfasından kopyalanan çalışan veri EmployeeSecurity adında yeni bir tablo oluşturulur.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>FactInternetSales, DimGeography ve DimSalesTerritory tabloları arasında ilişki oluşturma  
Merhaba Factınternetsales, DimGeography ve DimSalesTerritory tablosu tüm SalesTerritoryId ortak bir sütun içerir. Merhaba DimSalesTerritory tablodaki Hello SalesTerritoryId sütun satış her bölge için farklı bir kimlik değerleri içerir.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>Merhaba Factınternetsales, DimGeography ve hello DimSalesTerritory tablo arasındaki toocreate ilişkileri  
  
1.  Diyagram görünümünde, hello **DimGeography** tablo,'ı tıklatın ve üzerinde hello tutun **SalesTerritoryId** sütun sonra sürükleme hello imleç toohello **SalesTerritoryId** hello sütununda **DimSalesTerritory** tablo ve bırakın.  
  
2.  Merhaba, **Factınternetsales** tablo,'ı tıklatın ve üzerinde hello tutun **SalesTerritoryId** sütun sonra sürükleme hello imleç toohello **SalesTerritoryId** hello sütununda **DimSalesTerritory** tablo ve bırakın.  
  
    Bildirim hello etkin özelliği bu ilişki için etkin olmayan deyişle False ' tır. Merhaba Factınternetsales tablosunda başka bir etkin ilişki zaten mevcut.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>Merhaba EmployeeSecurity tablo istemci uygulamalardan Gizle  
Bu görevde, bir istemci uygulamanın alan listesindeki görünmesini tutma hello EmployeeSecurity tablo gizleyin. Gizleme işleminin, tabloyu güvenli hale getirmeyeceğini unutmayın. Nasıl yapacağını bilen kullanıcılar EmployeeSecurity tablosundaki verileri sorgulayabilir. toosecure Merhaba EmployeeSecurity tablo verileri, kullanıcıların mümkün tooquery olmasını önleyen herhangi verilerini, daha yeni bir görevi bir filtre uygulayın.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>istemci uygulamaları toohide hello EmployeeSecurity tablosundan  
  
-   Diyagram görünümünde hello modeli Tasarımcısı'nda hello sağ **çalışan** tablo başlık ve ardından **istemci Araçları'ndan Gizle**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Sales Employees by Territory kullanıcı rolü oluşturma  
Bu görevde bir kullanıcı rolü oluşturacaksınız. Bu rolü hangi hello DimSalesTerritory tablonun satırlarını görünür toousers olduğunu tanımlama bir satır filtresi içerir. Merhaba filtre sonra uygulanır hello bire çok ilişkide tooall yönü diğer ilgili tooDimSalesTerritory tabloları. Ayrıca hello rolünün bir üyesi olan herhangi bir kullanıcı tarafından sorgulanabilir engeller hello tüm EmployeeSecurity tablo güvenli hale getirdiği bir filtre uygulayın.  
  
> [!NOTE]  
> Merhaba satış çalışanlar bu ders oluşturduğunuz bölge Rol üyeleri toobrowse (veya sorgu) yalnızca satış verilerini ait oldukları hello satış bölge toowhich kısıtlar. Bir rol bir üye oluşturulmuş olan da var olan bölge rolüne göre üye toohello Satış çalışanları olarak kullanıcı ekleme, [Ders 11: roller oluşturmak](../tutorials/aas-lesson-11-create-roles.md), izinleri bileşimini alın. Bir kullanıcı birden çok rol, hello izinleri ve her rol için tanımlanan satır filtrelerini üyesi olduğunda toplu. Diğer bir deyişle, hello kullanıcı rolleri hello birleşimi tarafından belirlenen hello büyük izinlerine sahip değil.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate bölge kullanıcı rolüne göre satış çalışanları  
  
1.  Merhaba SSDT içinde tıklatın **modeli** menüsüne ve ardından **rolleri**.  
  
2.  **Rol Yöneticisi**'nde **Yeni**'ye tıklayın.  
  
    Yeni bir rol ile Merhaba hiçbiri izni toohello listesi eklendi.  
  
3.  Merhaba yeni rolüne tıklayın ve ardından hello **adı** sütun hello rol çok yeniden adlandırma**bölgeye göre satış çalışanları**.  
  
4.  Merhaba, **izinleri** sütunu hello açılır listeye tıklayın ve ardından hello seçin **okuma** izni.  
  
5.  Merhaba tıklatın **üyeleri** sekmesini ve ardından **Ekle**.  
  
6.  Merhaba, **kullanıcı veya Grup Seç** iletişim kutusunda **tooselect adlı Enter hello nesne**, hello EmployeeSecurity tablo oluştururken kullanılan türü hello ilk örnek kullanıcı adı. Tıklatın **Adları Denetle** tooverify hello kullanıcı adının geçerli olduğundan ve ardından **Tamam**.  
  
    Merhaba EmployeeSecurity tablo oluştururken kullanılan diğer örnek kullanıcı adları Hello ekleme, bu adımı yineleyin.  
  
7.  Merhaba tıklatın **satır filtrelerini** sekmesi.  
  
8.  Hello için **EmployeeSecurity** tabloda hello **DAX filtre** sütun, formül aşağıdaki türü hello:  
  
    ```
      =FALSE()  
    ```
  
    Bu formülü tüm sütunları toohello false Boole koşulunu gidermek belirtir. Merhaba EmployeeSecurity tablosu için hiç sütun hello satış çalışanlar tarafından bölge kullanıcı rolü üyesi tarafından sorgulanabilir.  
  
9. Hello için **DimSalesTerritory** tablo, formül aşağıdaki türü hello:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    Bu formülde burada hello EmployeeSecurity [LoginId] olan hello aynı hello geçerli Windows kullanıcı adı ve EmployeeSecurity [oturum olarak hello LOOKUPVALUE işlevinde hello DimEmployeeSecurity [SalesTerritoryId] sütunu için tüm değerleri döndürür SalesTerritoryId] olan hello hello DimSalesTerritory [SalesTerritoryId] ile aynı.  
  
    kullanılan toorestrict hello sonra hello DimSalesTerritory tabloda gösterilen satırları hello LOOKUPVALUE tarafından döndürülen satış bölge kimlikleri kümesidir. Merhaba SalesTerritoryID hello satır için kimlikleri hello LOOKUPVALUE işlevi tarafından döndürülen hello kümesindeki olduğu yalnızca satır görüntüleniyor.  
  
10. Rol Yöneticisi'nde **Tamam**'a tıklayın.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Merhaba Satış çalışanları bölge kullanıcı Role göre test etme  
Bu görevde SSDT tootest hello sürecinin hello Satış çalışanları bölge kullanıcı rolüne göre içinde hello Çözümle Excel özelliğini kullanın. Bir tane belirtin toohello EmployeeSecurity tablo eklediğiniz hello kullanıcı adlarını ve hello rolünün bir üyesi olarak. Bu kullanıcı adı, ardından Excel ve hello modeli arasında oluşturulan hello bağlantı hello etkin kullanıcı adı olarak kullanılır.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>Bölge kullanıcı rolüne göre tootest hello Satış çalışanları  
  
1.  Merhaba SSDT içinde tıklatın **modeli** menüsüne ve ardından **Excel'de çözümleme özelliği**.  
  
2.  Merhaba, **Excel'de çözümleme özelliği** iletişim kutusunda **belirt hello kullanıcı adını veya rolü toouse tooconnect toohello modeli**seçin **başka bir Windows kullanıcı**ve ardından**Gözat**.  
  
3.  Merhaba, **kullanıcı veya Grup Seç** iletişim kutusunda **hello nesne adı tooselect girin**hello EmployeeSecurity tablosunda bulunan bir kullanıcı adı yazın ve ardından **Adları Denetle**.  
  
4.  Tıklatın **Tamam** tooclose hello **kullanıcı veya Grup Seç** iletişim kutusunu ve ardından **Tamam** tooclose hello **Excel'de çözümleme özelliği** iletişim kutusu.  
  
    Excel yeni bir çalışma kitabı ile açılır. Bir PivotTable otomatik olarak oluşturulur. Merhaba PivotTable alanları listesi hello veri alanları yeni modelinizde kullanılabilir çoğunu içerir.  
  
    Bildirim hello EmployeeSecurity tablo hello PivotTable alanlar listesinde görünür değil. Bu tabloyu önceki görevlerden birinde istemci araçlarından gizlemiştiniz.  
  
5.  Merhaba, **alanları** listesinde **∑ Internet satış** (ölçüler) select hello **InternetTotalSales** ölçü. Merhaba ölçü hello girdiğiniz **değerleri** alanları.  
  
6.  Select hello **SalesTerritoryId** hello sütundan **DimSalesTerritory** tablo. Merhaba sütun hello girdiğiniz **satır etiketleri** alanları.  
  
    Kullandığınız yalnızca hello bir bölge toowhich hello etkili kullanıcı adı için satış rakamlarını görünen bildirim Internet aittir. Başka bir sütunu seçerseniz, satır etiket alanı, yalnızca şehirlerde hello satış bölge toowhich hello etkili kullanıcı ait olduğu gibi hello DimGeography tablosundan şehir gibi görüntülenir.  
  
    Bu kullanıcı göz atın veya herhangi bir Internet satış veri ait hello biri dışındaki bölgeler için sorgu. Bu kısıtlama Hello hello satış çalışanlar bölge kullanıcı rolüne göre de hello DimSalesTerritory tablosunda tanımlanan satır filtresi tüm veriler için veri güvenliğini sağlar çünkü ilgili tooother satış bölgeleri.  
  
## <a name="see-also"></a>Ayrıca Bkz.  
[USERNAME İşlevi (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE İşlevi (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA İşlevi (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  