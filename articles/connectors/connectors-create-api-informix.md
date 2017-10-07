---
title: "Mantıksal uygulamalarınızı aaaAdd hello Informix Bağlayıcısı | Microsoft Docs"
description: "REST API parametrelerle Informix bağlayıcı genel bakış"
services: 
documentationcenter: 
author: gplarsen
manager: anneta
editor: 
tags: connectors
ms.assetid: ca2393f0-3073-4dc2-8438-747f5bc59689
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: 7a163e2ebf00fa3109b93e34845d922c2174a48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-informix-connector"></a>Merhaba Informix Bağlayıcısı ile çalışmaya başlama
Informix için Microsoft Bağlayıcısı bir IBM Informix veritabanında depolanan Logic Apps tooresources bağlanır. Merhaba Informix bağlayıcı bir TCP/IP ağı üzerinden bir Microsoft istemci toocommunicate tooremote Informix sunucu bilgisayarları içerir. Bu Windows Azure sanallaştırma çalıştıran için IBM Informix gibi bulut veritabanlarını içerir ve şirket içi hello şirket içi veri ağ geçidi kullanarak veritabanlarını. Merhaba bkz [liste desteklenen](connectors-create-api-informix.md#supported-informix-platforms-and-versions) IBM Informix platformları ve sürümleri (Bu konudaki).

Merhaba Bağlayıcısı veritabanı işlemleri aşağıdaki hello destekler:

* Liste veritabanı tabloları
* SELECT kullanarak bir satır okuma
* Tüm satırları seçin kullanarak okuyun
* INSERT kullanarak bir satır Ekle
* Alter bir satır güncelleştirme kullanma
* DELETE kullanma bir satırı Kaldır

Bu konu, nasıl bir mantıksal uygulama tooprocess toouse hello Bağlayıcısı veritabanı işlemleri gösterir.

Logic Apps hakkında daha fazla toolearn bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Kullanılabilir eylemler
Bu bağlayıcı mantıksal uygulama eylemleri aşağıdaki hello destekler:

* Getables
* GetRow
* GetRows
* Insertrow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Listede tablolar
Merhaba Microsoft Azure portalı üzerinden gerçekleştirilen birçok adımlar herhangi bir işlem için bir mantıksal uygulama oluşturma oluşur.

Merhaba mantıksal uygulama içinde bir Informix veritabanına bir eylem toolist tablolar ekleyebilirsiniz. Bu eylemin hello bağlayıcı tooprocess Informix schema deyiminin gibi bildirir `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `InformixgetTables`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**.  
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın **Informix** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **Informix - Get tabloları (Önizleme)**.
   
   ![](./media/connectors-create-api-informix/InformixconnectorActions.png)  
6. Merhaba, **Informix - Get tablolar** yapılandırma bölmesinde, **onay kutusunu** tooenable **Connect şirket içi veri ağ geçidi üzerinden**. Bulut tooon içi hello ayarlarını değiştirme dikkat edin.
   
   * Tür için değer **Server**, adres veya diğer iki nokta üst üste bağlantı noktası numarası hello biçiminde. Örneğin, `ibmserver01:9089`.
   * Tür için değer **veritabanı**. Örneğin, `nwind`.
   * İçin değer seçin **kimlik doğrulama**. Örneğin, seçin **temel**.
   * Tür için değer **kullanıcıadı**. Örneğin, `informix`.
   * Tür için değer **parola**. Örneğin, `Password1`.
   * İçin değer seçin **ağ geçidi**. Örneğin, seçin **datagateway01**.
7. Seçin **oluşturma**ve ardından **kaydetmek**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)
8. Merhaba, **InformixgetTables** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
9. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_tables**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; tabloların bir listesini içermelidir.
   
   ![](./media/connectors-create-api-informix/InformixconnectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Merhaba bağlantıları oluşturma
Bu bağlayıcı içi toodatabase bağlantılarını destekler ve hello bulutta kullanarak hello bağlantı özelliklerini aşağıdaki. 

| Özellik | Açıklama |
| --- | --- |
| sunucu |Gereklidir. TCP/IP adresi veya IPv4 veya IPv6 biçiminde, ardından (iki nokta üst üste TCP/IP bağlantı noktası numarası ile ayrılmış) diğer temsil eden bir dize değeri kabul eder. |
| Veritabanı |Gereklidir. Bir DRDA ilişkisel veritabanı adı (RDBNAM) temsil eden bir dize değeri kabul eder. Informix 128 bayt dizesi kabul eder (veritabanı bir IBM Informix veritabanı adı (dbname) olarak bilinir). |
| Kimlik doğrulaması |İsteğe bağlı. Bir liste öğesi değeri, temel veya Windows (kerberos) kabul eder. |
| kullanıcı adı |Gereklidir. Bir dize değeri kabul eder. |
| password |Gereklidir. Bir dize değeri kabul eder. |
| Ağ geçidi |Gereklidir. Merhaba depolama grubu içinde Hello şirket içi veri tanımlı ağ geçidi tooLogic uygulamaları temsil eden bir liste öğesi değeri kabul eder. |

## <a name="create-hello-on-premises-gateway-connection"></a>Merhaba şirket içi ağ geçidi bağlantısı oluşturma
Bu bağlayıcı hello şirket içi veri ağ geçidi kullanarak şirket içi Informix veritabanına erişebilir. Daha fazla bilgi için ağ geçidi konularına bakın. 

1. Merhaba, **ağ geçitleri** yapılandırma bölmesinde, **onay kutusunu** tooenable **Connect ağ geçidi üzerinden**. Bulut tooon içi ayarlarını değiştirme hello bakın.
2. Tür için değer **Server**, adres veya diğer iki nokta üst üste bağlantı noktası numarası hello biçiminde. Örneğin, `ibmserver01:9089`.
3. Tür için değer **veritabanı**. Örneğin, `nwind`.
4. İçin değer seçin **kimlik doğrulama**. Örneğin, seçin **temel**.
5. Tür için değer **kullanıcıadı**. Örneğin, `informix`.
6. Tür için değer **parola**. Örneğin, `Password1`.
7. İçin değer seçin **ağ geçidi**. Örneğin, seçin **datagateway01**.
8. Seçin **oluşturma** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Merhaba bulut bağlantı oluşturma
Bu bağlayıcı bir bulut Informix veritabanına erişebilir. 

1. Merhaba, **ağ geçitleri** yapılandırma bölmesinde, bırakın hello **onay kutusunu** (Tıklatılmamış) devre dışı **Connect ağ geçidi üzerinden**. 
2. Tür için değer **bağlantı adı**. Örneğin, `hisdemo2`.
3. Tür için değer **Informix sunucu adı**, adres veya diğer iki nokta üst üste bağlantı noktası numarası hello biçiminde. Örneğin, `hisdemo2.cloudapp.net:9089`.
4. Tür için değer **Informix veritabanı adı**. Örneğin, `nwind`.
5. Tür için değer **kullanıcıadı**. Örneğin, `informix`.
6. Tür için değer **parola**. Örneğin, `Password1`.
7. Seçin **oluşturma** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Tüm satırları seçin kullanarak getirme
Merhaba Informix tabloda tüm satırların mantığı uygulama eylem toofetch oluşturabilirsiniz. Bu eylemin hello bağlayıcı tooprocess bir Informix SELECT deyimi gibi bildirir `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı** (örn. "**InformixgetRows**"), **abonelik**, **kaynak grubu**, **konumu**, ve **App Service planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın **Informix** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **Informix - Get satırları (Önizleme)** .
6. Merhaba, **alma satırları (Önizleme)** eylem, select **değiştirmek bağlantı**.
7. Merhaba, **bağlantıları** yapılandırma bölmesinde, **Yeni Oluştur**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorNewConnection.png)
8. Merhaba, **ağ geçitleri** yapılandırma bölmesinde, bırakın hello **onay kutusunu** (Tıklatılmamış) devre dışı **Connect ağ geçidi üzerinden**.
   
   * Tür için değer **bağlantı adı**. Örneğin, `HISDEMO2`.
   * Tür için değer **Informix sunucu adı**, adres veya diğer iki nokta üst üste bağlantı noktası numarası hello biçiminde. Örneğin, `HISDEMO2.cloudapp.net:9089`.
   * Tür için değer **Informix veritabanı adı**. Örneğin, `NWIND`.
   * Tür için değer **kullanıcıadı**. Örneğin, `informix`.
   * Tür için değer **parola**. Örneğin, `Password1`.
