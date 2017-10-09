



Hello Azure işlem birimi (ACU) tooprovide Azure SKU'ları üzerinde işlem (CPU) performans karşılaştırma bir şekilde hello kavramı oluşturduk. Bu büyük olasılıkla toosatisfy SKU olan kolayca tanımlamanıza yardımcı olur, performans gereksinimlerinizi.  ACU şu anda Küçük (Standard_A1) VM'de 100 olarak standart haline getirilmiş ve diğer tüm SKU'lar, standart bir karşılaştırmalı testte sunabilecekleri yaklaşık hıza göre derecelendirilmiştir. 

> [!IMPORTANT]
> Merhaba ACU yalnızca bir kılavuz olarak sağlanmıştır.  iş yükü Hello sonuçları değişebilir. 
> 
> 

<br>

| SKU Ailesi | ACU \ vCPU |
| --- | --- |
| [A0](../articles/virtual-machines/windows/sizes-general.md) |50 |
| [A1-A4](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A5-A7](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A1_v2-A8_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A2m_v2-A8m_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A8-A11](../articles/virtual-machines/windows/sizes-hpc.md) |225* |
| [D1-D14](../articles/virtual-machines/windows/sizes-general.md) |160 |
| [D1_v2-D15_v2](../articles/virtual-machines/windows/sizes-general.md) |210-250* |
| [DS1-DS14](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160 |
| [DS1_v2-DS15_v2](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |210-250* |
| [D_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [Ds_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [E_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [Es_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [F1-F16](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [F1s-F16s](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [G1-G5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180-240* |
| [GS1-GS5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180-240* |
| [H](../articles/virtual-machines/windows/sizes-hpc.md) |290-300* |
| [L4s L32s](../articles/virtual-machines/windows/sizes-storage.md) |180-240* |
| [M](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) | 160-180** |

İle işaretlenen ACUs bir * Intel® Turbo teknolojisi tooincrease CPU sıklığı kullanın ve performans artışı sağlar.  Merhaba hello artırma miktarı hello VM boyutu, iş yükü ve hello üzerinde çalışan diğer iş yüklerini göre değişebilir aynı ana bilgisayar.

** Hiper iş parçacığı. 
