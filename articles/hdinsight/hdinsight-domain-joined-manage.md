---
title: "aaaManage etki alanına katılmış Hdınsight kümeleri - Azure | Microsoft Docs"
description: "Nasıl toomanage etki alanına katılmış Hdınsight kümeleri öğrenin"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>Etki alanına katılmış Hdınsight kümeleri (Önizleme) yönetme
Merhaba kullanıcılar ve etki alanına katılmış ve nasıl toomanage etki alanına katılmış Hdınsight kümeleri hello roller öğrenin.

## <a name="users-of-domain-joined-hdinsight-clusters"></a>Kullanıcıları etki alanına katılmış Hdınsight kümeleri
Merhaba küme oluşturma sırasında oluşturulan iki kullanıcı hesapları olmayan etki alanına katılmış bir Hdınsight kümesi vardır:

* **Ambari yönetici**: Bu hesap olarak da bilinen, *Hadoop kullanıcı* veya *HTTP kullanıcı*. Bu hesap https:// adresindeki tooAmbari üzerinde kullanılan toolog olabilir&lt;clustername >. azurehdinsight.net. Bu da kullanılan toorun sorgu Ambari görünümleri, harici araçlar (yani PowerShell, Templeton, Visual Studio) aracılığıyla işleri yürütmek ve hello Hive ODBC sürücüsü ve BI Araçları (yani Excel, Powerbı veya Tableau) ile kimlik doğrulaması.
* **SSH kullanıcı**: Bu hesap ile SSH kullanılabilir ve sudo komutları yürütün. Kök ayrıcalıkları toohello Linux VM'ler sahiptir.

Bir etki alanına katılmış Hdınsight kümesi üç yeni kullanıcı eklenmesi tooAmbari yönetici ve SSH kullanıcı sahiptir.

* **Bırakabilmenizi yönetici**: Bu hesap hello yerel Apache bırakabilmenizi yönetici hesabıdır. Bir active directory etki alanı kullanıcısı değil. Bu hesap, kullanılan toosetup ilkelerine ve diğer kullanıcıların yöneticileri veya temsilci olarak atanan Yöneticiler (kullanıcılarla ilkeleri yönetebilmeniz için) hale getirebilirsiniz. Varsayılan olarak, hello kullanıcı adınızdır *yönetici* ve hello parola Ambari yönetici parolası hello aynı hello değil. Merhaba parola hello Ayarları sayfasından bırakabilmenizi güncelleştirilebilir.
* **Küme Yöneticisi etki alanı kullanıcısı**: Hadoop küme yönetim Ambari ve bırakabilmenizi gibi hello olarak atanmış bir active directory etki alanı kullanıcısı bu hesabıdır. Küme oluşturma sırasında bu kullanıcının kimlik bilgilerini sağlamanız gerekir. Bu kullanıcı ayrıcalıkları aşağıdaki hello sahiptir:

  * Makineler toohello etki alanına katılma ve hello küme oluşturma sırasında belirttiğiniz OU içinde yerleştirin.
  * Hizmet sorumluları hello küme oluşturma sırasında belirttiğiniz OU içinde oluşturun.
  * Geriye doğru DNS girdilerini oluşturun.

    Not hello diğer AD kullanıcılar da bu ayrıcalıklarına sahiptir.

    Bırakabilmenizi tarafından yönetilmeyen ve bu nedenle güvenli olmayan bazı bitiş noktalarını hello küme (örneğin, Templeton) içinde vardır. Bu uç noktaları, hello küme yönetici etki alanı kullanıcısı dışındaki tüm kullanıcılar için kilitlendiğini.
* **Normal**: küme oluşturma sırasında birden çok active directory grupları sağlayabilir. Bu gruplardaki kullanıcıların Hello eşitlenen tooRanger ve Ambari olacaktır. Bu kullanıcılar etki alanı kullanıcıları ve erişim tooonly bırakabilmenizi yönetilen uç noktaları (örneğin, Hiveserver2) sahip olacaktır. Tüm RBAC ilkeleri hello ve denetim geçerli toothese kullanıcılar olacaktır.

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>Etki alanına katılmış Hdınsight kümeleri rolleri
Etki alanına katılmış Hdınsight rolleri aşağıdaki hello vardır:

* Küme Yöneticisi
* Küme işleci
* Hizmet Yöneticisi
* Hizmet işleci
* Küme kullanıcı

**Bu rolleri toosee hello izinleri**

1. Merhaba ambarı Yönetimi kullanıcı arabirimini açın.  Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).
2. Merhaba sol menüden **rolleri**.
3. Merhaba mavi soru işareti toosee hello izinler'i tıklatın:

    ![Etki alanına katılmış Hdınsight rolleri izinleri](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>Açık hello ambarı Yönetimi Arabirimi
1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Hdınsight kümenize bir dikey pencerede açın. Bkz: [listesi ve Göster kümeleri](hdinsight-administer-use-management-portal.md#list-and-show-clusters).
3. Tıklatın **Pano** hello üst menü tooopen Ambari gelen.
4. Üzerinde tooAmbari Hello Küme Yöneticisi etki alanı kullanıcı adı ve parola kullanarak oturum açın.
5. Merhaba tıklatın **yönetici** hello sağ üst köşedeki ve ardından açılır menüsünden **yönetmek Ambari**.

    ![Etki alanına katılmış Hdınsight Ambari yönetme](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    Merhaba UI şuna benzer:

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>Active Directory'nizden eşitlenen hello etki alanı kullanıcıları listele
1. Merhaba ambarı Yönetimi kullanıcı arabirimini açın.  Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).
2. Merhaba sol menüden **kullanıcılar**. Active Directory toohello Hdınsight kümenizden eşitlenen tüm hello kullanıcılar göreceksiniz.

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi kullanıcıları listele](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>Active Directory'nizden eşitlenen hello etki alanı grupları listesi
1. Merhaba ambarı Yönetimi kullanıcı arabirimini açın.  Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).
2. Merhaba sol menüden **grupları**. Active Directory toohello Hdınsight kümenizden eşitlenen tüm hello grupları göreceksiniz.

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi listesi grupları](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>Hive görünümleri izinlerini yapılandırma
1. Merhaba ambarı Yönetimi kullanıcı arabirimini açın.  Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).
2. Merhaba sol menüden **görünümleri**.
3. Tıklatın **HIVE** tooshow hello ayrıntıları.

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi Hive görünümleri](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. Merhaba tıklatın **Hive görünümü** tooconfigure Hive görünümleri bağlantı.
5. Toohello aşağı **izinleri** bölümü.

    ![Etki alanına katılmış Hdınsight ambarı Yönetimi UI Hive görünümleri izinleri yapılandırma](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. Tıklatın **Kullanıcı Ekle** veya **Grup Ekle**ve ardından hello kullanıcılar veya Hive görünümleri grupları belirtin.

## <a name="configure-users-for-hello-roles"></a>Kullanıcılar hello rolleri için yapılandırma
 toosee roller ve onların izinlerini listesini görmek [rolleri, etki alanına katılmış Hdınsight kümeleri](#roles-of-domain---joined-hdinsight-clusters).

1. Merhaba ambarı Yönetimi kullanıcı arabirimini açın.  Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).
2. Merhaba sol menüden **rolleri**.
3. Tıklatın **Kullanıcı Ekle** veya **Grup Ekle** tooassign kullanıcılar ve gruplar toodifferent rolleri.

## <a name="next-steps"></a>Sonraki adımlar
* Etki alanına katılmış HDInsight kümesini yapılandırmak için bkz. [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md).
* Hive ilkelerini yapılandırmak ve Hive sorgularını çalıştırmak için bkz. [Etki alanına katılmış HDInsight kümeleri için Hive ilkelerini yapılandırma](hdinsight-domain-joined-run-hive.md).
* Etki alanına katılmış Hdınsight kümelerinde SSH kullanarak Hive sorguları çalıştırmak için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