9. Seçin **oluşturma** toocontinue.
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)
10. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
11. İsteğe bağlı olarak, seçin **Gelişmiş Seçenekleri Göster** toospecify sorgu seçenekleri.
12. **Kaydet**’i seçin. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsTableName.png)
13. Merhaba, **InformixgetRows** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
14. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; satır listesini içermelidir.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>INSERT kullanarak bir satır Ekle
Bir Informix tabloda bir mantıksal uygulama eylem tooadd bir satır oluşturabilirsiniz. Bu eylemin hello bağlayıcı tooprocess bir Informix INSERT deyimi gibi bildirir `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `InformixinsertRow`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın **Informix** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **Informix - Satır Ekle (Önizleme)**.
6. Merhaba, **alma satırları (Önizleme)** eylem, select **değiştirmek bağlantı**. 
7. Merhaba, **bağlantıları** yapılandırma bölmesinde, bir bağlantı seçin tooselect. Örneğin, seçin **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
9. Gerekli tüm sütunlar (kırmızı yıldız bakın) için değerleri girin. Örneğin, `99999` için **AREAID**, türü `Area 99999`ve türü `102` için **REGİONID**. 
10. **Kaydet**’i seçin.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowValues.png)
11. Merhaba, **InformixinsertRow** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
12. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; hello yeni satır içermelidir.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>SELECT kullanarak bir satır getirme
Bir Informix tabloda bir mantıksal uygulama eylem toofetch bir satır oluşturabilirsiniz. Bu eylemin hello bağlayıcı tooprocess bir Informix yeri seçin deyimi gibi bildirir `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `InformixgetRow`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın **Informix** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **Informix - Get satırları (Önizleme)** .
6. Merhaba, **alma satırları (Önizleme)** eylem, select **değiştirmek bağlantı**. 
7. Merhaba, **bağlantıları** yapılandırmaları bölmesinde, select tooselect mevcut bir bağlantı. Örneğin, seçin **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
9. Gerekli tüm sütunlar (kırmızı yıldız bakın) için değerleri girin. Örneğin, `99999` için **AREAID**. 
10. İsteğe bağlı olarak, seçin **Gelişmiş Seçenekleri Göster** toospecify sorgu seçenekleri.
11. **Kaydet**’i seçin. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowValues.png)
12. Merhaba, **InformixgetRow** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
13. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; satır içermelidir.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Bir satır güncelleştirme kullanarak değiştirme
Bir Informix tabloda bir mantıksal uygulama eylem toochange bir satır oluşturabilirsiniz. Bu eylemin hello bağlayıcı tooprocess bir Informix güncelleştirme deyimi gibi bildirir `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `InformixupdateRow`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın **Informix** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **Informix - güncelleştirme satır (Önizleme)**.
6. Merhaba, **alma satırları (Önizleme)** eylem, select **değiştirmek bağlantı**. 
7. Merhaba, **bağlantıları** yapılandırmaları bölmesinde, select tooselect mevcut bir bağlantı. Örneğin, seçin **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
9. Gerekli tüm sütunlar (kırmızı yıldız bakın) için değerleri girin. Örneğin, `99999` için **AREAID**, türü `Updated 99999`ve türü `102` için **REGİONID**. 
10. **Kaydet**’i seçin. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowValues.png)
11. Merhaba, **InformixupdateRow** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
12. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; hello yeni satır içermelidir.
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>DELETE kullanma bir satırı Kaldır
Bir Informix tabloda bir mantıksal uygulama eylem tooremove bir satır oluşturabilirsiniz. Bu eylemin hello bağlayıcı tooprocess bir Informix DELETE deyimi gibi bildirir `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma
1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.
2. Merhaba girin **adı**, gibi `InformixdeleteRow`, **abonelik**, **kaynak grubu**, **konumu**, ve **uygulama Hizmet planı**. Seçin **PIN toodashboard**ve ardından **oluşturma**.

