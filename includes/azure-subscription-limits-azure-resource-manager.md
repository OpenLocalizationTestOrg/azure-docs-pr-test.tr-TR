| Kaynak | Varsayılan Sınır | Üst Sınır |
| --- | --- | --- |
| [Abonelik](../articles/billing-buy-sign-up-azure-subscription.md) başına VM |Bölge başına 10.000 <sup>1</sup> |Bölge başına 10.000 |
| [Abonelik](../articles/billing-buy-sign-up-azure-subscription.md) başına toplam VM çekirdeği sayısı |Bölge başına 20<sup>1</sup> | Desteğe başvurun |
| Bir [abonelikteki](../articles/billing-buy-sign-up-azure-subscription.md) seri (Dv2, F vb.) çekirdeği başına VM |Bölge başına 20<sup>1</sup> | Desteğe başvurun |
| Abonelik başına [ortak yönetici](../articles/billing-add-change-azure-subscription-administrator.md) sayısı |Sınırsız |Sınırsız |
| Abonelik başına [depolama hesabı](../articles/storage/common/storage-create-storage-account.md) sayısı |200 |200<sup>2</sup> |
| Abonelik başına [Kaynak Grubu](../articles/azure-resource-manager/resource-group-overview.md) |800 |800 |
| Abonelik başına [Kullanılabilirlik Kümesi](../articles/virtual-machines/windows/manage-availability.md#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) |Bölge başına 2.000 |Bölge başına 2.000 |
| Resource Manager API'si Okuma İşlemleri |Saatte 15.000 |Saatte 15.000 |
| Resource Manager API'si Yazma İşlemleri |Saatte 1.200 |Saatte 1.200 |
| Resource Manager API'si istek boyutu |4.194.304 bayt |4.194.304 bayt |
| Abonelik başına etiket<sup>3</sup> |sınırsız |sınırsız |
| Abonelik başına benzersiz etiket hesaplaması<sup>3</sup> | 10,000 | 10,000 |
| Abonelik başına [bulut hizmeti](../articles/cloud-services/cloud-services-choose-me.md) sayısı |Uygulanamaz<sup>4</sup> |Uygulanamaz<sup>4</sup> |
| Abonelik başına [benzeşim grubu](../articles/virtual-network/virtual-networks-migrate-to-regional-vnet.md) sayısı |Uygulanamaz<sup>4</sup> |Uygulanamaz<sup>4</sup> |

<sup>1</sup>Varsayıla limitler Ücretsiz Deneme, Kullandıkça Öde gibi teklif Kategori Türüne ve Dv2, F, G vb. serilere göre farklılık gösterir.

<sup>2</sup>Buna hem Standart hem de Premium depolama hesapları dahildir. 200'den fazla depolama hesabı gerekiyorsa, [Azure Destek](https://azure.microsoft.com/support/faq/) üzerinden bir istek oluşturun. Hello Azure depolama ekibi iş durumunuz incelenecek ve too250 depolama hesapları onaylama.

<sup>3</sup>Abonelik başına sınırsız sayıda etiket uygulayabilirsiniz. Merhaba, kaynak veya kaynak grubu başına etiketleri sınırlı too15 sayısıdır. Kaynak Yöneticisi yalnızca döndüren bir [benzersiz etiket adı ve değerlerin listesi](/rest/api/resources/tags#Tags_List) etiketleri hello sayısı 10.000 veya daha az olduğunda hello Abonelikteki. Ancak, Hello 10.000 sayısını aştığında etikete göre kaynak hala bulabilirsiniz.  

<sup>4</sup>bu özellikleri artık Azure kaynak gruplarını ve hello Azure Resource Manager ile gereklidir.

> [!NOTE]
> Bölgesel toplam sınırı ve bunun yanı sıra ayrı olarak uygulanan (Dv2, F, vb.) serisi sınırına başına bir bölgesel sanal makine çekirdek sahip önemli tooemphasize olur.  Örneğin, Doğu ABD toplam VM çekirdek limiti 30, A serisi çekirdek limiti 30 ve D serisi çekirdek limiti 30 olan bir abonelik düşünün.  Bu abonelik, toodeploy 30 A1 VM'ler veya 30 D1 VM'ler izin ya da bir birleşimini hello iki tooexceed toplam 30 çekirdek (örneğin, 10 A1 VM'ler ve 20 D1 VM'ler).  
> <!-- -->
> 
> 

