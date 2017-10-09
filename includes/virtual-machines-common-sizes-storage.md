
Merhaba Ls-serisi Cassandra, MongoDB, Cloudera dahil olmak üzere NoSQL veritabanları gibi düşük gecikme süresi geçici depolama gerektiren ve Redis iş yükleri için optimize edilmiştir. Merhaba Ls-serisi sunar hello kullanarak too32 Vcpu'lar [Intel® Xeon İşlemci E5 v3 ailesi](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html). Merhaba Ls-serisi alır aynı CPU performans G/GS serisi hello gibi hello ve bellek vCPU başına 8 Gib'den ile birlikte gelir.  

## <a name="ls-series"></a>Ls serisi

ACU: 180-240
 
| Boyut          | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum veri diskleri | Maksimum önbelleğe alınmış ve geçici depolama aktarım hızı: IOPS-MB/sn (önbellek boyutu GiB biriminde) | Maksimum önbelleğe alınmamış disk aktarım hızı: IOPS-MB/sn | Maks NIC / Beklenen ağ performansı (Mbps) | 
|---------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standart_L4s  | 4    | 32   | 678   | 8              | Yok / Yok (0)          | 5000/125                               | 2 / 4000       | 
| Standart_L8s  | 8    | 64   | 1,388 | 16             | Yok / Yok (0)          | 10.000/250                              | 4 / 8000  | 
| Standart_L16s | 16   | 128  | 2,807 | 32             | Yok / Yok (0)          | 20.000/500                              | 8 / 6000 - 16000 &#8224; | 
| Standard_L32s* | 32 | 256  | 5,630 | 64             | Yok / Yok (0)          | 40.000/1000                            | 8 / 20000 | 
 

Merhaba en fazla disk verimlilik Ls-serisi VM'ler ile mümkün olabilir hello sayısı, boyutu ve şeritleme herhangi biri tarafından sınırlandırılır bağlı diskler. Ayrıntılar için bkz. [Premium Depolama: Azure sanal makine iş yükleri için yüksek performanslı depolama](../articles/storage/common/storage-premium-storage.md). 

* Yalıtılmış toohardware ayrılmış tooa tek müşteri örneğidir.

