---
title: "aaaConfigure etki alanına katılmış Hdınsight kümeleri - Azure | Microsoft Docs"
description: "Bilgi nasıl tooset ayarlama ve etki alanına katılmış Hdınsight kümeleri yapılandırma"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 8c4b3d269a7662d27a49b839e5cd05a3e24f7023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>Etki alanına katılmış Hdınsight kümeleri (Önizleme) yapılandırma

Nasıl bir Azure Hdınsight yukarı tooset küme Azure Active Directory (Azure AD) ile bilgi edinin ve [Apache bırakabilmenizi](http://hortonworks.com/apache/ranger/) tootake avantajlarından güçlü kimlik doğrulaması ve zengin rol tabanlı erişim denetimi (RBAC) ilkeleri.  Etki alanına katılmış Hdınsight yalnızca Linux tabanlı kümelerde yapılandırılabilir. Daha fazla bilgi için bkz: [tanıtmak etki alanına katılmış Hdınsight kümeleri](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> Oozie etki alanına katılmış Hdınsight üzerinde etkin değil.

Bu makalede, bir dizinin ilk öğreticide hello şöyledir:

* Hdınsight küme bağlı tooAzure AD (aracılığıyla hello Azure Directory etki alanı Hizmetleri yeteneği) Apache bırakabilmenizi etkin oluşturun.
* Oluşturmak ve Apache bırakabilmenizi aracılığıyla Hive ilkeleri uygulamak ve tooconnect tooHive ODBC tabanlı araçlar, örneğin Excel, Tableau vb. kullanarak, kullanıcıların (örneğin, veri bilimcilerine) sağlar. Microsoft, HBase, Spark ve Storm, Hdınsight tooDomain katılmış gibi diğer iş yüklerinin en kısa sürede ekleme üzerinde çalışmaktadır.

Merhaba son topoloji örneği şu şekilde görünür:

![Etki alanına katılmış Hdınsight topolojisi](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Şu anda Azure AD Klasik sanal ağlar (Vnet'ler) yalnızca destekler ve yalnızca destek Linux tabanlı Hdınsight kümeleri için Azure Resource Manager tabanlı sanal ağlar, iki sanal ağlar ve bunlar arasında eşleme Hdınsight Azure AD tümleştirme gerektirir. Merhaba karşılaştırma için hello iki dağıtım modelleri arasında bilgi [Azure Resource Manager ve klasik dağıtım: dağıtım modellerini anlama ve hello kaynaklarınızın durumunu](../azure-resource-manager/resource-manager-deployment-model.md). iki Vnet hello olmalıdır hello hello Azure AD DS aynı bölgede.

Azure hizmet adları benzersiz olmalıdır. Bu öğreticide adlarından hello kullanılır. Contoso adlı kurgusal bir addır. Değiştirmeniz gereken *contoso* hello öğreticide olduğunuzda farklı bir ada sahip. 

**Adları:**

| Özellik | Değer |
| --- | --- |
| Azure AD VNet |contosoaadvnet |
| Azure AD Vnet kaynak grubu |contosoaadrg |
| Azure AD dizini |contosoaaddirectory |
| Azure AD etki alanı adı |contoso (contoso.onmicrosoft.com) |
| Hdınsight VNet |contosohdivnet |
| Hdınsight VNet kaynak grubu |contosohdirg |
| Hdınsight kümesi |contosohdicluster |

Bu öğretici, bir etki alanına katılmış Hdınsight kümesi yapılandırmak için hello adımları sağlar. Her bölümde bağlantılar tooother makaleleri ile ilgili daha fazla bilgi bulunur.

## <a name="prerequisite"></a>Önkoşul:
* İle öğrenmeniz [Azure AD etki alanı Hizmetleri](https://azure.microsoft.com/services/active-directory-ds/) kendi [fiyatlandırma](https://azure.microsoft.com/pricing/details/active-directory-ds/) yapısı.
* Aboneliğiniz bu genel Önizleme için Güvenilenler listesine olduğundan emin olun. Bir e-posta göndererek yapabilirsiniz toohdipreview@microsoft.com abonelik kimliğinizi içeren
* Etki alanınız için imzalama yetkilisi tarafından imzalanmış bir SSL sertifikası. Güvenli LDAP yapılandırarak Hello sertifika gereklidir. Otomatik olarak imzalanan sertifikalar kullanılamaz.

## <a name="procedures"></a>Yordamları
1. Azure AD için Azure klasik bir VNet oluşturun.  
2. Oluşturun ve Azure AD ve Azure AD DS yapılandırın.
3. Bir Hdınsight VNet hello Azure kaynak yönetimi modunda oluşturun.
4. Eş iki Vnet hello.
5. Hdınsight kümesi oluşturun.

> [!NOTE]
> Bu öğretici, Azure AD olmadığını varsayar. Varsa, 2. adımda hello bölümüne atlayabilirsiniz.
> 
> 

3. adım adım 7 aracılığıyla otomatikleştiren bir PowerShell komut dosyası yok.  Daha fazla bilgi için bkz: [yapılandırma etki alanına katılmış Hdınsight kümeleri kullanan Azure PowerShell](hdinsight-domain-joined-configure-use-powershell.md).

## <a name="create-an-azure-virtual-network-classic"></a>Bir Azure sanal ağ (Klasik) oluşturun
Bu bölümde, hello Azure portal kullanarak sanal ağ (Klasik) oluşturun. Merhaba sonraki bölümde, Azure AD hello sanal ağ için hello Azure AD DS etkinleştirin. Aşağıdaki yordamı ve diğer sanal ağ oluşturma yöntemlerini kullanarak hello hakkında daha fazla bilgi için bkz: [hello Azure portal kullanarak bir sanal ağ (Klasik) oluşturmak](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

**toocreate klasik bir VNet**

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com). 
2. Tıklatın **yeni** > **ağ** > **sanal ağ**.
3. İçinde **dağıtım modeli seçin**seçin **Klasik**ve ardından **oluşturma**.
4. Girin veya değerleri aşağıdaki hello seçin:
   
   * **Ad**: contosoaadvnet
   * **Adres alanı**: 10.1.0.0/16
   * **Alt ağ adı**: Subnet1
   * **Alt ağ adres aralığı**: 10.1.0.0/24
   * **Abonelik**: (Bu VNet oluşturmak için kullanılan bir abonelik seçin.)
   * **Kaynak grubu**: contosoaadrg
   * **Konum**: (Hdınsight kümeniz için bir bölge seçin.)
     
     > [!IMPORTANT]
     > Azure AD DS destekleyen bir konum seçmeniz gerekir. Daha fazla bilgi için bkz. [Bölgelere göre kullanılabilir ürünler](https://azure.microsoft.com/en-us/regions/services/). 
     > 
     > Her ikisi de klasik VNet hello ve hello kaynak grubu VNet hello olmalıdır hello Azure AD DS aynı bölgede.
     > 
     > 
5. Tıklatın **oluşturma** toocreate hello VNet.

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>Oluşturma ve Azure AD için Azure AD DS yapılandırma
Bu bölümde şunları yapacaksınız:

1. Azure AD oluşturun.
2. Azure AD kullanıcıları oluşturun. Bu etki alanı kullanıcıyı görürsünüz. Merhaba ilk kullanıcı hello Azure AD ile Merhaba Hdınsight kümesi yapılandırmak için kullanın.  Merhaba iki diğer kullanıcıların Bu öğretici için isteğe bağlıdır. İçinde kullanılacak [etki alanına katılmış Hdınsight kümeleri için ilkeler yapılandırma Hive](hdinsight-domain-joined-run-hive.md) Apache bırakabilmenizi ilkeleri yapılandırırken.
3. Merhaba AAD DC Yöneticiler grubu oluşturun ve hello Azure AD kullanıcı toohello grubuna ekleyin. Bu kullanıcı toocreate hello kuruluş birimi kullanın.
4. Hello Azure AD için Azure AD etki alanı Hizmetleri (Azure AD DS) etkinleştirin.
5. LDAPS hello Azure AD için yapılandırın. Merhaba Basit Dizin Erişim Protokolü (LDAP) gelen kullanılan tooread olduğu ve tooAzure AD yazın.

Var olan Azure AD bir toouse tercih ederseniz, 1 ve 2. adımları atlayabilirsiniz.

**Azure AD bir toocreate**

1. Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **yeni** > **uygulama hizmetleri** > **Active Directory**  >  **Directory** > **özel Oluştur**. 
2. Girin veya değerleri aşağıdaki hello seçin:
   
   * **Ad**: contosoaaddirectory
   * **Etki alanı adı**: contoso.  Bu ad genel olarak benzersiz olmalıdır.
   * **Ülke veya bölge**: ülkenizi veya bölgenizi seçin.
3. **Tamamla**’ya tıklayın.

**Bir Azure AD kullanıcı oluşturun**

1. Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **Active Directory** -> **contosoaaddirectory**. 
2. Tıklatın **kullanıcılar** hello üst menüsünde.
3. Tıklatın **kullanıcı ekleme**.
4. Girin **kullanıcı adı**ve ardından **sonraki**. 
5. Kullanıcı profili yapılandırın; İçinde **rol**seçin **genel yönetici**; ve ardından **sonraki**.  Merhaba genel yönetici rolü gerekli toocreate kuruluş birimleri kullanılır.
6. Tıklatın **oluşturma** tooget geçici bir parola.
7. Merhaba parola bir kopyasını alın ve ardından **tam**. Bu öğreticide daha sonra bu genel yönetici kullanıcı toocreate hello Hdınsight kümesi kullanır.

İzleme ile Merhaba iki daha fazla kullanıcı aynı yordamı toocreate hello **kullanıcı** rol, hiveuser1 ve hiveuser2. Merhaba şu kullanıcılar kullanılacak [etki alanına katılmış Hdınsight kümeleri için yapılandırma Hive ilkeleri](hdinsight-domain-joined-run-hive.md).

**toocreate AAD DC Administrators grubunun hello ve bir Azure AD kullanıcı ekleyin**

1. Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **Active Directory** > **contosoaaddirectory**. 
2. Tıklatın **grupları** hello üst menüsünde.
3. Tıklatın **grup ekleme** veya **grubu eklemek**.
4. Girin veya değerleri aşağıdaki hello seçin:
   
   * **Ad**: AAD DC yöneticileri.  Merhaba grup adı değişmez.
   * **Grup türü**: güvenlik.
5. **Tamamla**’ya tıklayın.
6. Tıklatın **AAD DC Yöneticiler** tooopen hello grubu.
7. Tıklatın **üye eklemek**.
8. Merhaba önceki adımda oluşturduğunuz hello ilk kullanıcıyı seçin ve ardından **tam**.
9. Yineleme hello aynı adımları toocreate başka bir grup olarak adlandırılan **HiveUsers**, ve hello iki Hive kullanıcılar toohello grubunu ekleyin.

Daha fazla bilgi için bkz: [Azure AD etki alanı Hizmetleri (Önizleme) - 'AAD DC Yöneticiler' hello oluşturma grup](../active-directory-domain-services/active-directory-ds-getting-started.md).

**Azure AD için Azure AD DS tooenable**

1. Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **Active Directory** > **contosoaaddirectory**. 
2. Tıklatın **yapılandırma** hello üst menüsünde.
3. Çok ilerleyin**etki alanı Hizmetleri**, ve kümesi hello aşağıdaki değerler:
   
   * **Bu dizin için etki alanı Hizmetleri'ni etkinleştirme**: Evet.
   * **DNS etki alanı adı, etki alanı Hizmetleri'nin**: Bu hello Azure directory hello varsayılan DNS adını gösterir. Örneğin, contoso.onmicrosoft.com.
   * **Etki Alanı Hizmetleri toothis sanal ağa bağlanmak**: seçin, daha önce oluşturduğunuz Klasik sanal ağı hello yani **contosoaadvnet**.
4. Tıklatın **kaydetmek** hello sayfasının hello Alttan. Göreceğiniz **bekleniyor...**  sonraki çok**bu dizin için etki alanı Hizmetleri'ni etkinleştirme**.  
5. Bekle **bekleniyor...**  kaybolur, ve **IP adresi** doldurulmuş. İki IP adresi doldurulacak. Bunlar hello IP hello etki alanı denetleyicilerinin etki alanı Hizmetleri tarafından sağlanan adresleridir. Merhaba karşılık gelen etki alanı denetleyicisi sağlanan ve hazır olduktan sonra her IP adresi görünür. Merhaba iki IP adresi yazın. Bunları daha sonra ihtiyacınız olacak.

Daha fazla bilgi için bkz: [Azure AD etki alanı Hizmetleri (Önizleme) - Azure AD etki alanı Etkinleştirme Hizmetleri](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md).

**toosynchronize parola**

Kendi etki alanı kullanıyorsanız, toosynchronize hello parola gerekir. Bkz: [etkinleştirmek parola eşitleme tooAzure AD etki alanı Hizmetleri salt bulut Azure AD dizini](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md).

**tooconfigure LDAPS hello Azure AD için**

1. Etki alanınız için imzalama yetkilisi tarafından imzalanmış bir SSL sertifikası alın. Kendinden imzalı bir sertifika toouse istiyorsanız, lütfen ulaşmak toohdipreview@microsoft.com için bir özel durum.
2. Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **Active Directory** > **contosoaaddirectory**. 
3. Tıklatın **yapılandırma** hello üst menüsünde.
4. Çok kaydırma**etki alanı Hizmetleri**.
5. Tıklatın **yapılandırma sertifika**.
6. Merhaba yönerge toospecify hello sertifika dosyasını ve hello parola izleyin. Göreceğiniz **bekleniyor...**  sonraki çok**bu dizin için etki alanı Hizmetleri'ni etkinleştirme**.  
7. Bekle **bekleniyor...**  kaybolur, ve **güvenli LDAP sertifikası** doldurulmuş.  Bu, 10 dakika veya daha fazla alabilir.

> [!NOTE]
> Azure AD DS hello üzerinde bazı arka plan görevleri çalıştırmak, sertifikası karşıya yükleniyor - çalışırken bir hata görebilirsiniz <i>bu Kiracı için gerçekleştirilen bir işlem yoktur. Lütfen daha sonra yeniden deneyin</i>.  Lütfen bu hatanın oluştuğu durumda süre sonra yeniden deneyin. Merhaba, ikinci etki alanı denetleyicisi IP sağlanan too3 saatleri toobe sürebilir.
> 
> 

Daha fazla bilgi için bkz: [yapılandırma güvenli LDAP (LDAPS) bir Azure AD etki alanı Hizmetleri yönetilen etki alanı](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md).

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>Hdınsight kümesi için Resource Manager Vnet'i oluşturma
Bu bölümde, hello Hdınsight kümesi için kullanılan bir Azure Resource Manager Vnet'i oluşturur. Azure başka yöntemler kullanarak VNET oluşturma hakkında daha fazla bilgi için bkz: [bir sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)

Merhaba VNet oluşturduktan sonra Resource Manager Vnet'i toouse hello hello Azure AD VNet için aynı DNS sunucuları olarak hello yapılandırır. Bu öğretici toocreate hello adımları izlediyseniz Klasik VNet ve hello Azure AD hello hello DNS sunucuları: 10.1.0.4 ve 10.1.0.5.

**Resource Manager Vnet'i toocreate**

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **yeni**, **ağ**ve ardından **sanal ağ**. 
3. İçinde **dağıtım modeli seçin**seçin **Resource Manager**ve ardından **oluşturma**.
4. Değerleri aşağıdaki hello seçin veya yazın:
   
   * **Ad**: contosohdivnet
   * **Adres alanı**: 10.2.0.0/16. Başlangıç adresi aralığı başlangıç IP adresi aralığı hello ile örtüşemez emin olun Klasik VNet.
   * **Alt ağ adı**: Subnet1
   * **Alt ağ adres aralığı**: 10.2.0.0/24
   * **Abonelik**: (Azure aboneliğinizi seçin.)
   * **Kaynak grubu**: contosohdirg
   * **Konum**: (seçin hello aynı konuma Azure AD VNet, yani contosoaadvnet hello gibi.)
5. **Oluştur**'a tıklayın.

**Merhaba Resource Manager Vnet'i için DNS tooconfigure**

1. Merhaba gelen [Azure portal](https://portal.azure.com), tıklatın **daha fazla hizmet** -> **sanal ağlar**. Değil tooclick olun **sanal ağları (Klasik)**.
2. Tıklatın **contosohdivnet**.
3. Tıklatın **DNS sunucuları** yan hello yeni dikey pencerenin sol hello gelen.
4. Tıklatın **özel**ve değerlerini aşağıdaki hello girin:
   
   * 10.1.0.4
   * 10.1.0.5
     
     Bu DNS sunucusu IP adreslerini toohello DNS sunucularının hello Azure AD VNet (Klasik VNet) eşleşmesi gerekir.
5. **Kaydet** düğmesine tıklayın.

## <a name="peer-hello-azure-ad-vnet-and-hello-hdinsight-vnet"></a>Hello Azure AD VNet eş ve Hdınsight VNet hello
**toopeer hello iki sanal ağ**

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **daha fazla hizmet** hello sol menüden.
3. Tıklatın **sanal ağlar**. Tıklamayın **sanal ağları (Klasik)**.
4. Tıklatın **contosohdivnet**.  Merhaba Hdınsight VNet budur.
5. Tıklatın **eşlemeler** hello dikey pencerenin sol hello menüsünde.
6. Tıklatın **Ekle** hello üst menüsünde. Merhaba açılır **eklemek eşliği** dikey.
7. Merhaba üzerinde **Ekle eşliği** dikey penceresinde, aşağıdaki değerleri ayarlayın veya select hello:
   
   * **Ad**: ContosoAADHDIVNetPeering
   * **Sanal ağ dağıtım modeli**: Klasik
   * **Abonelik**: hello (Azure AD) Klasik vnet için kullanılan, abonelik adını seçin.
   * **Sanal ağ**: contosoaadvnet.
   * **Sanal ağ erişimine izin ver**: (denetleyin)
   * **İletilen trafiğe izin**: (denetleyin). Merhaba, diğer iki onay işaretini kaldırın.
8. **Tamam** düğmesine tıklayın.

## <a name="create-hdinsight-cluster"></a>Hdınsight kümesi oluşturma
Bu bölümde, her iki hello Azure portal kullanarak hdınsight'ta Linux tabanlı Hadoop kümesi oluşturun veya [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md). Diğer küme oluşturma yöntemleri ve hello ayarlarını anlama, bkz: [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md). Hdınsight'ta Resource Manager şablonu toocreate Hadoop kullanma hakkında daha fazla bilgi kümeleri için bkz: [Resource Manager şablonları kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**kullanarak bir etki alanına katılmış Hdınsight küme toocreate hello Azure portalı**

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **yeni**, **Intelligence + analiz**ve ardından **Hdınsight**.
3. Merhaba gelen **yeni Hdınsight kümesi** dikey penceresinde girin veya seçin değerleri aşağıdaki hello:
   
   * **Küme adı**: hello etki alanına katılmış Hdınsight kümesi için yeni bir küme adı girin.
   * **Abonelik**: Bu küme oluşturmak için kullanılan Azure aboneliğini seçin.
   * **Küme Yapılandırması**:
     
     * **Küme türü**: Hadoop. Etki alanına katılmış Hdınsight şu anda yalnızca üzerinde desteklenen Hadoop kümeleri değil.
     * **İşletim sistemi**: Linux.  Etki alanına katılmış Hdınsight yalnızca Linux tabanlı Hdınsight kümelerinde desteklenir.
     * **Sürüm**: HDI 3.6. Etki alanına katılmış Hdınsight yalnızca Hdınsight kümesi sürüm 3.6 desteklenir.
     * **Küme türü**: PREMIUM
       
       Tıklatın **seçin** toosave hello değişiklikleri.
   * **Kimlik bilgileri**: hello küme kullanıcı ve hello SSH kullanıcı için hello kimlik bilgilerini yapılandırın.
   * **Veri kaynağı**: yeni bir depolama hesabı oluşturun veya varolan bir depolama hesabını hello Hdınsight kümesi için varsayılan depolama hesabı hello olarak kullanın. Başlangıç konumu gerekir olması hello iki Vnet hello gibi aynı.  Merhaba konumu da hello hello Hdınsight kümesinin konumdur.
   * **Fiyatlandırma**: hello kümenizin çalışan düğümü sayısını seçin.
   * **Yapılandırmaları Gelişmiş**: 
     
     * **Etki alanına katılma & sanal/alt**: 
       
       * **Etki alanı ayarları**: 
         
         * **Etki alanı adı**: contoso.onmicrosoft.com
         * **Etki alanı kullanıcı adı**: bir etki alanı kullanıcı adı girin. Bu etki alanında ayrıcalıkları aşağıdaki hello olmalıdır: makineler toohello etki alanına katılma ve küme oluşturma sırasında; belirttiğiniz hello kuruluş birimine yerleştirin Küme oluşturma sırasında belirttiğiniz hello kuruluş birimi içinde hizmet sorumluları oluşturmak; Geriye doğru DNS girdilerini oluşturun. Bu etki alanı kullanıcısı bu etki alanına katılmış Hdınsight kümesinin Merhaba yönetici olur.
         * **Etki alanı parolası**: hello etki alanı kullanıcı parolası girin.
         * **Kuruluş birimi**: Merhaba toouse Hdınsight kümesi ile istediğiniz OU hello ayırt edici adını girin. Örneğin: OU HDInsightOU, DC = contoso, DC = onmicrosoft, DC = com. Bu OU mevcut değilse, Hdınsight kümesi bu OU toocreate dener. Merhaba OU zaten var veya hello etki alanı hesabı izinleri toocreate yeni bir tane emin olun. AADDC Yöneticiler parçası olan hello etki alanı hesabı kullanırsanız, gerekli izinlere sahip toocreate hello OU.
         * **LDAPS URL**: ldaps://contoso.onmicrosoft.com:636
         * **Access kullanıcı grubuna**: hello güvenlik grubu, kullanıcıları belirtmek toosync toohello küme istiyor. Örneğin, HiveUsers.
           
           Tıklatın **seçin** toosave hello değişiklikleri.
           
           ![Etki alanına katılmış Hdınsight portal etki alanı ayarını yapılandırın](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **Sanal ağ**: contosohdivnet
       * **Alt ağ**: Subnet1
         
         Tıklatın **seçin** toosave hello değişiklikleri.        
         Tıklatın **seçin** toosave hello değişiklikleri.
   * **Kaynak grubu**: Select hello kaynak grubu hello Hdınsight VNet (contosohdirg) için kullanılır.
4. **Oluştur**'a tıklayın.  

Etki alanına katılmış Hdınsight kümesi oluşturmak için başka bir seçenek toouse Azure kaynak yönetimi şablonudur. Aşağıdaki yordamı hello şunların nasıl yapıldığını gösterir:

**toocreate kaynak yönetimi şablonunu kullanarak bir etki alanına katılmış Hdınsight kümesi**

1. Görüntü tooopen hello Azure portalında bir Resource Manager şablonu aşağıdaki hello'ı tıklatın. Merhaba Resource Manager şablonu bir ortak blob kapsayıcısında bulunur. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Merhaba gelen **parametreleri** dikey penceresinde hello aşağıdaki değerleri girin:
   
   * **Abonelik**: (Azure aboneliğinizi seçin).
   * **Kaynak grubu**: tıklatın **var olanı kullan**ve hello belirtin şimdiye aynı kaynak grubu.  Örneğin contosohdirg. 
   * **Konum**: bir kaynak grubu konumu belirtin.
   * **Küme adı**: oluşturacağınız hello Hadoop kümesi için bir ad girin. Örneğin contosohdicluster.
   * **Küme türü**: bir küme türü seçin.  Merhaba varsayılan değer **hadoop**.
   * **Konum**: hello kümesi için bir konum seçin.  Merhaba varsayılan depolama hesabını kullanan aynı konuma hello.
   * **Çalışan düğüm sayısı küme**: hello çalışan düğümü sayısını seçin.
   * **Küme oturum açma adı ve parola**: hello varsayılan oturum açma adı **yönetici**.
   * **SSH kullanıcı adı ve parola**: hello varsayılan kullanıcı adı **sshuser**.  Bunu yeniden adlandırabilirsiniz. 
   * **Sanal ağ kimliği**: /subscriptions/&lt;Abonelikkimliği > /resourceGroups/&lt;ResourceGroupName > /providers/Microsoft.Network/virtualNetworks/&lt;vnetname adlı >
   * **Sanal ağ alt**: /subscriptions/&lt;Abonelikkimliği > /resourceGroups/&lt;ResourceGroupName > /providers/Microsoft.Network/virtualNetworks/&lt;vnetname adlı >/alt ağlar/Subnet1
   * **Etki alanı adı**: contoso.onmicrosoft.com
   * **Kuruluş birimi DN**: OU HDInsightOU, DC = contoso, DC = onmicrosoft, DC = com =
   * **Küme Users grubunun DNs**: [\"HiveUsers\"]
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (Merhaba etki alanı yönetici kullanıcı adını girin)
   * **DomainAdminPassword**: (Merhaba etki alanı yönetici kullanıcı parolasını girin)
   * **Toohello hüküm ve koşullar yukarıda belirtildiği kabul**: (denetleyin)
   * **PIN toodashboard**: (denetleyin)
3. **Satın al**’a tıklayın. **Şablon Dağıtımı’nı dağıtma** başlıklı yeni bir kutucuk görürsünüz. Bir küme hakkında toocreate yaklaşık 20 dakika sürer. Merhaba Küme oluşturulduktan sonra hello küme dikey penceresinde hello portal tooopen tıklatabilirsiniz.

Merhaba öğreticiyi tamamladıktan sonra toodelete hello küme isteyebilirsiniz. HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz. Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir. Merhaba ücretleri hello küme için hello ücretleri depolama birkaç katı olduğundan, bunlar kullanımda olmadığında ekonomik toodelete kümeleri mantıklıdır. Bir küme silme hello yönergeler için bkz: [kullanarak yönetmek Hadoop kümeleri hdınsight'ta Azure portalına hello](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Sonraki adımlar
* Hive ilkelerini yapılandırmak ve Hive sorgularını çalıştırmak için bkz. [Etki alanına katılmış HDInsight kümeleri için Hive ilkelerini yapılandırma](hdinsight-domain-joined-run-hive.md).
* SSH tooconnect tooDomain katılmış Hdınsight kümeleri için bkz [Linux, Unix veya OS X Hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

