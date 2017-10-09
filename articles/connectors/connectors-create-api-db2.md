---
title: "Mantıksal uygulamalarınızı aaaAdd hello DB2 Bağlayıcısı | Microsoft Docs"
description: "DB2 Bağlayıcısı REST API parametrelerle genel bakış"
services: 
documentationcenter: 
author: gplarsen
manager: erikre
editor: 
tags: connectors
ms.assetid: 1c6b010c-beee-496d-943a-a99e168c99aa
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: d836c61231d3c9cfdb30ff9c40a48b1718f3ffb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-db2-connector"></a>Merhaba DB2 Bağlayıcısı ile çalışmaya başlama
DB2 için Microsoft Bağlayıcısı bir IBM DB2 veritabanında depolanan Logic Apps tooresources bağlanır. Bu bağlayıcı bir TCP/IP ağı üzerinden uzak DB2 sunucu bilgisayarlarla Microsoft istemci toocommunicate içerir. Bu bulut veritabanları, IBM Bluemix dashDB veya Azure sanallaştırma çalışan Windows için IBM DB2 gibi içerir ve şirket içi hello şirket içi veri ağ geçidi kullanarak veritabanlarını. Merhaba bkz [liste desteklenen](connectors-create-api-db2.md#supported-db2-platforms-and-versions) IBM DB2 platformları ve sürümleri (Bu konudaki).

Merhaba DB2 Bağlayıcısı veritabanı işlemleri aşağıdaki hello destekler:

* Liste veritabanı tabloları
* SELECT kullanarak bir satır okuma
* Tüm satırları seçin kullanarak okuyun
* INSERT kullanarak bir satır Ekle
* Alter bir satır güncelleştirme kullanma
* DELETE kullanma bir satırı Kaldır

Bu konu, nasıl bir mantıksal uygulama tooprocess toouse hello Bağlayıcısı veritabanı işlemleri gösterir.

Logic Apps hakkında daha fazla toolearn bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Kullanılabilir eylemler
Merhaba DB2 Bağlayıcısı mantıksal uygulama eylemleri aşağıdaki hello destekler:

* GetTables
* GetRow
* GetRows
* Insertrow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Listede tablolar
Merhaba Microsoft Azure portalı üzerinden gerçekleştirilen birçok adımlar herhangi bir işlem için bir mantıksal uygulama oluşturma oluşur.

Merhaba mantıksal uygulama içinde bir DB2 veritabanında bir eylem toolist tablolar ekleyebilirsiniz. Hello eylemin hello bağlayıcı tooprocess bir DB2 schema deyiminin gibi bildirir `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `Db2getTables`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından hello ayarlayın**Aralığı** tootype **7**.  
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın `db2` hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **DB2 - Get tabloları (Önizleme)**.
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. Merhaba, **DB2 - Get tablolar** yapılandırma bölmesinde, **onay kutusunu** tooenable **Connect şirket içi veri ağ geçidi üzerinden**. Bulut tooon içi hello ayarlarını değiştirme dikkat edin.
   
   * Tür için değer **Server**, adres veya diğer iki nokta üst üste bağlantı noktası numarası hello biçiminde. Örneğin, `ibmserver01:50000`.
   * Tür için değer **veritabanı**. Örneğin, `nwind`.
   * İçin değer seçin **kimlik doğrulama**. Örneğin, seçin **temel**.
   * Tür için değer **kullanıcıadı**. Örneğin, `db2admin`.
   * Tür için değer **parola**. Örneğin, `Password1`.
   * İçin değer seçin **ağ geçidi**. Örneğin, seçin **datagateway01**.
7. Seçin **oluşturma**ve ardından **kaydetmek**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. Merhaba, **Db2getTables** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
9. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_tables**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; tabloların bir listesini içermelidir.
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Merhaba bağlantıları oluşturma
Bu bağlayıcı içi barındırılan toodatabases bağlantılarını destekler ve hello bulutta kullanarak hello bağlantı özelliklerini aşağıdaki. 

| Özellik | Açıklama |
| --- | --- |
| sunucu |Gereklidir. TCP/IP adresi veya izlenen IPv4 veya IPv6 biçiminde (virgülle ayrılmış) diğer bir TCP/IP bağlantı noktası numarası ile temsil eden bir dize değeri kabul eder. |
| Veritabanı |Gereklidir. Bir DRDA ilişkisel veritabanı adı (RDBNAM) temsil eden bir dize değeri kabul eder. DB2 z/OS için 16 bayt dizesini kabul eder (bir IBM DB2 z/OS konumu olarak veritabanı bilinir). DB2 i5/OS için kabul 18-bayt dizisi (veritabanı için bir IBM DB2 olarak bilinir i ilişkisel veritabanı). DB2 LUW için 8-bayt dizisi kabul eder. |
| Kimlik doğrulaması |İsteğe bağlı. Bir liste öğesi değeri, temel veya Windows (kerberos) kabul eder. |
| kullanıcı adı |Gereklidir. Bir dize değeri kabul eder. DB2 z/OS için 8-bayt dizisi kabul eder. DB2 için i 10 bayt dizesini kabul eder. DB2 Linux veya UNIX için 8-bayt dizisi kabul eder. DB2 için Windows 30-bayt dizesini kabul eder. |
| password |Gereklidir. Bir dize değeri kabul eder. |
| Ağ geçidi |Gereklidir. Merhaba depolama grubu içinde Hello şirket içi veri tanımlı ağ geçidi tooLogic uygulamaları temsil eden bir liste öğesi değeri kabul eder. |

## <a name="create-hello-on-premises-gateway-connection"></a>Merhaba şirket içi ağ geçidi bağlantısı oluşturma
Bu bağlayıcı hello şirket içi ağ geçidi kullanarak bir şirket içi DB2 veritabanına erişebilir. Daha fazla bilgi için ağ geçidi konularına bakın. 

1. Merhaba, **ağ geçitleri** yapılandırma bölmesinde, **onay kutusunu** tooenable **Connect ağ geçidi üzerinden**. Bulut tooon içi hello ayarlarını değiştirme dikkat edin.
2. Tür için değer **Server**, adres veya diğer iki nokta üst üste bağlantı noktası numarası hello biçiminde. Örneğin, `ibmserver01:50000`.
3. Tür için değer **veritabanı**. Örneğin, `nwind`.
4. İçin değer seçin **kimlik doğrulama**. Örneğin, seçin **temel**.
5. Tür için değer **kullanıcıadı**. Örneğin, `db2admin`.
6. Tür için değer **parola**. Örneğin, `Password1`.
7. İçin değer seçin **ağ geçidi**. Örneğin, seçin **datagateway01**.
8. Seçin **oluşturma** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Merhaba bulut bağlantı oluşturma
Bu bağlayıcı bir bulut DB2 veritabanına erişebilir. 

1. Merhaba, **ağ geçitleri** yapılandırma bölmesinde, bırakın hello **onay kutusunu** (Tıklatılmamış) devre dışı **Connect ağ geçidi üzerinden**. 
2. Tür için değer **bağlantı adı**. Örneğin, `hisdemo2`.
3. Tür için değer **DB2 sunucu adı**, adres veya diğer iki nokta üst üste bağlantı noktası numarası hello biçiminde. Örneğin, `hisdemo2.cloudapp.net:50000`.
4. Tür için değer **DB2 veritabanı adı**. Örneğin, `nwind`.
5. Tür için değer **kullanıcıadı**. Örneğin, `db2admin`.
6. Tür için değer **parola**. Örneğin, `Password1`.
7. Seçin **oluşturma** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Tüm satırları seçin kullanarak getirme
Bir DB2 tablodaki tüm satırları mantığı uygulama eylem toofetch tanımlayabilirsiniz. Bu gibi hello bağlayıcı tooprocess bir DB2 SELECT deyimi bildirir `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `Db2getRows`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın `db2` hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **DB2 - Get satırları (Önizleme)**.
6. Merhaba, **alma satırları (Önizleme)** eylem, select **değiştirmek bağlantı**.
7. Merhaba, **bağlantıları** yapılandırma bölmesinde, **Yeni Oluştur**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. Merhaba, **ağ geçitleri** yapılandırma bölmesinde, bırakın hello **onay kutusunu** (Tıklatılmamış) devre dışı **Connect ağ geçidi üzerinden**.
   
   * Tür için değer **bağlantı adı**. Örneğin, `HISDEMO2`.
   * Tür için değer **DB2 sunucu adı**, adres veya diğer iki nokta üst üste bağlantı noktası numarası hello biçiminde. Örneğin, `HISDEMO2.cloudapp.net:50000`.
   * Tür için değer **DB2 veritabanı adı**. Örneğin, `NWIND`.
   * Tür için değer **kullanıcıadı**. Örneğin, `db2admin`.
   * Tür için değer **parola**. Örneğin, `Password1`.
9. Seçin **oluşturma** toocontinue.
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
11. İsteğe bağlı olarak, seçin **Gelişmiş Seçenekleri Göster** toospecify sorgu seçenekleri.
12. **Kaydet**’i seçin. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. Merhaba, **Db2getRows** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
14. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; satır listesini içermelidir.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>INSERT kullanarak bir satır Ekle
Bir DB2 tablosunda bir mantıksal uygulama eylem tooadd bir satır tanımlayabilirsiniz. Bu eylemin hello bağlayıcı tooprocess bir DB2 INSERT deyimi gibi bildirir `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `Db2insertRow`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın **db2** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **DB2 - Satır Ekle (Önizleme)**.
6. Merhaba, **DB2 - Satır Ekle (Önizleme)** eylem, select **değiştirmek bağlantı**. 
7. Merhaba, **bağlantıları** yapılandırma bölmesinde, bir bağlantı seçin. Örneğin, seçin **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
9. Gerekli tüm sütunlar (kırmızı yıldız bakın) için değerleri girin. Örneğin, `99999` için **AREAID**, türü `Area 99999`ve türü `102` için **REGİONID**. 
10. **Kaydet**’i seçin.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. Merhaba, **Db2insertRow** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
12. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; hello yeni satır içermelidir.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>SELECT kullanarak bir satır getirme
Bir DB2 tablosunda bir mantıksal uygulama eylem toofetch bir satır tanımlayabilirsiniz. Bu eylemin hello bağlayıcı tooprocess bir DB2 yeri seçin deyimi gibi bildirir `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı** (örn. "**Db2getRow**"), **abonelik**, **kaynak grubu**, **konumu**, ve **App Service planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi. 
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın **db2** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **DB2 - Get satırları (Önizleme)**.
6. Merhaba, **alma satırları (Önizleme)** eylem, select **değiştirmek bağlantı**. 
7. Merhaba, **bağlantıları** yapılandırmaları bölmesinde, varolan bir bağlantı seçin. Örneğin, seçin **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
9. Gerekli tüm sütunlar (kırmızı yıldız bakın) için değerleri girin. Örneğin, `99999` için **AREAID**. 
10. İsteğe bağlı olarak, seçin **Gelişmiş Seçenekleri Göster** toospecify sorgu seçenekleri.
11. **Kaydet**’i seçin. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. Merhaba, **Db2getRow** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
13. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; satır içermelidir.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Bir satır güncelleştirme kullanarak değiştirme
Bir DB2 tablosunda bir mantıksal uygulama eylem toochange bir satır tanımlayabilirsiniz. Bu eylemin hello bağlayıcı tooprocess DB2 güncelleştirme deyimi gibi bildirir `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `Db2updateRow`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın **db2** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **DB2 - güncelleştirme satır (Önizleme)**.
6. Merhaba, **DB2 - güncelleştirme satır (Önizleme)** eylem, select **değiştirmek bağlantı**. 
7. Merhaba, **bağlantıları** yapılandırmaları bölmesinde, select tooselect mevcut bir bağlantı. Örneğin, seçin **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
9. Gerekli tüm sütunlar (kırmızı yıldız bakın) için değerleri girin. Örneğin, `99999` için **AREAID**, türü `Updated 99999`ve türü `102` için **REGİONID**. 
10. **Kaydet**’i seçin. 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. Merhaba, **Db2updateRow** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
12. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; hello yeni satır içermelidir.
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>DELETE kullanma bir satırı Kaldır
Bir DB2 tablosunda bir mantıksal uygulama eylem tooremove bir satır tanımlayabilirsiniz. Bu eylemin hello bağlayıcı tooprocess bir DB2 DELETE deyimi gibi bildirir `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `Db2deleteRow`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi. 
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde **db2** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **DB2 - Satır Sil (Önizleme)**.
6. Merhaba, **DB2 - Satır Sil (Önizleme)** eylem, select **değiştirmek bağlantı**. 
7. Merhaba, **bağlantıları** yapılandırmaları bölmesinde, varolan bir bağlantı seçin. Örneğin, seçin **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
9. Gerekli tüm sütunlar (kırmızı yıldız bakın) için değerleri girin. Örneğin, `99999` için **AREAID**. 
10. **Kaydet**’i seçin. 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. Merhaba, **Db2deleteRow** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
12. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; hello silinen satır içermelidir.
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>Desteklenen DB2 platformları ve sürümleri
Bu bağlayıcı IBM DB2 platformları ve sürümlerinin yanı sıra, dağıtılmış ilişkisel veritabanı mimarisi (DRDA) SQL Erişim Yöneticisi (SQLAM) sürüm 10 ve 11 desteği IBM DB2 uyumlu ürünler (örneğin IBM Bluemix dashDB) aşağıdaki hello destekler:

* IBM DB2 z/OS 11.1 için
* IBM DB2 z/OS 10.1 için
* IBM DB2 için i 7.3
* IBM DB2 için i 7.2
* IBM DB2 için i 7.1
* IBM DB2 LUW 11
* IBM DB2 LUW 10.5 için

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/db2/). 

## <a name="next-steps"></a>Sonraki adımlar
[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

