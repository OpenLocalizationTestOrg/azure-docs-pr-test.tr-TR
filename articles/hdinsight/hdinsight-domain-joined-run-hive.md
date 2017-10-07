---
title: "Etki alanına katılmış Hdınsight - Azure aaaConfigure Hive ilkelerinde | Microsoft Docs"
description: "Öğrenin ...."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>Etki alanına katılmış HDInsight’ta (Önizleme) Hive ilkelerini yapılandırma
Bilgi nasıl Hive için tooconfigure Apache bırakabilmenizi ilkeleri. Bu makalede, iki bırakabilmenizi ilkeleri toorestrict erişim toohello hivesampletable oluşturun. Merhaba hivesampletable Hdınsight kümeleri ile birlikte gelir. Merhaba ilkeleri yapılandırdıktan sonra Excel ve ODBC sürücüsü tooconnect tooHive tablolarını Hdınsight'ta kullanın.

## <a name="prerequisites"></a>Ön koşullar
* Etki alanına katılmış HDInsight kümesi. Bkz. [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md).
* Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013’ün tek başına sürümü veya Office 2010 Professional Plus yüklü iş istasyonu.

## <a name="connect-tooapache-ranger-admin-ui"></a>TooApache bırakabilmenizi yönetici UI Bağlan
**tooconnect tooRanger yönetim kullanıcı Arabirimi**

1. Tarayıcıdan tooRanger yönetici UI bağlayın. Merhaba URL'dir https://&lt;ClusterName >.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > Ranger’ın kimlik bilgileri Hadoop kümesinin kimlik bilgilerinden farklıdır. önbelleğe alınan Hadoop kimlik bilgilerini kullanarak tooprevent tarayıcılar yeni InPrivate tarayıcı penceresini tooconnect toohello bırakabilmenizi yönetici kullanıcı arabirimini kullanın.
   >
   >
