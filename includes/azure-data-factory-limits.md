Veri Fabrikası aboneliklerini birbirlerinin iş yüklerini korunan emin olmak için yerinde aşağıdaki varsayılan sınırları sahip çok kiracılı bir hizmettir. Birçok sınırları kolayca sınırına kadar aboneliğiniz için desteğe başvurarak yükseltilebilir.

| **Kaynak** | **Varsayılan Sınır** | **Üst Sınır** |
| --- | --- | --- |
| bir Azure aboneliğinizin Data factory'leri |50 |[Desteğe başvurun](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| data factory içinde komut zincirleri |2500 |[Desteğe başvurun](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| data factory içinde veri kümeleri |5000 |[Desteğe başvurun](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| veri kümesi başına eşzamanlı dilimleri |10 |10 |
| Ardışık Düzen nesneleri için nesne başına bayt <sup>1</sup> |200 KB |200 KB |
| veri kümesi için nesne ve bağlantılı hizmet nesneleri başına bayt <sup>1</sup> |100 KB |2000 KB |
| Bir abonelik içindeki Hdınsight isteğe bağlı küme çekirdeği <sup>2</sup> |60 |[Desteğe başvurun](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Bulut veri taşıma birimi <sup>3</sup> |32 |[Desteğe başvurun](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Yeniden deneme sayısı ardışık düzen etkinlik çalışması |1000 |MAXINT (32 bit) |

<sup>1</sup> ardışık düzeni, veri kümesi ve bağlantılı hizmet nesneleri temsil eden İş yükünüzün mantıksal bir gruplandırması. Bu nesneler için sınırları taşıyın ve Azure Data Factory hizmetiyle işlem veri miktarı ile ilgili değildir. Veri Fabrikası petabaytlarca verileri işlemek için ölçeklendirmek için tasarlanmıştır.

<sup>2</sup> isteğe bağlı Hdınsight çekirdek, veri fabrikası içeren abonelik dışında ayrılır. Sonuç olarak, yukarıdaki Data Factory isteğe bağlı Hdınsight çekirdek çekirdek sınırını zorunlu ve Azure aboneliğinizle ilişkili çekirdek sınırına farklıdır sınırlıdır.

<sup>3</sup> bulut veri taşıma birimi (DMU) bir Bulut Bulut kopyalama işleminde kullanılıyor. Veri Fabrikası'nda tek bir birimi (CPU, bellek ve ağ kaynağı ayırma birleşimi) gücünü temsil eden bir ölçüsüdür. Bazı senaryolar için daha fazla DMUs yararlanarak daha yüksek kopyalama verimlilik elde edebilirsiniz. Başvurmak [bulut veri taşıma birimleri](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) ayrıntıları bölümü.

| **Kaynak** | **Varsayılan alt sınırı** | **Alt sınırı** |
| --- | --- | --- |
| Zamanlama aralığı |15 dakika |15 dakika |
| Yeniden deneme girişimleri arasındaki aralığı |1 saniye |1 saniye |
| Zaman aşımı değeri yeniden deneyin |1 saniye |1 saniye |

### <a name="web-service-call-limits"></a>Web hizmeti çağrısı sınırları
Azure Resource Manager API çağrıları için sınırları vardır. İçinde bir hızda API çağrıları yapma [Azure Kaynak Yöneticisi API'si sınırlar](../articles/azure-subscription-service-limits.md#resource-group-limits).
