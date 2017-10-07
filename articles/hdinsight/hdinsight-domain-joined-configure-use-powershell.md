---
title: "PowerShell - Azure kullanarak etki alanına katılmış Hdınsight kümelerini aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl tooset ayarlama ve Azure PowerShell kullanarak etki alanına katılmış Hdınsight kümelerini yapılandırma"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>Azure PowerShell kullanarak etki alanına katılmış Hdınsight kümeleri (Önizleme) yapılandırma
Nasıl bir Azure Hdınsight yukarı tooset küme Azure Active Directory (Azure AD) ile bilgi edinin ve [Apache bırakabilmenizi](http://hortonworks.com/apache/ranger/) Azure PowerShell kullanarak. Bir Azure PowerShell Betiği toomake hello yapılandırma daha hızlı ve daha az hataya sağlanır. Etki alanına katılmış Hdınsight yalnızca Linux tabanlı kümelerde yapılandırılabilir. Daha fazla bilgi için bkz: [tanıtmak etki alanına katılmış Hdınsight kümeleri](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> Oozie etki alanına katılmış Hdınsight üzerinde etkin değil.

Tipik bir etki alanına katılmış Hdınsight küme yapılandırması hello aşağıdaki adımları içerir:

1. Azure AD için Azure klasik bir VNet oluşturun.  
2. Oluşturun ve Azure AD ve Azure AD DS yapılandırın.
3. VM toohello eklemek kuruluş birimi oluşturmak için Klasik VNet. 
4. Azure AD DS için bir kuruluş birimi oluşturun.
5. Bir Hdınsight VNet hello Azure kaynak yönetimi modunda oluşturun.
6. Geriye doğru DNS bölgeleri hello Azure AD DS için ayarlayın.
7. Eş iki Vnet hello.
8. Hdınsight kümesi oluşturun.

Merhaba sağlanan PowerShell komut dosyasını 3 ile 7 arasındaki adımları gerçekleştirir. 1 ve 2. adım el ile gitmeniz gerekir.  Toouse Azure PowerShell tercih ederseniz, bkz. [yapılandırma etki alanına katılmış Hdınsight kümeleri](hdinsight-domain-joined-configure.md). 

Merhaba son topoloji örneği şu şekilde görünür:

![Etki alanına katılmış Hdınsight topolojisi](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Şu anda Azure AD Klasik sanal ağlar (Vnet'ler) yalnızca destekler ve yalnızca destek Linux tabanlı Hdınsight kümeleri için Azure Resource Manager tabanlı sanal ağlar, iki sanal ağlar ve bunlar arasında eşleme Hdınsight Azure AD tümleştirme gerektirir. Merhaba karşılaştırma için hello iki dağıtım modelleri arasında bilgi [Azure Resource Manager ve klasik dağıtım: dağıtım modellerini anlama ve hello kaynaklarınızın durumunu](../azure-resource-manager/resource-manager-deployment-model.md). iki Vnet hello olmalıdır hello hello Azure AD DS aynı bölgede.

> [!NOTE]
> Bu öğretici, Azure AD olmadığını varsayar. Varsa, 2. adımda hello bölümüne atlayabilirsiniz.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticide öğeleri toogo aşağıdaki hello sahip olmanız gerekir:

* İle öğrenmeniz [Azure AD etki alanı Hizmetleri](https://azure.microsoft.com/services/active-directory-ds/) kendi [fiyatlandırma](https://azure.microsoft.com/pricing/details/active-directory-ds/) yapısı.
* Aboneliğiniz bu genel Önizleme için Güvenilenler listesine olduğundan emin olun. Bir e-posta göndererek yapabilirsiniz toohdipreview@microsoft.com abonelik kimliğinizi içeren
* Etki alanınız için imzalama yetkilisi tarafından imzalanmış bir SSL sertifikası. Güvenli LDAP yapılandırarak Hello sertifika gereklidir. Otomatik olarak imzalanan sertifikalar kullanılamaz.
* Azure PowerShell.  Bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>Azure AD için Azure klasik bir VNet oluşturun.
Merhaba yönergeler için bkz: [burada](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic).

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>Oluşturun ve Azure AD ve Azure AD DS yapılandırın.
Merhaba yönergeler için bkz: [burada](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).

## <a name="run-hello-powershell-script"></a>Merhaba PowerShell betiğini çalıştırın
Merhaba PowerShell Betiği adresinden yüklenebilir [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight). Merhaba zip dosyasını ayıklayın ve hello dosyaları yerel olarak kaydedin.

**tooedit hello PowerShell Betiği**

1. Windows PowerShell ISE veya herhangi bir metin düzenleyicisi kullanarak run.ps1 açın.
2. Değişkenleri aşağıdaki hello Hello değerlerini doldurun:
   
   * **$SubscriptionName** – hello hello Hdınsight kümenize toocreate istediğiniz Azure aboneliği adı. Bu abonelikte Klasik sanal ağda zaten oluşturmuş ve abonelik altında hello Hdınsight kümesi için bir Azure Resource Manager sanal ağ oluşturma.
   * **$ClassicVNetName** -hello Azure AD DS içeren hello Klasik sanal ağı. Bu sanal ağ hello olmalıdır, yukarıda verilen aynı abonelik. Bu sanal ağ hello Azure portal kullanarak ve klasik portal kullanmayan oluşturulması gerekir. Merhaba yönergesinde izlerseniz [yapılandırma etki alanına katılmış Hdınsight kümeleri (Önizleme)](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic), hello varsayılan addır contosoaadvnet.
   * **$ClassicResourceGroupName** – yukarıda belirtilen hello Klasik sanal ağı için hello Resource Manager grup adı. Örneğin contosoaadrg. 
   * **$ArmResourceGroupName** – hello kaynak grubu adı, içinde toocreate hello Hdınsight kümesi istiyor. Merhaba kullanabilirsiniz $ArmResourceGroupName aynı kaynak grubunda.  Merhaba kaynak grubu mevcut değilse hello betik hello kaynak grubu oluşturur.
   * **$ArmVNetName** -toocreate hello Hdınsight kümesi içinde istediğiniz hello Resource Manager sanal ağ adı. Bu sanal ağ $ArmResourceGroupName yerleştirilecek.  Merhaba PowerShell Betiği Hello VNet yoksa oluşturur. Mevcut değilse, yukarıdaki sağladığınız hello kaynak grubunun parçası olmalıdır.
   * **$AddressVnetAddressSpace** – hello ağ hello Resource Manager sanal ağın adres alanı. Bu adres alanı kullanılabilir olduğundan emin olun. Bu adres alanı hello Klasik sanal ağın adres alanı çakışamaz. Örneğin, "10.1.0.0/16"
   * **$ArmVnetSubnetName** -tooplace hello Hdınsight kümesi VM'ler içinde istediğiniz hello Resource Manager sanal ağ alt ağ adı. Merhaba PowerShell Betiği Hello alt ağ yoksa oluşturur. Mevcut değilse, yukarıdaki sağladığınız hello sanal ağın parçası olması gerekir.
   * **$AddressSubnetAddressSpace** – hello ağ hello Resource Manager sanal ağ alt ağ için adres aralığı. Bu alt ağ adres aralığından hello Hdınsight kümesi VM IP adresleri olacaktır. Örneğin, "10.1.0.0/24".
   * **$ActiveDirectoryDomainName** – toojoin hello Hdınsight istediğiniz hello Azure AD etki alanı adı için sanal makineleri küme. Örneğin, "contoso.onmicrosoft.com"
   * **$ClusterUsersGroups** – toosync toohello Hdınsight kümesi istediğiniz AD hello güvenlik gruplarındaki hello ortak adı. Merhaba kullanıcılar bu güvenlik grubundaki kullanıcıların active directory etki alanı kimlik bilgilerini kullanarak toohello küme Panoda mümkün toolog olacaktır. Bu güvenlik gruplarını hello active Directory'de mevcut olması gerekir. Örneğin, "hiveusers" veya "clusteroperatorusers".
   * **$OrganizationalUnitName** -hello etki alanında, hangi içinde tooplace hello Hdınsight küme VM'ler istediğiniz ve hello küme tarafından kullanılan hizmet asıl adı hello hello kuruluş birimi. henüz yoksa hello PowerShell Betiği Bu OU oluşturursunuz. Örneğin, "HDInsightOU".
3. Merhaba değişiklikleri kaydedin.

**toorun hello komut dosyası**

1. Çalıştırma **Windows PowerShell** yönetici olarak.
2. Run.ps1 toohello klasörüne göz atın. 
3. Merhaba dosya adını yazarak Hello komut dosyasını çalıştırın ve isabet **ENTER**.  Oturum açma 3 iletişim açılır:
   
   1. **TooAzure Klasik Portalı'nda oturum** – kullandığınız kimlik bilgilerinizi girmeniz toosign tooAzure Klasik Portalı'nda. Hello Azure AD ve Azure AD DS'yi bu kimlik bilgilerini kullanarak oluşturmuş olmanız gerekir.
   2. **TooAzure Resource Manager Portalı'nda oturum** – kullandığınız kimlik bilgilerinizi girmeniz toosign tooAzure Resource Manager Portalı'nda.
   3. **Etki alanı kullanıcı adı** – toobe hello Hdınsight kümesinde bir yönetim istediğiniz hello etki alanı kullanıcı adı hello kimlik bilgilerini girin. Azure AD sıfırdan oluşturduysanız bu belgelerini kullanarak bu kullanıcı oluşturmuş olmanız gerekir. 
      
      > [!IMPORTANT]
      > Merhaba kullanıcı adı şu biçimde girin: 
      > 
      > EtkiAlanıAdı\KullanıcıAdı (örneğin contoso.onmicrosoft.com\clusteradmin)
      > 
      > 
      
      Bu kullanıcı 3 ayrıcalıklarına sahip olmalıdır: toojoin makineler toohello sağlanan Active Directory etki alanı; Kuruluş birimi toocreate hizmet asıl adı ve makine nesneleri hello içinde sağlanan; ve tooadd geriye doğru DNS proxy kuralları.

Oluşturma geriye doğru DNS bölgeleri, hello betik ister sırada tooenter ağ kimliği. Bu ağ kimliği hello Resource Manager sanal ağın adres ön eki olmalıdır. Resource Manager sanal ağ alt ağ adresi alanınızı 10.2.0.0/24 ise, hello aracı hello ağ kimliği için istediğinde 10.2.0.0/24 Örneğin 

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
     * **Sürüm**: Hadoop 2.7.3 (HDI 3.5). Etki alanına katılmış Hdınsight yalnızca Hdınsight kümesi sürüm 3.5 desteklenir.
     * **Küme türü**: PREMIUM
       
       Tıklatın **seçin** toosave hello değişiklikleri.
   * **Kimlik bilgileri**: hello küme kullanıcı ve hello SSH kullanıcı için hello kimlik bilgilerini yapılandırın.
   * **Veri kaynağı**: yeni bir depolama hesabı oluşturun veya varolan bir depolama hesabını hello Hdınsight kümesi için varsayılan depolama hesabı hello olarak kullanın. Başlangıç konumu gerekir olması hello iki Vnet hello gibi aynı.  Merhaba konumu da hello hello Hdınsight kümesinin konumdur.
   * **Fiyatlandırma**: hello kümenizin çalışan düğümü sayısını seçin.
   * **Yapılandırmaları Gelişmiş**: 
     
     * **Etki alanına katılma & sanal/alt**: 
       
       * **Etki alanı ayarları**: 
         
         * **Etki alanı adı**: contoso.onmicrosoft.com
         * **Etki alanı kullanıcı adı**: bir etki alanı kullanıcı adı girin. Bu etki alanında ayrıcalıkları aşağıdaki hello olmalıdır: katılma makineler toohello etki alanı ve bunları daha önce; yapılandırdığınız hello kuruluş birimine yerleştirin Hizmet sorumluları içinde daha önce yapılandırılmış hello kuruluş birimi oluşturun; Geriye doğru DNS girdilerini oluşturun. Bu etki alanı kullanıcısı bu etki alanına katılmış Hdınsight kümesinin Merhaba yönetici olur.
         * **Etki alanı parolası**: hello etki alanı kullanıcı parolası girin.
         * **Kuruluş birimi**: hello daha önce yapılandırılmış OU hello ayırt edici adını girin. Örneğin: OU HDInsightOU, DC = contoso, DC = onmicrosoft, DC = com =
         * **LDAPS URL**: ldaps://contoso.onmicrosoft.com:636
         * **Access kullanıcı grubuna**: kullanıcılar, wan hello güvenlik grubu belirtmeniz toosync toohello küme. Örneğin, HiveUsers.
           
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
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
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
   * **Küme Users grubunun D Ns**: "\"CN HiveUsers, OU = AADDC kullanıcılar, DC = =<DomainName>, DC onmicrosoft, DC = com =\""
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (Merhaba etki alanı yönetici kullanıcı adını girin)
   * **DomainAdminPassword**: (Merhaba etki alanı yönetici kullanıcı parolasını girin)
   * **Toohello hüküm ve koşullar yukarıda belirtildiği kabul**: (denetleyin)
   * **PIN toodashboard**: (denetleyin)
3. **Satın al**’a tıklayın. **Şablon Dağıtımı’nı dağıtma** başlıklı yeni bir kutucuk görürsünüz. Bir küme hakkında toocreate yaklaşık 20 dakika sürer. Merhaba Küme oluşturulduktan sonra hello küme dikey penceresinde hello portal tooopen tıklatabilirsiniz.

Merhaba öğreticiyi tamamladıktan sonra toodelete hello küme isteyebilirsiniz. HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz. Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir. Merhaba ücretleri hello küme için hello ücretleri depolama birkaç katı olduğundan, bunlar kullanımda olmadığında ekonomik toodelete kümeleri mantıklıdır. Bir küme silme hello yönergeler için bkz: [kullanarak yönetmek Hadoop kümeleri hdınsight'ta Azure portalına hello](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Sonraki adımlar

* Hive ilkelerini yapılandırmak ve Hive sorgularını çalıştırmak için bkz. [Etki alanına katılmış HDInsight kümeleri için Hive ilkelerini yapılandırma](hdinsight-domain-joined-run-hive.md).
* SSH tooconnect tooDomain katılmış Hdınsight kümeleri için bkz [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

