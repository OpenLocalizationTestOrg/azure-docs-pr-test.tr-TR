---
title: "aaaSQL sunucu kullanılabilirlik grupları - Azure sanal makineleri - önkoşulları | Microsoft Docs"
description: "Bu öğretici, Azure Vm'lerinde SQL Server Always On kullanılabilirlik oluşturmak için tooconfigure hello Önkoşullar Grup nasıl gösterir."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: c492db4c-3faa-4645-849f-5a1a663be55a
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: eed0729ead25c7793bb17a04cd7fd996c7dc8c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-prerequisites-for-creating-always-on-availability-groups-on-azure-virtual-machines"></a>Azure sanal makinelerde Always On kullanılabilirlik grupları oluşturmak için tam hello önkoşulları

Bu öğretici nasıl toocomplete hello oluşturmak için Önkoşullar gösterir bir [SQL Server Always On kullanılabilirlik grubu Azure sanal makinelerde (VM'ler)](virtual-machines-windows-portal-sql-availability-group-tutorial.md). Bir etki alanı denetleyicisi, iki SQL Server Vm'lerinin ve bir Tanık hello Önkoşullar tamamladığınızda, tek bir kaynak grubu içinde vardır.

**Zaman tahmin**: toocomplete hello Önkoşullar birkaç saat sürebilir. Bu süre çoğunu sanal makinelerin oluşturulmasını harcanmaktadır.

Merhaba Aşağıdaki diyagramda hello öğreticide yapı gösterilmektedir.

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="review-availability-group-documentation"></a>Kullanılabilirlik grubu belgelerini gözden geçirin

Bu öğretici, SQL Server Always On kullanılabilirlik grupları temel bilgilere sahip olduğunuzu varsayar. Bu teknolojiyle bilmiyorsanız bkz [genel bakış, Always On kullanılabilirlik grupları (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).


## <a name="create-an-azure-account"></a>Bir Azure hesabı oluşturun
Bir Azure hesabınız olmalıdır. Yapabilecekleriniz [ücretsiz bir Azure hesabı açın](/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone Avantajlarınızı etkinleştirebilir](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
1. İçinde toohello oturum [Azure portal](http://portal.azure.com).
2. Tıklatın  **+**  toocreate hello portalında yeni bir nesne.

   ![Yeni nesne](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-portalplus.png)

3. Tür **kaynak grubu** hello içinde **Market** arama penceresi.

   ![Kaynak grubu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroupsymbol.png)
4. Tıklatın **kaynak grubu**.
5. **Oluştur**'a tıklayın.
6. Merhaba üzerinde **kaynak grubu** dikey altında **kaynak grubu adı**, hello kaynak grubu için bir ad yazın. Örneğin, **sql-ha-rg**.
7. Birden çok Azure aboneliğiniz varsa, hello abonelik hello toocreate hello kullanılabilirlik grubu istediğiniz Azure aboneliği olduğundan emin olun.
8. Bir konum seçin. Merhaba, hello toocreate hello kullanılabilirlik grubu Azure bölgesini konumdur. Bu öğretici için tüm kaynakları tek bir Azure konumda toobuild yapacağız.
9. Doğrulayın **PIN toodashboard** denetlenir. Bu isteğe bağlı ayar hello Azure portalı panosunun üzerinde hello kaynak grubu için bir kısayol yerleştirir.

   ![Kaynak grubu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroup.png)

10. Tıklatın **oluşturma** toocreate hello kaynak grubu.

Azure hello kaynak grubu ve PIN hello Portalı'nda bir kısayol toohello kaynak grubu oluşturur.

## <a name="create-hello-network-and-subnets"></a>Merhaba ağ ve alt ağlar oluşturun
Merhaba sonraki toocreate hello ağları ve alt ağlar hello Azure kaynak grubu içinde adımdır.

Merhaba çözüm iki alt ağa sahip bir sanal ağ kullanır. Merhaba [sanal ağa genel bakış](../../../virtual-network/virtual-networks-overview.md) Azure ağlar hakkında daha fazla bilgi sağlar.

toocreate hello sanal ağ:

1. Merhaba, kaynak grubundaki Azure portal'ı tıklatın **+ Ekle**. Azure açılır hello **her şeyi** dikey.

   ![Yeni öğe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/02-newiteminrg.png)
2. Arama **sanal ağ**.

     ![Arama sanal ağ](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/04-findvirtualnetwork.png)
3. Tıklatın **sanal ağ**.
4. Merhaba üzerinde **sanal ağ** dikey penceresinde hello tıklatın **Resource Manager** dağıtım modeli ve ardından **oluşturma**.

    Merhaba aşağıdaki tabloda hello sanal ağ için hello ayarları gösterilmektedir:

   | **Alan** | Değer |
   | --- | --- |
   | **Ad** |autoHAVNET |
   | **Adres alanı** |10.33.0.0/24 |
   | **Alt ağ adı** |Yönetici |
   | **Alt ağ adres aralığı** |10.33.0.0/29 |
   | **Abonelik** |Toouse düşündüğünüz hello abonelik belirtin. **Abonelik** yalnızca bir aboneliğiniz varsa boştur. |
   | **Kaynak grubu** |Seçin **var olanı kullan** ve hello hello kaynak grubunun adını seçin. |
   | **Konum** |Hello Azure konumu belirtin. |

   Adres alanı ve alt ağ adres aralığınızı hello tablodan farklı olabilir. Aboneliğinize bağlı olarak, kullanılabilir adres alanı ve karşılık gelen alt ağ adres aralığı hello portal önerir. Hiçbir yeterli adres alanı varsa, farklı bir abonelik kullanın.

   Merhaba örneği kullanan bir alt ağ adı hello **yönetici**. Bu alt ağ hello etki alanı denetleyicileri içindir.

5. **Oluştur**'a tıklayın.

   ![Merhaba sanal ağ yapılandırma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/06-configurevirtualnetwork.png)

Azure portalı panosunun toohello döndürür ve hello yeni ağ oluşturulduğunda sizi uyarır.

### <a name="create-a-second-subnet"></a>İkinci alt ağ oluşturma
Merhaba yeni bir sanal ağ olan bir alt ağ, **yönetici**. hello etki alanı denetleyicileri bu alt ağ kullanın. SQL Server Vm'lerinin Hello kullanmak adlı ikinci bir alt ağ **SQL**. tooconfigure bu alt ağ:

1. Panonuzda, oluşturduğunuz hello kaynak grubu tıklatın **SQL-HA-RG**. Merhaba ağ hello kaynak grubu altında bulun **kaynakları**.

    Varsa **SQL-HA-RG** görünmeyen, bunu bulmak **kaynak grupları** ve hello kaynak grubu adına göre filtreleme.
2. Tıklatın **autoHAVNET** kaynakları hello listesinde. Azure hello ağ yapılandırma dikey penceresi açılır.
3. Merhaba üzerinde **autoHAVNET** sanal ağ dikey altında **ayarları** , tıklatın **alt ağlar**.

    Önceden oluşturulmuş hello alt unutmayın.

   ![Merhaba sanal ağ yapılandırma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/07-addsubnet.png)
5. İkinci bir alt ağ oluşturun. Tıklatın **+ alt**.
6. Merhaba üzerinde **alt ağ Ekle** dikey penceresinde hello alt yazarak yapılandırın **sqlsubnet** altında **adı**. Azure otomatik olarak belirtir geçerli bir **adres aralığı**. Bu adres aralığı en az 10 adresleri içinde olduğunu doğrulayın. Bir üretim ortamında, daha fazla adresleri gerektirebilir.
7. **Tamam** düğmesine tıklayın.

    ![Merhaba sanal ağ yapılandırma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/08-configuresubnet.png)

Aşağıdaki tablonun hello hello ağ yapılandırması ayarları özetlenmektedir:

| **Alan** | Değer |
| --- | --- |
| **Ad** |**autoHAVNET** |
| **Adres alanı** |Bu değer hello kullanılabilir adres alanları aboneliğinizde bağlıdır. Tipik bir değer 10.0.0.0/16 ' dir. |
| **Alt ağ adı** |**Yönetici** |
| **Alt ağ adres aralığı** |Bu değer hello kullanılabilir adres aralıklarını aboneliğinizde bağlıdır. Tipik bir değer 10.0.0.0/24 ' dir. |
| **Alt ağ adı** |**sqlsubnet** |
| **Alt ağ adres aralığı** |Bu değer hello kullanılabilir adres aralıklarını aboneliğinizde bağlıdır. Tipik bir değer 10.0.1.0/24 ' dir. |
| **Abonelik** |Toouse düşündüğünüz hello abonelik belirtin. |
| **Kaynak Grubu** |**SQL-HA-RG** |
| **Konum** |Belirtin hello hello kaynak grubu için seçtiğiniz aynı konumu. |

## <a name="create-availability-sets"></a>Kullanılabilirlik kümeleri oluşturma

Sanal makineleri oluşturmadan önce toocreate kullanılabilirlik kümeleri gerekir. Kullanılabilirlik kümeleri, planlı veya plansız bir bakım olayları hello kapalı kalma süresini azaltın. Bir Azure kullanılabilirlik kümesi, fiziksel hata etki alanları ve güncelleme etki alanına Azure yerleştirir kaynakların mantıksal bir gruptur. Hata etki alanı hello kullanılabilirlik kümesinin hello üyeleri ayrı güç ve ağ kaynaklarına sahip olmasını sağlar. Bir güncelleştirme etki alanı hello kullanılabilirlik kümesi üyeleri Merhaba, bakım için aynı duruma olmayan olduğunu sağlar zaman. Daha fazla bilgi için bkz: [hello sanal makinelerin kullanılabilirliğini yönetme](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

İki kullanılabilirlik kümesi gerekir. Merhaba etki alanı denetleyicileri için biridir. Merhaba ikinci hello SQL Server VM'ler için değil.

Kullanılabilirlik kümesi, gidin toohello kaynak grubu ve tıklayın toocreate **Ekle**. Filtre Hello sonuçları yazarak **kullanılabilirlik kümesi**. Tıklatın **kullanılabilirlik kümesi** hello sonuçları ve ardından **oluşturma**.

Aşağıdaki tablonun hello toohello parametrelere göre iki kullanılabilirlik kümesi yapılandırın:

| **Alan** | Etki alanı denetleyicisi kullanılabilirlik kümesi | SQL Server kullanılabilirlik kümesi |
| --- | --- | --- |
| **Ad** |adavailabilityset |sqlavailabilityset |
| **Kaynak grubu** |SQL-HA-RG |SQL-HA-RG |
| **Hata etki alanları** |3 |3 |
| **Güncelleme etki alanları** |5 |3 |

Merhaba kullanılabilirlik kümeleri oluşturduktan sonra toohello kaynak grubu hello Azure portalına dönün.

## <a name="create-domain-controllers"></a>Etki alanı denetleyicileri oluşturun
Merhaba ağ, alt ağlar, kullanılabilirlik kümeleri ve bir Internet'e yönelik Yük Dengeleyici oluşturduktan sonra hazır toocreate hello sanal makineleri hello etki alanı denetleyicileri için demektir.

### <a name="create-virtual-machines-for-hello-domain-controllers"></a>Etki alanı denetleyicileri hello için sanal makineler oluşturun
toocreate ve hello etki alanı denetleyicileri yapılandırın, toohello **SQL-HA-RG** kaynak grubu.

1. **Ekle**'ye tıklayın. Merhaba **her şeyi** dikey pencere açılır.
2. Tür **Windows Server 2016 Datacenter**.
3. Tıklatın **Windows Server 2016 Datacenter**. Merhaba, **Windows Server 2016 Datacenter** dikey penceresinde bu hello dağıtım modeli olduğunu doğrulayın **Resource Manager**ve ardından **oluşturma**. Azure açılır hello **sanal makine oluşturma** dikey.

Önceki adımları toocreate iki sanal makine hello yineleyin. Merhaba iki sanal makine adı:

* ad birincil dc
* ad ikincil dc

  > [!NOTE]
  > Merhaba **ad ikincil dc** sanal makine isteğe bağlı, Active Directory etki alanı Hizmetleri için yüksek kullanılabilirlik tooprovide.
  >
  >

Merhaba aşağıdaki tabloda bu iki makine hello ayarları gösterilmektedir:

| **Alan** | Değer |
| --- | --- |
| **Ad** |İlk etki alanı denetleyicisi: *ad birincil dc*.</br>İkinci etki alanı denetleyicisi *ad ikincil dc*. |
| **VM disk türü** |SSD |
| **Kullanıcı adı** |Etki alanı yöneticisi |
| **Parola** |Contoso! 0000 |
| **Abonelik** |*Aboneliğiniz* |
| **Kaynak grubu** |SQL-HA-RG |
| **Konum** |*Konumunuz* |
| **Boyut** |DS1_V2 |
| **Depolama** | **Yönetilen diskler kullanan** - **Evet** |
| **Sanal ağ** |autoHAVNET |
| **Alt ağ** |Yönetici |
| **Genel IP adresi** |*Merhaba VM adıyla aynı* |
| **Ağ güvenlik grubu** |*Merhaba VM adıyla aynı* |
| **Kullanılabilirlik kümesi** |adavailabilityset </br>**Hata etki alanları**: 2</br>**Güncelleme etki alanları**: 2|
| **Tanılama** |Etkin |
| **Tanılama depolama hesabı** |*Otomatik olarak oluşturulur* |

   >[!IMPORTANT]
   >Bu gibi durumlarda, bir VM yalnızca kullanılabilirlik oluşturduğunuzda kümesi içinde yerleştirebilirsiniz. Merhaba kullanılabilirlik VM oluşturulduktan sonra değiştirilemez. Bkz: [hello sanal makinelerin kullanılabilirliğini yönetme](../manage-availability.md).

Azure hello sanal makineler oluşturur.

Merhaba sanal makine oluşturulduktan sonra hello etki alanı denetleyicisi yapılandırın.

### <a name="configure-hello-domain-controller"></a>Merhaba etki alanı denetleyicisini Yapılandır
Hello aşağıdaki adımlar, yapılandırma hello **ad birincil dc** corp.contoso.com etki alanı denetleyicisi olarak makine.

1. Merhaba Hello Portalı'nda açmak **SQL-HA-RG** kaynak grubu ve select hello **ad birincil dc** makine. Merhaba üzerinde **ad birincil dc** dikey penceresinde tıklatın **Bağlan** tooopen bir RDP dosyası için Uzak Masaüstü erişimi.

    ![Tooa sanal makineye bağlanma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/20-connectrdp.png)
2. Yapılandırılmış Yönetici hesabınızla oturum açın (**\DomainAdmin**) ve parolayı (**Contoso! 0000**).
3. Varsayılan olarak, hello **Sunucu Yöneticisi'ni** Pano görüntülenmesi.
4. Merhaba tıklatın **rol ve Özellik Ekle** hello Panoda bağlantı.

    ![Sunucu Yöneticisi - rolleri Ekle](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
5. Seçin **sonraki** toohello elde edene kadar **sunucu rolleri** bölümü.
6. Select hello **Active Directory etki alanı Hizmetleri** ve **DNS sunucusu** rolleri. İstendiğinde, bu roller için gerekli olan diğer ek özellikleri ekleyin.

   > [!NOTE]
   > Windows, statik IP adresi olduğunu sizi uyarır. Merhaba yapılandırma test ediyorsanız tıklatın **devam**. Üretim senaryoları için başlangıç IP adresi toostatic hello Azure portal, ayarlama veya [PowerShell tooset hello statik IP adresi hello etki alanı denetleyicisi makinenin kullanmak](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   >
   >

    ![Rolleri iletişim ekleyin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/23-addroles.png)
7. Tıklatın **sonraki** hello ulaşana kadar **onay** bölümü. Select hello **otomatik olarak yeniden başlatma hello hedef sunucu** onay kutusu.
8. **Yükle**'ye tıklayın.
9. Yükleme, dönüş toohello Hello özellikleri tamamladıktan sonra **Sunucu Yöneticisi'ni** Pano.
10. Select hello yeni **AD DS** hello sol bölmede seçeneği.
11. Merhaba tıklatın **daha fazla** hello sarı uyarı çubuğundaki bağlantı.

    ![AD DS iletişim kutusunda hello DNS sunucusu VM](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/24-addsmore.png)
12. Merhaba, **eylem** hello sütunu **tüm sunucu görev ayrıntıları** iletişim kutusunda, tıklatın **bu sunucu tooa etki alanı denetleyicisini**.
13. Merhaba, **Active Directory etki alanı Hizmetleri Yapılandırma Sihirbazı**, hello aşağıdaki değerleri kullanın:

    | **Sayfa** | Ayar |
    | --- | --- |
    | **Dağıtım Yapılandırması** |**Yeni orman Ekle**<br/> **Kök etki alanı adı** corp.contoso.com = |
    | **Etki alanı denetleyicisi seçenekleri** |**DSRM parolasını** Contoso =! 0000<br/>**Parolayı onaylayın** Contoso =! 0000 |
14. Tıklatın **sonraki** toogo aracılığıyla hello hello Sihirbazı diğer sayfalar. Merhaba üzerinde **Önkoşul denetimi** sayfasında, iletiden hello gördüğünüzü doğrulayın: **tüm önkoşul denetimlerinden başarıyla geçti**. Uygulanabilir tüm uyarı iletilerini gözden geçirebilirsiniz ancak hello yüklemesiyle olası toocontinue değil.
15. **Yükle**'ye tıklayın. Merhaba **ad birincil dc** sanal makine otomatik olarak yeniden başlatılır.

### <a name="note-hello-ip-address-of-hello-primary-domain-controller"></a>Merhaba birincil etki alanı denetleyicisinin Hello IP adresini not alın

Merhaba birincil etki alanı denetleyicisi, DNS için kullanın. Merhaba birincil etki alanı denetleyicisi IP adresini not edin.

Tek yönlü tooget hello birincil etki alanı denetleyicisi IP hello Azure portal adresidir.

1. Hello Azure portal, hello kaynak grubu açın.

2. Merhaba birincil etki alanı denetleyicisini tıklatın.

3. Merhaba birincil etki alanı denetleyicisi dikey penceresinde **ağ arabirimleri**.

![Ağ arabirimleri](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/25-primarydcip.png)

Bu sunucu için özel IP adresi Hello unutmayın.

### <a name="configure-hello-virtual-network-dns"></a>Merhaba sanal ağ DNS yapılandırma
Merhaba ilk etki alanı denetleyicisi oluşturmak ve DNS hello ilk sunucuda etkinleştirme sonra hello sanal ağ toouse bu sunucuyu DNS için yapılandırın.

1. Hello Azure portal, hello sanal ağ'ı tıklatın.

2. Altında **ayarları**, tıklatın **DNS sunucusu**.

3. Tıklatın **özel**ve hello birincil etki alanı denetleyicisi hello özel IP adresini yazın.

4. **Kaydet** düğmesine tıklayın.

### <a name="configure-hello-second-domain-controller"></a>Merhaba ikinci etki alanı denetleyicisi yapılandırma
Merhaba birincil etki alanı denetleyicisi yeniden başlatıldıktan sonra ikinci etki alanı denetleyicisi hello yapılandırabilirsiniz. Bu isteğe bağlı yüksek kullanılabilirlik için bir adımdır. Bu adımları tooconfigure hello ikinci etki alanı denetleyicisi izleyin:

1. Merhaba Hello Portalı'nda açmak **SQL-HA-RG** kaynak grubu ve select hello **ad ikincil dc** makine. Merhaba üzerinde **ad ikincil dc** dikey penceresinde tıklatın **Bağlan** tooopen bir RDP dosyası için Uzak Masaüstü erişimi.
2. Toohello VM yapılandırılmış yönetici hesabınızı kullanarak oturum (**BUILTIN\DomainAdmin**) ve parolayı (**Contoso! 0000**).
3. Değişiklik hello tercih edilen DNS sunucusu adresi toohello adresi hello etki alanı denetleyicisi.
4. İçinde **ağ ve Paylaşım Merkezi**, hello ağ arabirimi'ı tıklatın.
   ![Ağ arabirimi](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/26-networkinterface.png)

5. **Özellikler**'e tıklayın.
6. Seçin **Internet Protokolü sürüm 4 (TCP/IPv4)** tıklatıp **özellikleri**.
7. Seçin **aşağıdaki DNS sunucu adreslerini kullan hello** ve hello birincil etki alanı denetleyicisinin hello adresini belirtin **tercih edilen DNS sunucusu**.
8. Tıklatın **Tamam**ve ardından **Kapat** toocommit hello değişiklikleri. Artık mümkün toojoin hello VM çok olduğunuz**corp.contoso.com**.

   >[!IMPORTANT]
   >Merhaba DNS ayarı değiştirdikten sonra hello bağlantı tooyour Uzak Masaüstü kaybederseniz, toohello Azure portal ve yeniden başlatma hello sanal makine gidin.

9. Merhaba Uzak Masaüstü toohello ikincil etki alanı denetleyicisinden açmak **Sunucu Yöneticisi Panosu**.
10. Merhaba tıklatın **rol ve Özellik Ekle** hello Panoda bağlantı.

    ![Sunucu Yöneticisi - rolleri Ekle](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
11. Seçin **sonraki** toohello elde edene kadar **sunucu rolleri** bölümü.
12. Select hello **Active Directory etki alanı Hizmetleri** ve **DNS sunucusu** rolleri. İstendiğinde, bu roller için gerekli olan diğer ek özellikleri ekleyin.
13. Yükleme, dönüş toohello Hello özellikleri tamamladıktan sonra **Sunucu Yöneticisi'ni** Pano.
14. Select hello yeni **AD DS** hello sol bölmede seçeneği.
15. Merhaba tıklatın **daha fazla** hello sarı uyarı çubuğundaki bağlantı.
16. Merhaba, **eylem** hello sütunu **tüm sunucu görev ayrıntıları** iletişim kutusunda, tıklatın **bu sunucu tooa etki alanı denetleyicisini**.
17. Altında **Dağıtım Yapılandırması**seçin **etki alanı denetleyicisi tooan varolan etki alanı eklemek**.
   ![Dağıtım Yapılandırması](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/28-deploymentconfig.png)
18. **Seç**'e tıklayın.
19. Merhaba yönetici hesabı kullanarak bağlanmak (**CORP. CONTOSO.COM\domainadmin**) ve parolayı (**Contoso! 0000**).
20. İçinde **hello ormandan bir etki alanı seçin**etki alanınızı tıklatın ve ardından **Tamam**.
21. İçinde **etki alanı denetleyicisi seçenekleri**, hello varsayılan değerleri kullanın ve DSRM parolasını ayarlayın.

   >[!NOTE]
   >Merhaba **DNS seçenekleri** sayfa uyar, bu DNS sunucusu için bir temsilci oluşturulamıyor. Üretim dışı ortamlarında bu uyarıyı yoksayabilirsiniz.
22. Tıklatın **sonraki** hello iletişim hello ulaşana kadar **Önkoşullar** denetleyin. Ardından **Yükle**'ye tıklayın.

Merhaba sunucu hello yapılandırma değişikliklerini bittikten sonra hello sunucuyu yeniden başlatın.

### <a name="add-hello-private-ip-address-toohello-second-domain-controller-toohello-vpn-dns-server"></a>Merhaba özel IP adresi toohello ikinci etki alanı denetleyicisi toohello VPN DNS sunucusu Ekle

Hello Azure portal, sanal ağ altında hello ikincil etki alanı denetleyicisi hello DNS sunucusu tooinclude hello IP adresini değiştirin. Bu hello DNS hizmeti artıklık sağlar.

### <a name=DomainAccounts></a>Merhaba etki alanı hesaplarını yapılandırma

Merhaba sonraki adımlarda hello Active Directory hesaplarını yapılandırın. Merhaba aşağıdaki tabloda hello hesapları gösterilmektedir:

| |Yükleme hesabı<br/> |SQLServer-0 <br/>SQL Server ve SQL aracısı hizmet hesabı |SQLServer-1<br/>SQL Server ve SQL aracısı hizmet hesabı
| --- | --- | --- | ---
|**İlk adı** |Yükleme |SQLSvc1 | SQLSvc2
|**Kullanıcı SamAccountName** |Yükleme |SQLSvc1 | SQLSvc2

Aşağıdaki adımları toocreate hello her hesabı kullanın.

1. İçinde toohello oturum **ad birincil dc** makine.
2. İçinde **Sunucu Yöneticisi'ni**seçin **Araçları**ve ardından **Active Directory Yönetim Merkezi'ni**.   
3. Seçin **corp (yerel)** hello sol bölmesinden.
4. Merhaba sağ üzerinde **görevleri** bölmesinde, **yeni**ve ardından **kullanıcı**.
   ![Active Directory Yönetim Merkezi](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/29-addcnewuser.png)

   >[!TIP]
   >Her hesap için karmaşık bir parola ayarlayın.<br/> Üretim dışı ortamlar için kümesi hello kullanıcı hesabı toonever süresi.

5. Tıklatın **Tamam** toocreate hello kullanıcı.
6. Merhaba her hello üç hesapları için önceki adımları yineleyin.

### <a name="grant-hello-required-permissions-toohello-installation-account"></a>Merhaba gerekli izinleri toohello yükleme hesabı
1. Merhaba, **Active Directory Yönetim Merkezi'ni**seçin **corp (yerel)** hello sol bölmede. Merhaba sağ sonra **görevleri** bölmesinde tıklatın **özellikleri**.

    ![CORP kullanıcı özellikleri](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/31-addcproperties.png)
2. Seçin **uzantıları**ve ardından hello **Gelişmiş** hello düğmesinde **güvenlik** sekmesi.
3. Merhaba, **corp için Gelişmiş güvenlik ayarları** iletişim kutusunda, tıklatın **Ekle**.
4. Tıklatın **sorumlu Seç**, arama **CORP\Install**ve ardından **Tamam**.
5. Select hello **tüm özellikleri oku** onay kutusu.

6. Select hello **bilgisayar nesneleri oluşturma** onay kutusu.

     ![Corp kullanıcı izinleri](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/33-addpermissions.png)
7. Tıklatın **Tamam**ve ardından **Tamam** yeniden. Kapat hello **corp** Özellikler penceresi.

Active Directory ve hello kullanıcı nesneleri yapılandırma bitirdikten sonra iki SQL Server VM'ler ve Tanık VM oluşturun. Ardından, tüm üç toohello etki alanına katılın.

## <a name="create-sql-server-vms"></a>SQL Server Vm'lerinin oluşturma

Üç ek sanal makineler oluşturun. SQL Server örnekleri iki sanal makinelerle Hello çözümü gerektirir. Üçüncü sanal makineye bir tanığı olarak çalışır. Windows Server 2016 kullanabileceğiniz bir [bulut Tanık](http://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness), ancak bu belgenin önceki işletim sistemleri ile tutarlılığını tanığı için bir sanal makine kullanır.  

Devam etmeden önce deisign kararları aşağıdaki hello göz önünde bulundurun.

* **Depolama - Azure tarafından yönetilen disklerde**

   Merhaba sanal makine depolama için Azure yönetilen diskleri kullanın. Microsoft SQL Server sanal makineler için yönetilen diskleri önerir. Diskleri tanıtıcılarını depolama hello perde arkasında yönetilen. Ayrıca, sanal makineleri yönetilen disklerle olduğunda hello aynı kullanılabilirlik kümesi, Azure hello depolama kaynakları tooprovide uygun artıklık dağıtır. Daha fazla bilgi için bkz. [Azure Yönetilen Disklere Genel Bakış](../managed-disks-overview.md). Bir kullanılabilirlik kümesinde yönetilen diskler hakkında daha fazla ayrıntı için bkz: [bir kullanılabilirlik kümesindeki sanal makineleri için kullanım yönetilen diskleri](../manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).

* **Ağ - üretimde özel IP adresleri**

   Merhaba sanal makineler için Bu öğretici ortak IP adreslerini kullanır. Internet üzerinden toohello sanal makine hello doğrudan bu uzak bağlantı sağlar - yapılandırma adımlarını kolaylaştırır. Üretim ortamlarında, Microsoft, yalnızca özel IP adresleri sipariş tooreduce hello güvenlik açığı ayak hello SQL Server örneğinin VM kaynak önerir.

### <a name="create-and-configure-hello-sql-server-vms"></a>Oluşturma ve hello SQL Server Vm'lerinin yapılandırma
Ardından, üç sanal makineleri--iki SQL Server VM'ler ve ek bir küme düğümüne için bir VM oluşturun. toocreate her hello VM'lerin Geri Git toohello **SQL-HA-RG** kaynak grubu, tıklatın **Ekle**, arama hello uygun galeri öğesi için tıklatın **sanal makine**ve ardından tıklatın **Galeri'den**. Aşağıdaki tabloda toohelp hello VM'ler oluşturmak hello Hello bilgileri kullanın:


| Sayfa | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Merhaba uygun galeri öğesi seçin |**Windows Server 2016 Datacenter** |**Windows Server 2016 SQL Server 2016 SP1 Enterprise** |**Windows Server 2016 SQL Server 2016 SP1 Enterprise** |
| Sanal Makine Yapılandırması **temelleri** |**Ad** küme fsw =<br/>**Kullanıcı adı** DomainAdmin =<br/>**Parola** Contoso =! 0000<br/>**Abonelik** aboneliğinizi =<br/>**Kaynak grubu** SQL-HA-RG =<br/>**Konum** azure konumunuz = |**Ad** sqlserver-0 =<br/>**Kullanıcı adı** DomainAdmin =<br/>**Parola** Contoso =! 0000<br/>**Abonelik** aboneliğinizi =<br/>**Kaynak grubu** SQL-HA-RG =<br/>**Konum** azure konumunuz = |**Ad** sqlserver-1 =<br/>**Kullanıcı adı** DomainAdmin =<br/>**Parola** Contoso =! 0000<br/>**Abonelik** aboneliğinizi =<br/>**Kaynak grubu** SQL-HA-RG =<br/>**Konum** azure konumunuz = |
| Sanal Makine Yapılandırması **boyutu** |**BOYUTU** DS1 =\_V2 (1 çekirdek, 3.5 GB) |**BOYUTU** DS2 =\_V2 (2 Çekirdek, 7 GB)</br>Merhaba boyutu SSD depolama (Premium disk desteği. desteklemesi gerekir )) |**BOYUTU** DS2 =\_V2 (2 Çekirdek, 7 GB) |
| Sanal Makine Yapılandırması **ayarları** |**Depolama**: yönetilen diskleri kullanın.<br/>**Sanal ağ** autoHAVNET =<br/>**Alt ağ** sqlsubnet(10.1.1.0/24) =<br/>**Genel IP adresi** otomatik olarak oluşturulan.<br/>**Ağ güvenlik grubu** = yok<br/>**Tanılama izleme** = etkin<br/>**Tanılama depolama hesabı** otomatik olarak oluşturulan depolama hesabı kullan =<br/>**Kullanılabilirlik kümesi** sqlAvailabilitySet =<br/> |**Depolama**: yönetilen diskleri kullanın.<br/>**Sanal ağ** autoHAVNET =<br/>**Alt ağ** sqlsubnet(10.1.1.0/24) =<br/>**Genel IP adresi** otomatik olarak oluşturulan.<br/>**Ağ güvenlik grubu** = yok<br/>**Tanılama izleme** = etkin<br/>**Tanılama depolama hesabı** otomatik olarak oluşturulan depolama hesabı kullan =<br/>**Kullanılabilirlik kümesi** sqlAvailabilitySet =<br/> |**Depolama**: yönetilen diskleri kullanın.<br/>**Sanal ağ** autoHAVNET =<br/>**Alt ağ** sqlsubnet(10.1.1.0/24) =<br/>**Genel IP adresi** otomatik olarak oluşturulan.<br/>**Ağ güvenlik grubu** = yok<br/>**Tanılama izleme** = etkin<br/>**Tanılama depolama hesabı** otomatik olarak oluşturulan depolama hesabı kullan =<br/>**Kullanılabilirlik kümesi** sqlAvailabilitySet =<br/> |
| Sanal Makine Yapılandırması **SQL Server ayarları** |Uygulanamaz |**SQL Bağlantısı** özel (sanal ağ dahilinde) =<br/>**Bağlantı noktası** 1433 =<br/>**SQL kimlik doğrulaması** = devre dışı bırak<br/>**Depolama yapılandırması** genel =<br/>**Otomatik düzeltme eki uygulama** 2: 00'dan Pazar =<br/>**Otomatik yedekleme** = devre dışı</br>**Azure anahtar kasası tümleştirme** = devre dışı |**SQL Bağlantısı** özel (sanal ağ dahilinde) =<br/>**Bağlantı noktası** 1433 =<br/>**SQL kimlik doğrulaması** = devre dışı bırak<br/>**Depolama yapılandırması** genel =<br/>**Otomatik düzeltme eki uygulama** 2: 00'dan Pazar =<br/>**Otomatik yedekleme** = devre dışı</br>**Azure anahtar kasası tümleştirme** = devre dışı |

<br/>

> [!NOTE]
> burada önerilen makine boyutlarını hello kullanılabilirlik grupları Azure Vm'lerde test etmek için yöneliktir. Merhaba en iyi performans için üretim iş yükleri üzerinde SQL Server makine boyutlarını ve yapılandırmada hello önerilerini görmek [performans Azure sanal makinelerde SQL Server için en iyi uygulamaları](virtual-machines-windows-sql-performance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

Merhaba üç VM'ler tam olarak sağlandıktan sonra toojoin gereksinim bunları toohello **corp.contoso.com** CORP\Install yönetici hakları toohello makineler etki alanı ve verin.

### <a name="joinDomain"></a>Merhaba sunucuları toohello etki alanına katılma

Mümkün toojoin hello artık sanal makineleri çok olduğunuz**corp.contoso.com**. Merhaba aşağıdaki hello SQL Server Vm'lerinin ve hello dosyası Tanık paylaşım:

1. Toohello sanal makineyle uzaktan bağlantı **BUILTIN\DomainAdmin**.
2. İçinde **Sunucu Yöneticisi'ni**, tıklatın **yerel sunucu**.
3. Merhaba tıklatın **çalışma grubu** bağlantı.
4. Merhaba, **bilgisayar adı** 'yi tıklatın **değişiklik**.
5. Select hello **etki alanı** onay kutusunu ve türü **corp.contoso.com** hello metin kutusuna. **Tamam** düğmesine tıklayın.
6. Merhaba, **Windows Güvenliği** açılan iletişim kutusunda, hello varsayılan etki alanı yöneticisi hesabı hello kimlik bilgilerini belirtin (**CORP\DomainAdmin**) ve hello parola (**Contoso! 0000**).
7. Merhaba "Hoş Geldiniz toohello corp.contoso.com etki alanında" iletisini gördüğünüzde, tıklatın **Tamam**.
8. Tıklatın **Kapat**ve ardından **şimdi yeniden Başlat** hello açılan iletişim kutusunda.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-cluster-vm"></a>Her küme VM üzerinde bir yönetici olarak Hello Corp\Install kullanıcı ekleme

Merhaba etki alanının bir üyesi olarak her sanal makine yeniden başlatıldıktan sonra add **CORP\Install** hello yerel Yöneticiler grubunun bir üyesi olarak.

1. Merhaba VM yeniden başlatılıncaya kadar bekleyin, sonra hello RDP dosyasından yeniden hello birincil etki alanı denetleyicisi toosign çok başlatma**sqlserver-0** hello kullanarak **CORP\DomainAdmin** hesabı.
   >[!TIP]
   >Merhaba etki alanı yönetici hesabıyla oturum emin olun. Merhaba önceki adımlarda hello YERLEŞİK IN yönetici hesabını kullanarak. Merhaba sunucu hello etki alanında olduğundan, hello etki alanı hesabı kullanın. RDP oturumunuzda belirtin *etki alanı*\\*kullanıcıadı*.

2. İçinde **Sunucu Yöneticisi'ni**seçin **Araçları**ve ardından **Bilgisayar Yönetimi**.
3. Merhaba, **Bilgisayar Yönetimi** penceresinde genişletin **yerel kullanıcılar ve gruplar**ve ardından **grupları**.
4. Merhaba çift **Yöneticiler** grubu.
5. Merhaba, **Yöneticiler özellikleri** iletişim kutusunda, hello tıklatın **Ekle** düğmesi.
6. Merhaba kullanıcı girin **CORP\Install**ve ardından **Tamam**.
7. Tıklatın **Tamam** tooclose hello **yönetici özellikleri** iletişim.
8. Merhaba önceki adımları tekrarlayın **sqlserver-1** ve **küme fsw**.

### <a name="setServiceAccount"></a>Merhaba SQL Server hizmet hesapları

Her SQL Server VM üzerinde hello SQL Server hizmet hesabı ayarlayın. Ne zaman oluşturulan hello hesapları kullanmak, [hello etki alanı hesapları yapılandırılmış](#DomainAccounts).

1. Açık **SQL Server Configuration Manager**.
2. Merhaba SQL Server hizmetini sağ tıklatın ve ardından **özellikleri**.
3. Merhaba hesap ve parola ayarlayın.
4. Diğer SQL Server VM hello bu adımları yineleyin.  

SQL Server kullanılabilirlik grupları için her SQL Server VM bir etki alanı hesabı olarak toorun gerekir.

### <a name="create-a-sign-in-on-each-sql-server-vm-for-hello-installation-account"></a>Bir oturum açma hello yükleme hesabı için her bir SQL Server VM oluşturma

Merhaba yükleme hesabı (CORP\install) tooconfigure hello kullanılabilirlik grubu kullanın. Bu hesap toobe hello üyesi olmalıdır **sysadmin** her SQL Server VM üzerinde sabit sunucu rolü. Merhaba aşağıdaki adımlar bir oturum açma için hello yükleme hesabı oluşturun:

1. Hello kullanarak Uzak Masaüstü Protokolü (RDP) hello toohello sunucusuna bağlanan  *\<MachineName\>\DomainAdmin* hesabı.

1. SQL Server Management Studio'yu açın ve toohello yerel SQL Server örneğine bağlanın.

1. İçinde **Object Explorer**, tıklatın **güvenlik**.

1. Sağ **oturumları**. Tıklatın **yeni oturum açma**.

1. İçinde **yeni oturum açma -**, tıklatın **arama**.

1. Tıklatın **konumları**.

1. Merhaba etki alanı yöneticisi ağ kimlik bilgilerini girin.

1. Merhaba yükleme hesabı kullanın.

1. Oturum açma Hello toobe kümesi hello üyesi **sysadmin** sabit sunucu rolü.

1. **Tamam** düğmesine tıklayın.

Diğer SQL Server VM hello adımları önceki hello yineleyin.

## <a name="add-failover-clustering-features-tooboth-sql-server-vms"></a>Yük Devretme Kümelemesi özellikleri tooboth SQL Server Vm'lerinin Ekle

Yük devretme kümeleme özellikleri tooadd hello her iki SQL Server VM üzerinde aşağıdaki:

1. Hello kullanarak Uzak Masaüstü Protokolü (RDP) hello toohello SQL Server sanal makineye bağlanmak *CORP\install* hesabı. Açık **Sunucu Yöneticisi Panosu**.
2. Merhaba tıklatın **rol ve Özellik Ekle** hello Panoda bağlantı.

    ![Sunucu Yöneticisi - rolleri Ekle](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
3. Seçin **sonraki** toohello elde edene kadar **Server özellikleri** bölümü.
4. İçinde **özellikleri**seçin **Yük Devretme Kümelemesi**.
5. Gerekli diğer ek özellikleri ekleyin.
6. Tıklatın **yükleme** tooadd hello özellikleri.

Diğer SQL Server VM hello Hello adımları yineleyin.

## <a name="a-nameendpoint-firewall-configure-hello-firewall-on-each-sql-server-vm"></a><a name="endpoint-firewall">Her SQL Server VM Hello güvenlik duvarını yapılandırma

Merhaba çözüm TCP bağlantı noktaları toobe açık hello Güvenlik Duvarı'nda aşağıdaki hello gerektirir:

- **SQL Server VM**:<br/>
   Bağlantı noktası 1433'ü SQL Server'ın varsayılan bir örnek için.
- **Azure yük dengeleyici araştırmasını:**<br/>
   Tüm kullanılabilir bağlantı noktası. Örnekler sık 59999 kullanın.
- **Veritabanı yansıtma uç noktası:** <br/>
   Tüm kullanılabilir bağlantı noktası. Örnekler sık 5022 kullanın.

Merhaba Güvenlik Duvarı hem de SQL Server Vm'lerinde açık gerek toobe bağlantı noktaları.

Merhaba bağlantı noktaları açma hello yöntemi kullandığınız hello güvenlik duvarı çözüm üzerinde bağlıdır. nasıl tooopen hello Windows Güvenlik Duvarı'nda bağlantı noktaları Hello sonraki bölümde açıklanmaktadır. Her SQL Server Vm'lerinin hello gerekli bağlantı noktalarını açın.

### <a name="open-a-tcp-port-in-hello-firewall"></a>Merhaba Güvenlik Duvarı'nda bir TCP bağlantı noktasını açın

1. İlk SQL Server üzerinde hello **Başlat** ekranında, başlatma **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı**.
2. Merhaba soldaki bölmede bulunan seçin **gelen kuralları**. Merhaba sağ bölmesinde tıklatın **yeni kural**.
3. İçin **kural türü**, seçin **bağlantı noktası**.
4. Merhaba bağlantı noktasını belirtin **TCP** ve bağlantı noktası numaralarını uygun türü hello. Aşağıdaki örnek hello bakın:

   ![SQL güvenlik duvarı](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/35-tcpports.png)

5. **İleri**’ye tıklayın.
6. Merhaba üzerinde **eylem** sayfasında, tutmak **hello bağlantıya izin verme** seçili ve ardından **sonraki**.
7. Merhaba üzerinde **profil** sayfasında, hello varsayılan ayarları kabul edin ve ardından **sonraki**.
8. Merhaba üzerinde **adı** sayfasında, bir kural adı belirtin (gibi **Azure LB araştırma**) hello içinde **adı** metin kutusuna ve ardından **son**.

İkinci SQL Server VM hello şu adımları yineleyin.

## <a name="next-steps"></a>Sonraki adımlar

* [Azure sanal makinelerde bir SQL Server Always On kullanılabilirlik grubu oluşturma](virtual-machines-windows-portal-sql-availability-group-tutorial.md)
