# oVirt
oVirt（open Virtualization）是類似於VMware的vSphere，基於KVM(Kernel-based Virtual Machine)虛擬化技術的開源IaaS雲服務解決方案。
oVirt是Red Hat Enterprise Virtualization產品的基石，是RHEV的一個上游項目，新特性都是先在oVirt上開發，之後才會出現在企業版的產品中。

# oVirt的特性
- 能管理多個虛擬節點
- 多樣化的用戶接口，可以提供對數據中心各種各樣的管理
- 提供在Host上創建虛擬機的多種選擇：manual, “optimised”, pinned 
- 虛擬機的動態遷移，從一個Hypervisor到另一個Hypervisor 
- 簡單並集中增加新的Hypervisor節點
- 監測VMs的資源使用情況
- 管理資源的配額（storage, compute, network）
- 自助服務控制台提供簡單或高級的用例

# oVirt架構
![oVirt] (img2016.itdadao.com/d/file/tech/2016/12/14/it286478141122041.png)

Host:運行Hypervisor的Server，oVirt的Hypervisor是KVM 。

Agent and tools:運行在Host上的包括VDSM（Virtual Desktop Server Manager），QEMU和libvirt。這些工具提供了虛擬機、網路以及存儲的本地管理。

oVirt:一個oVirt環境的集中管理平台。它提供了一個圖形界面，以便查看，提供以及管理資源

Storage Domain:在上圖中並沒有顯示出來，在RHEV的架構圖中是有這個組件的，它保存虛擬資源如：VM，templates, ISOs等。

A database:用來跟踪環境的狀態變化，這裡用PostgreSQL，OpenStack中默認使用MySQL。

提供外部的Directory Server的訪問，以此來提供用戶以及授權。

網絡用來將整個環境連接在一起，包括物理網絡連接和邏輯網絡。


# oVirt由兩部分組成
客戶端 ovirt-node 類似於 vmware esxi，是由fedaro 16訂制而成。也可以在linux系統上安裝vdsm服務而得到一個ovirt客戶端。
管理端 overt-engine 類似於 vmware vcenter，但是是基於web頁面的。

# 標準的oVirt平台包含三部分：

ovirt-engine：主要用於(批量)部署，監聽，導入/導出，開關機，遷移，創建虛擬機和配置存儲/網絡等。
ovirt-nodes：物理服務器，虛擬化軟件和虛擬機都運行在上面。
storage-nodes：存儲節點，主要存儲虛擬機的鏡像和ISOs。

# ovirt-node 
ovirt-node 是開源社區oVirt 的一個開源項目，它是基於KVM 和Linux 技術的一套最小化的Linux 系統，它只提供最基本的操作系統功能以及虛擬機管理等。

簡單地說ovirt-node 是一個小的主機鏡像，該鏡像提供libvirt/vdsm(Virtual Desktop Server Manager) 和KVM(Kernel based virtual machine) 等，虛擬化服務，使用libvirt/vdsm 管理KVM 虛擬機。

ovirt-node 與普通的linux 發行版的區別在於,ovirt-node 專注於提供虛擬化功能，它只包含了最小化的操作系統所需要的軟件和虛擬機管理軟件, 大約只有200 多個rpm 安裝包；具備良好管理界面的API。相比於普通的Linux 發行版，ovirt-node 的只需要一個很小的運行環境，其安裝鏡像小於150M，安裝到磁盤空間也只有不到1G，運行時存儲器僅需500M，另外，也可以根據需求定制虛擬機管理軟件，如libvirt/VDSM。

正因為ovirt-node 是基於minimal fedora 系統進行定制化的，所以使得ovirt-node 的安裝鏡像很小，除了需要安裝一些必要的系統管理軟件，網絡管理軟件等，還需要包含kvm 模塊，一起管理kvm的libvirt 或VDSM 等。因此，完全可以忽略由於運行ovirt-node 帶來的資源的開銷，從而，可以將更多的資源分配給節點中的虛擬機。
![ovirt-note](http://www.ibm.com/developerworks/cn/linux/l-cn-ovirt/image001.jpg)


# 總結
oVirt 是一個開源的虛擬化平台，目前持續在開發與解決軟體細節問題，是在未來開源虛擬化管理平台的一項好工具。