2. Merhaba Küme Yöneticisi etki alanı kullanıcı adı ve parola kullanarak oturum açın:

    ![HDInsight etki alanına katılmış Ranger ana sayfası](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    Ranger şu an için yalnızca Yarn ve Hive ile birlikte çalışmaktadır.

## <a name="create-domain-users"></a>Etki alanı kullanıcılarını oluşturma
[Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) bölümünde hiveruser1 ve hiveuser2 kullanıcılarını oluşturmuştunuz. Bu öğreticide hello iki kullanıcı hesabını kullanır.

## <a name="create-ranger-policies"></a>Ranger ilkelerini oluşturma
Bu bölümde hivesampletable erişimi için iki Ranger ilkesi oluşturacaksınız. Farklı sütun kümelerine select izni vereceksiniz. İki kullanıcı da [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) bölümünde oluşturulmuştur.  Merhaba sonraki bölümde hello iki ilke Excel'de test edeceğiz.

**toocreate bırakabilmenizi ilkeleri**

1. Ranger Yönetici Arabirimini açın. Bkz: [tooApache bırakabilmenizi yönetici UI bağlanmak](#connect-to-apache-ranager-admin-ui).
2. ****Hive**’ın altındaki &lt;KümeAdı>_hive** öğesine tıklayın. Önceden yapılandırılmış iki ilke göreceksiniz.
3. Tıklatın **yeni ilke Ekle**ve değerlerini aşağıdaki hello girin:

   * Policy name: read-hivesampletable-all
   * Hive Database: default
   * table: hivesampletable
   * Hive column: *
   * Select User: hiveuser1
   * Permissions: select

     ![HDInsight etki alanına katılmış Ranger Hive ilkesi yapılandırma](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Bir etki alanı kullanıcısı Kullanıcı Seç doldurulmazsa bırakabilmenizi toosync aad'ye için birkaç dakika bekleyin.
     >
     >
4. Tıklatın **Ekle** toosave hello ilkesi.
5. Merhaba son iki adımı toocreate hello aşağıdaki özelliklere başka bir ilke Yinele:

   * Policy name: read-hivesampletable-devicemake
   * Hive Database: default
   * table: hivesampletable
   * Hive column: clientid, devicemake
   * Select User: hiveuser2
   * Permissions: select

## <a name="create-hive-odbc-data-source"></a>Hive ODBC veri kaynağı oluşturma
Merhaba yönergeleri bulunabilir [oluşturma Hive ODBC veri kaynağını](hdinsight-connect-excel-hive-odbc-driver.md).  

    Özellik|Açıklama
    ---|---
    Data Source Name|Bir ad tooyour veri kaynağı verin
    Host|&lt;HDInsightKümesiAdı>.azurehdinsight.net yazın. Örnek: HDIKumesi.azurehdinsight.net
    Bağlantı noktası|<strong>443</strong> yazın. (Bu bağlantı noktasına 563 too443 değiştirildi.)
    Database|<strong>Default</strong>’u kullanın.
    Hive Server Type|<strong>Hive Server 2</strong>’yi seçin
    Mechanism|<strong>Azure HDInsight Service</strong>’i seçin
    HTTP Path|Boş bırakın.
    User Name|Girin hiveuser1@contoso158.onmicrosoft.com. Farklı ise hello etki alanı adını güncelleştirin.
    Parola|Merhaba parola için hiveuser1 girin.
    </table>

Emin tooclick olun **Test** hello veri kaynağı kaydetmeden önce.

## <a name="import-data-into-excel-from-hdinsight"></a>HDInsight’tan Excel’e veri aktarma
Merhaba son bölümünde iki ilke yapılandırdınız.  hiveuser1 hello tüm hello sütunlarda izni seçin, ve iki sütun izninin seçin hello hiveuser2 sahiptir. Bu bölümde, hello iki kullanıcı tooimport verileri Excel'e taklit.

1. Excel’de yeni veya mevcut bir çalışma kitabını açın.
2. Merhaba gelen **veri** sekmesini tıklatın, **diğer veri kaynaklardan**ve ardından **Veri Bağlantı Sihirbazı'ndan** toolaunch hello **Veri Bağlantı Sihirbazı'nı**.

    ![Veri bağlantı sihirbazını açın][img-hdi-simbahiveodbc.excel.dataconnection]
3. Seçin **ODBC DSN** hello veri kaynağı ve ardından olarak **sonraki**.
4. ODBC veri kaynaklarından select hello veri kaynağı hello önceki adımda oluşturduğunuz adı ve ardından **sonraki**.
5. Başlangıç Sihirbazı'nda hello küme Hello parolayı yeniden girin ve ardından **Tamam**. Merhaba bekleyin **veritabanı ve Tablo Seç** iletişim tooopen. Bu işlem birkaç saniye sürebilir.
6. **hivesampletable**’ı seçip **İleri**’ye tıklayın.
7. **Son**'a tıklayın.
8. Merhaba, **Veri Al** iletişim kutusunda, değiştirmek veya hello sorgusunu belirtin. Bu nedenle, toodo'ı tıklatın **özellikleri**. Bu işlem birkaç saniye sürebilir.
9. Merhaba tıklatın **tanımı** sekmesini hello komut metni:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Tanımladığınız hello bırakabilmenizi ilkeleri tarafından hiveuser1 tüm hello sütunlarda select izni vardır.  Bu nedenle bu sorgu hiveuser1 kullanıcısının kimlik bilgileriyle çalışır ancak hiveuser2 kullanıcısının kimlik bilgileriyle çalışmaz.

   ![Bağlantı Özellikleri][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Tıklatın **Tamam** tooclose hello bağlantı özellikleri iletişim kutusu.
11. Tıklatın **Tamam** tooclose hello **Veri Al** iletişim.  
12. Hiveuser1 Hello parolasını yeniden girin ve ardından **Tamam**. Veri içe aktarılan tooExcel büyümeden birkaç saniye sürer. İşlem tamamlandığında 11 veri sütunu göreceksiniz.

Merhaba son bölümünde oluşturduğunuz tootest hello ikinci ilke (okuma hivesampletable devicemake)

1. Excel'de yeni bir sayfa ekleyin.
2. Merhaba son yordamı tooimport hello verileri izleyin.  vereceğiniz hello yalnızca hiveuser1'ın yerine toouse hiveuser2'in kimlik bilgilerini değişikliktir. Bu hiveuser2 yalnızca izni toosee iki sütun olduğu için başarısız olur. Aşağıdaki hata hello alın:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. İzleme hello aynı yordamı tooimport veri. Bu süre, hiveuser2'in kimlik bilgilerini kullanın ve ayrıca hello select deyiminden değiştirin:

        SELECT * FROM "HIVE"."default"."hivesampletable"

    yerine şunu yazın:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    İşlem tamamlandığında iki veri sütununun içe aktarıldığını göreceksiniz.

## <a name="next-steps"></a>Sonraki adımlar
* Etki alanına katılmış HDInsight kümesini yapılandırmak için bkz. [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md).
* Etki alanına katılmış HDInsight kümesini yönetmek için bkz. [Etki alanına katılmış HDInsight kümelerini yönetme](hdinsight-domain-joined-manage.md).
* Etki alanına katılmış Hdınsight kümelerinde SSH kullanarak Hive sorguları çalıştırmak için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Bağlanma JDBC Hive kullanarak Hive için bkz: [tooHive hello Hive JDBC sürücüsü kullanarak Azure hdınsight'ta Bağlan](hdinsight-connect-hive-jdbc-driver.md)
* Hive ODBC kullanarak bağlanan Excel tooHadoop için bkz: [hello Microsoft Hive ODBC sürücüsü ile bağlanma Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)
* Power Query kullanarak bağlanan Excel tooHadoop için bkz: [Power Query kullanarak bağlanmak Excel tooHadoop](hdinsight-connect-excel-power-query.md)