### <a name="add-a-trigger-and-action"></a>Bir tetikleyici ve Eylem Ekle
1. Merhaba, **Logic Apps Tasarımcısı**seçin **boş LogicApp** hello içinde **şablonları** listesi.
2. Merhaba, **Tetikleyicileri** listesinde **yineleme**. 
3. Merhaba, **yineleme** tetikleyici, select **Düzenle**seçin **sıklığı** açılan tooselect **gün**ve ardından  **Aralığı** tootype **7**. 
4. Select hello **+ yeni adım** kutusuna ve ardından **Eylem Ekle**.
5. Merhaba, **Eylemler** listesinde, yazın **Informix** hello içinde **diğer eylemler için arama** düzenleme kutusuna ve ardından **Informix - Satır Sil (Önizleme)**.
6. Merhaba, **alma satırları (Önizleme)** eylem, select **değiştirmek bağlantı**. 
7. Merhaba, **bağlantıları** yapılandırmaları bölmesinde, varolan bir bağlantı seçin. Örneğin, seçin **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Merhaba, **tablo adı** listesi, select hello **aşağı ok**ve ardından **alanı**.
9. Gerekli tüm sütunlar (kırmızı yıldız bakın) için değerleri girin. Örneğin, `99999` için **AREAID**. 
10. **Kaydet**’i seçin. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowValues.png)
11. Merhaba, **InformixdeleteRow** hello içinde dikey **tüm çalışır** altında listesinde **Özet**, select hello ilk listelenen öğesi (en son Çalıştır).
12. Merhaba, **çalıştırmak mantıksal uygulama** dikey penceresinde, select **çalıştırma ayrıntıları**. Merhaba içinde **eylem** listesinde **Get_rows**. Merhaba değeri bkz **durum**, gereken **başarılı**. Select hello **girişleri bağlantı** tooview hello girişleri. Select hello **çıkışları bağlantı**ve görünüm hello çıkarır; hello silinen satır içermelidir.
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowOutputs.png)

## <a name="supported-informix-platforms-and-versions"></a>Desteklenen Informix platformları ve sürümleri
Bu bağlayıcı yapılandırıldığında IBM Informix sürümleri aşağıdaki hello destekler toosupport dağıtılmış ilişkisel veritabanı mimarisi (DRDA) istemci bağlantıları.

* IBM Informix 12,1
* IBM Informix 11.7

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/informix/). 

## <a name="next-steps"></a>Sonraki adımlar
[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

