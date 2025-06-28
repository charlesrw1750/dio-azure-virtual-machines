# Projeto Azure - Gerenciamento de Máquinas Virtuais

Este projeto demonstra práticas essenciais no gerenciamento de máquinas virtuais no Microsoft Azure, com foco em alta disponibilidade, escalabilidade e operação sem interrupções. As etapas a seguir foram executadas em um ambiente de laboratório com duas máquinas virtuais em execução.

---

## 1. Criação de VM com Zona de Disponibilidade

Durante a criação das VMs, foi utilizada a opção de **Availability Zone** para garantir resiliência regional. As VMs `az104-vm1` e `az104-vm2` foram distribuídas entre as zonas 1 e 2 da região East US, garantindo que, em caso de falha em uma zona, a outra continue operando normalmente.

📍 *Região:* East US  
🔒 *Segurança:* Trusted launch VMs  
⚙️ *Imagem:* Windows Server 2019 Datacenter - Gen2  
🔁 *Zonas utilizadas:* 1 e 2

---

## 2. Alteração do Tamanho da VM (Disponibilidade)

Foi realizada a alteração do tamanho da VM `az104-vm1` para o tipo `Standard_DS1_v2`, mesmo com a máquina em execução. O Azure alerta que o processo pode causar reinicialização, o que foi aceito para fins de escalabilidade de recursos conforme a demanda.

📌 *Importante:* Redimensionar VMs exige parada momentânea do serviço (restart automático).

---

## 3. Adição e Remoção de Disco na VM (Hot Add)

Foi feita a adição de um novo disco de dados na VM `az104-vm1`, utilizando discos do tipo Premium SSD LRS.  
Essa operação foi realizada com a VM ligada (hot-add), garantindo continuidade dos serviços.

🔧 *Disco adicionado:* 127 GiB Premium SSD  
📈 *Max IOPS:* 500 | *Throughput:* 100 MB/s  
💡 *Host caching:* Read/Write  
🔒 *Criptografia:* SSE with PMK

---

## 4. Virtual Machine Scale Set (Alta Disponibilidade Horizontal)

Foi criado um **Scale Set** com as seguintes configurações:

- **Modo de orquestração:** Flexible (para suportar diferentes tipos de instância)
- **Tipo de segurança:** Trusted Launch
- **Modo de escalonamento:** Manual, com 2 instâncias
- **Zonas múltiplas habilitadas** para alta disponibilidade

Essa estrutura garante escalabilidade horizontal, permitindo a replicação das VMs com balanceamento de carga e alta disponibilidade em diferentes zonas.

---

## 5. Availability Set (Alta Disponibilidade de Hardware)

Para garantir tolerância a falhas de hardware, foi criado um **Availability Set** com:

- **2 Fault Domains:** separação física de recursos de energia e rede
- **5 Update Domains:** atualização em domínios distintos para evitar indisponibilidade

Essa estratégia garante que, mesmo durante falhas físicas ou atualizações planejadas, pelo menos uma instância da aplicação continue disponível.

---

## 🔧 Recursos Utilizados

- Microsoft Azure Portal
- Azure Compute
- Discos gerenciados (Managed Disks)
- Scale Sets e Availability Sets
- Zonas de disponibilidade
- Windows Server 2019

---

## 📷 Screenshots de Referência

1. Criação das VMs com zonas de disponibilidade
2. Alteração do tamanho da VM
3. Adição de disco a quente
4. Configuração de Scale Set
5. Configuração de Availability Set
6. Execução das VMs `az104-vm1` e `az104-vm2`

---

## ✅ Conclusão

Este projeto reforça a importância da **alta disponibilidade**, **resiliência** e **escalabilidade horizontal** em ambientes de produção no Azure, utilizando os recursos nativos da plataforma para manter serviços sempre operacionais.

