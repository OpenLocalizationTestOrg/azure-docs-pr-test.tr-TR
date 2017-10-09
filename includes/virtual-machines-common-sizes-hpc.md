<!-- A-series - compute-intensive instances, H-series -->

Merhaba A8-A11 ve H-serisi boyutları olarak da bilinir: *işlem yoğunluklu örnekler*. Bu boyutlar çalıştıran hello donanım tasarlanmış ve işlem yoğunluklu için en iyi duruma getirilmiş ve ağ kullanımı yoğun uygulamalar, yüksek performanslı bilgi işlem (HPC) dahil olmak üzere uygulamalar, model ve benzetimleri küme. Merhaba A8-A11 serisi Intel Xeon E5-2670 2.6 GHZ @ ve Intel Xeon E5-2667 v3 3,2 GHz @ hello H-serisi kullanır. 

Azure H-serisi sanal makine VM'ler molecular modelleme ve hesaplama sıvı dinamiği gibi yüksek son hesaplama gereksinimlerine yönelik hello İleri nesil yüksek performanslı bilgi işlem yok. Bu 8 ila 16 vCPU VM'ler DDR4 bellek bulunduğu hello Intel Haswell E5-2667 V3 işlemci teknolojisine yerleşiktir ve geçici depolama SSD tabanlı. 

Ayrıca toohello önemli ölçüde CPU gücü hello H-serisi FDR InfiniBand ve birkaç bellek yapılandırmaları toosupport bellek yoğun hesaplama gereksinimleri kullanarak düşük gecikme süresi RDMA ağ için çeşitli seçenekler sunar.



## <a name="h-series"></a>H Serisi

ACU: 290-300

| Boyut | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum veri diskleri | Maksimum diski aktarım hızı: IOPS | En fazla NIC |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1000 |16 |16x500 |2  |
| Standard_H16 |16 |112 |2000 |32 |32x500 |4 |
| Standard_H8m |8 |112 |1000 |16 |16x500 |2  |
| Standard_H16m |16 |224 |2000 |32 |32x500 |4  |
| Standard_H16r* |16 |112 |2000 |32 |32x500 |4  |
| Standard_H16mr* |16 |224 |2000 |32 |32x500 |4 |

*MPI uygulamaları için, adanmış RDMA arka uç ağı ultra düşük gecikme süresi ve yüksek bant genişliği sağlayan FDR InfiniBand ağı tarafından etkinleştirilir.

<br>



## <a name="a-series---compute-intensive-instances"></a>A Serisi - Yoğun işlem gücü kullanımlı örnekler

ACU: 225

| Boyut | Sanal işlemci | Bellek: GiB | Geçici depolama (HDD): GiB | Maksimum veri diskleri | Maksimum veri diski aktarım hızı: IOPS | En fazla NIC|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16x500 |2 |
| Standard_A9* |16 |112 |382 |16 |16x500 |4 |
| Standard_A10 |8 |56 |382 |16 |16x500 |2  |
| Standard_A11 |16 |112 |382 |16 |16x500 |4 |

*MPI uygulamaları için, adanmış RDMA arka uç ağı ultra düşük gecikme süresi ve yüksek bant genişliği sağlayan FDR InfiniBand ağı tarafından etkinleştirilir.

<br>



