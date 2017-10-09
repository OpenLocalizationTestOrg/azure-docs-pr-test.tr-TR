# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Azure'da sanal makineler için kullanılabilirlik ve bölgeler
Merhaba Dünya birden çok veri merkezlerinde Azure çalışır. Bu veri merkezlerinde nereye koyacağınızı seçmek esneklik vermiş toogeographic bölgelerde gruplandırılır toobuild uygulamalarınızı. Bu önemli toounderstand nasıl ve nerede sanal makineleri (VM'ler) seçenekleri toomaximize performans, kullanılabilirlik ve artıklık yanı sıra Azure içinde çalışmayabilir olur. Bu makalede hello kullanılabilirlik genel bir bakış ve Azure özelliklerini artıklık sağlar.

## <a name="what-are-azure-regions"></a>Azure bölgeleri nelerdir?
Tanımlanan coğrafi bölgelerde 'Batı ABD', 'Kuzey Avrupa' veya 'Güneydoğu Asya' gibi Azure kaynakları oluşturun. Merhaba gözden geçirebilirsiniz [bölgeler ve konumlarını listesi](https://azure.microsoft.com/regions/). Her bölge içinde birden çok veri merkezi tooprovide artıklık ve kullanılabilirlik için mevcut. Bu yaklaşım uygulamaları toocreate VM'ler en yakın tooyour kullanıcıları ve toomeet yasal, tüm uyumluluk tasarlarken veya amacıyla vergi esnekliği sağlar.

## <a name="special-azure-regions"></a>Özel Azure bölgeleri
Azure uygulamalarınızı uyumluluğu veya yasal amaçlar için genişletme oluştururken toouse isteyebilir bazı özel bölgeler sahiptir. Bu özel bölgeleri şunlardır:

* **ABD Virginia** ve **ABD Iowa**
  * ABD kamu kuruluşları ve iş ortaklarına yönelik olarak ABD’de bulunan ve denetlenen kişilerce çalıştırılan fiziksel ve mantıksal ağdan yalıtılmış Azure örneği. [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) ve [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA) gibi ek uyumluluk sertifikaları içerir. [Azure Kamu](https://azure.microsoft.com/features/gov/) hakkında daha fazla bilgi alın.
* **Çin Doğu** ve **Çin Kuzey**
  * Bu bölgeler arasında Microsoft ve alınabildiği Microsoft doğrudan hello veri merkezleri korumaz 21Vianet benzersiz ortaklık aracılığıyla kullanılabilir. [Çin’de Microsoft Azure](http://www.windowsazure.cn/) hakkında daha fazla bilgi alın.
* **Almanya Orta** ve **Almanya Kuzeydoğu**
  * Bu bölgeler yapabildiği denetimindeki T-sistemlerinin hello Almanca veri güvenliği davranan bir Alman Telekom şirket içinde Almanya müşteri verileri kalır veri güvenlik modelini aracılığıyla kullanılabilir.

## <a name="region-pairs"></a>Bölge çiftleri
Her Azure bölgesi hello içinde başka bir bölge ile eşleştirilmiş aynı coğrafi konum (örneğin, ABD, Avrupa veya Asya). Bu yaklaşım VM depolama gibi kaynaklar hello çoğaltılması için doğal afetler, hukuki unrest, güç kesintileri veya aynı anda hem bölgeler etkilemeden fiziksel ağ kesintileri hello olasılığını azaltmak bir coğrafi konum sağlar. Bölge çiftlerinin diğer avantajları şunlardır:

* Bir bölge daha geniş bir Azure hizmet kesintisi Hello olayda öncelik dışında her çifti toohelp azaltmak hello zaman toorestore uygulamalar için. 
* Planlanan Azure güncelleştirmeleri zaman toominimize kapalı kalma süresi ve uygulama kesinti riskini toopaired bölgeler bir alınır.
* Veri devam tooreside hello içinde aynı coğrafi konum (dışında Brezilya Güney) çiftini vergi ve yasa zorlama dairesi amaçlı olarak.

Bölge çiftlerinin örnekleri şunlardır:

| Birincil | İkincil |
|:--- |:--- |
| Batı ABD |Doğu ABD |
| Kuzey Avrupa |Batı Avrupa |
| Güneydoğu Asya |Doğu Asya |

Merhaba tam görebilirsiniz [bölge listesi çiftleri burada](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Özellik kullanılabilirliği
Belirli VM boyutları ya da depolama türleri gibi bazı hizmetler veya VM özellikleri yalnızca belirli bölgelerde kullanılabilir. Ayrıca belirli bir bölgenin tooselect gibi gerektirmeyen bazı genel Azure Hizmetleri olan [Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [trafik Yöneticisi](../articles/traffic-manager/traffic-manager-overview.md), veya [Azure DNS](../articles/dns/dns-overview.md). tooassist, uygulama ortamınızı tasarlarken, hello denetleyebilirsiniz [her bölge arasında Azure hizmetlerine kullanılabilirliğini](https://azure.microsoft.com/regions/#services). 

## <a name="storage-availability"></a>Depolama kullanılabilirliği
Kullanılabilir depolama çoğaltma seçenekleri hello göz önüne aldığınızda Azure bölgeler ve coğrafi anlama önemli hale gelir. Merhaba depolama türüne bağlı olarak, farklı çoğaltma seçeneğiniz vardır.

**Azure Yönetilen Diskler**
* Yerel olarak yedekli depolama (LRS)
  * Depolama hesabınızı oluşturduğunuz üç kez hello bölge içindeki verilerinizi çoğaltır.

**Depolama hesabı temelli diskler**
* Yerel olarak yedekli depolama (LRS)
  * Depolama hesabınızı oluşturduğunuz üç kez hello bölge içindeki verilerinizi çoğaltır.
* Bölgesel olarak yedekli depolama (ZRS)
  * Verilerinizi, tek bir bölge içinde veya iki bölgede iki toothree tesis üzerinde üç kez çoğaltır.
* Coğrafi olarak yedekli depolama (GRS)
  * Mil hello birincil bölge çıktığınızda yüzlerce olduğundan, veri tooa ikincil bölge çoğaltır.
* Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS)
  * GRS gibi ile veri tooa ikincil bölge çoğaltır, ancak daha sonra hello ikincil konumdaki salt okunur erişim toohello verileri sağlar.

Merhaba aşağıdaki tabloda hello depolama çoğaltma türleri arasındaki farklar hello hızlı bir genel bakış verilmektedir:

| Çoğaltma stratejisi | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Veriler birden çok tesis arasında çoğaltılır. |Hayır |Evet |Evet |Evet |
| Veri hello ikincil konumdan ve hello birincil konumdan okuyabilir. |Hayır |Hayır |Hayır |Evet |
| Ayrı düğümlerde tutulan veri kopyası sayısı. |3 |3 |6 |6 |

[Azure Depolama çoğaltma seçenekleri hakkında buradan](../articles/storage/common/storage-redundancy.md) daha fazla bilgi alabilirsiniz. Yönetilen diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../articles/virtual-machines/windows/managed-disks-overview.md).

### <a name="storage-costs"></a>Depolama maliyetleri
Fiyatlar hello depolama türünü ve seçtiğiniz kullanılabilirlik bağlı olarak değişir.

**Azure Yönetilen Diskler**
* Premium yönetilen diskleri Solid-State sürücüler tarafından (SSD) desteklenir ve standart yönetilen disk normal dönen disk ile desteklenir. Premium ve standart yönetilen disk hello disk sağlanan hello kapasitesine göre ücretlendirilen.

**Yönetilmeyen diskler**
* Premium depolama Solid-State sürücüler tarafından (SSD) ile yedeklenir ve hello disk hello kapasitesine dayalı olarak ücretlendirilir.
* Standart depolama normal dönen disk ile desteklenir ve hello kullanımda kapasite dayalı olarak ücretlendirilir ve depolama alanı kullanılabilirliği istenen.
  * RA-GRS, bu veri tooanother Azure bölgesi çoğaltılan hello bant genişliği için ek coğrafi çoğaltma veri aktarımı ücret yoktur.

Bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/) hello farklı depolama türlerini ve kullanılabilirlik seçenekleri hakkında bilgi fiyatlandırma için.

## <a name="availability-sets"></a>Kullanılabilirlik kümeleri
Bir kullanılabilirlik kümesi Azure toounderstand izin veren bir mantıksal VM'ler gruplandırmasıdır nasıl uygulamanızı tooprovide artıklık ve kullanılabilirlik için yerleşik olarak bulunur. İki veya daha fazla sanal makineleri yüksek oranda kullanılabilir bir uygulama ve toomeet hello bir kullanılabilirlik kümesi tooprovide içinde oluşturulan önerilen [% 99,95 Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Tek bir VM'ye kullanırken [Azure Premium Storage](../articles/storage/common/storage-premium-storage.md), hello Azure SLA Plansız bakım olayları için geçerlidir. 

Bir kullanılabilirlik kümesi toosafely olması güncelleştirmelere izin vermek ve donanım arızalarına karşı korumaya iki ek gruplandırmaları oluşan uygulanan - hata etki alanları (FDs) ve etki alanları (UDs) güncelleştirin.

![Merhaba güncelleştirme etki alanı ve hata etki alanı yapılandırmasını kavramsal çizimi](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

Daha fazla bilgi edinebilirsiniz nasıl toomanage hello kullanılabilirliğini [Linux VM'ler](../articles/virtual-machines/linux/manage-availability.md) veya [Windows VM'ler](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Hata etki alanları
Hata etki alanı bir mantıksal Grup ortak bir güç kaynağını paylaşmasına temel alınan donanımın ve ağ anahtarı, bir şirket içi veri merkezi benzer tooa rafta. Bir kullanılabilirlik kümesi sanal makineleri oluştururken hello Azure platformu Vm'leriniz bu hata etki alanları arasında otomatik olarak dağıtır. Bu yaklaşım, olası fiziksel donanım hataları, ağ kesintileri veya güç kesintilerinin hello etkisini sınırlar.

### <a name="update-domains"></a>Güncelleme etki alanları
Bir güncelleştirme etki alanı, bakım uygulayabilir veya hello başlatılması temel alınan donanım mantıksal grubudur aynı anda. Bir kullanılabilirlik kümesi sanal makineleri oluştururken hello Azure platformu otomatik olarak Vm'leriniz bunlar arasında dağıtır güncelleştirme etki alanları. Bu yaklaşım, uygulamanızın en az bir örneğini sağlar hello Azure platformu uğradığında düzenli bakım olarak çalışan her zaman kalır. Merhaba sırasını güncelleştirme etki alanlarını yeniden başlatıldığı sırayla planlı bakım sırasında ilerleyebilirsiniz değil, ancak yalnızca tek bir güncelleştirme etki alanı, aynı anda yeniden başlatılıncaya kadar.

### <a name="managed-disk-fault-domains"></a>Disk hata etki alanlarını yönetilen
[Azure Yönetilen Diskler](../articles/virtual-machines/windows/faq-for-disks.md)’i kullanan sanal makineler, yönetilen kullanılabilirlik kümesi kullanılırken yönetilen disk hata etki alanları ile hizalanır. Tüm iliştirilmiş tooa VM hello içinde yönetilen disklerde hello bu hizalama sağlar aynı yönetilen disk hata etki alanı. Yönetilen bir kullanılabilirlik kümesinde yalnızca, yönetilen disklere sahip VM’ler oluşturulabilir. Yönetilen disk hata etki alanlarını Hello sayısı iki veya üç yönetilen disk hata etki alanlarını her bölge - bölgeye göre değişir.

![Yönetilen Disk FD’leri](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> hata etki alanlarını yönetilen kullanılabilirlik kümeleri için Hello sayısı değişir bölgeye göre - iki veya üç her bölge. Merhaba aşağıdaki tabloda hello numarasını bölge başına gösterir

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bu kullanılabilirlik toouse bundan böyle başlayabilir ve artıklık toobuild Azure ortamınıza özellikleri. En iyi uygulama bilgileri için bkz. [Azure kullanılabilirlik en iyi uygulamaları](../articles/best-practices-availability-checklist.md).

