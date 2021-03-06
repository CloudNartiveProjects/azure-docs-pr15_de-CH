<properties
   pageTitle="Problembehandlung bei Windows VM-Bereitstellung Classic | Microsoft Azure"
   description="Beim Erstellen eines neuen Windows virtuellen Computers in Azure klassische Bereitstellung Problembehandlung"
   services="virtual-machines-windows"
   documentationCenter=""
   authors="JiangChen79"
   manager="felixwu"
   editor=""
   tags="top-support-issue"/>

<tags
  ms.service="virtual-machines-windows"
  ms.workload="na"
  ms.tgt_pltfrm="vm-windows"
  ms.devlang="na"
  ms.topic="article"
  ms.date="09/06/2016"
  ms.author="cjiang"/>

# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-windows-virtual-machine-in-azure"></a>Klassische Bereitstellung Problembehandlung mit einen neuen Windows-Computer in Azure erstellen

[AZURE.INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-selectors-include.md)]

[AZURE.INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-classic-include.md)]

[AZURE.INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Collect Überwachungsprotokolle

Sammeln Sie zum Starten der Problembehandlung Überwachungsprotokolle zum Problem zugeordneten Fehler zu identifizieren.

In Azure-Portal klicken Sie auf **Durchsuchen** > **virtuellen Computer** > *der virtuellen Windows-Maschine* > **Settings** > **Audit-Protokolle**.

[AZURE.INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[AZURE.INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** Wenn das Betriebssystem Windows verallgemeinert ist und es hochgeladen oder mit der allgemeinen Einstellung erfasst sein nicht Fehler vorhanden. Ebenso ist das Betriebssystem Windows spezialisiert, übertragen und/oder mit der speziellen erfasst, und Fehler nicht.

**Hochzuladen Sie Fehler:**

**N<sup>1</sup>:** Wenn das Betriebssystem Windows verallgemeinert und als hochgeladen spezialisiert, erhalten Sie einen Bereitstellung Timeoutfehler mit VM OOBE Bildschirm fest.

**N<sup>2</sup>:** Ist das Betriebssystem Windows spezialisiert und ist als allgemeine hochgeladen erhalten Sie einen Bereitstellung Fehler mit der VM OOBE-Bildschirm hängen, da die neue VM mit den ursprünglichen Computernamen, Benutzernamen und Kennwort ausgeführt wird.

**Auflösung:**

Um diese Fehler zu beheben, laden Sie ursprüngliche VHD verfügbar auf-Prem, dieselbe Einstellung wie für das Betriebssystem (generalized/spezialisiert). Zum Hochladen verallgemeinert, denken Sie daran, Ausführen von Sysprep. Weitere Informationen finden Sie unter [Erstellen und Hochladen einer virtuellen Windows Server in Azure](virtual-machines-windows-classic-createupload-vhd.md) .

**Erfassen Sie Fehler:**

**N<sup>3</sup>:** Wenn das Betriebssystem Windows verallgemeinert und als werden spezialisiert, erhalten Sie einen Bereitstellung Timeoutfehler ist der ursprünglichen virtuellen nicht verwendbar gekennzeichnet ist als verallgemeinert.

**N<sup>4</sup>:** Ist das Betriebssystem Windows spezialisiert und werden als allgemeine erhalten Sie einen Bereitstellung Fehler, da die neue VM mit den ursprünglichen Computernamen, Benutzernamen und Kennwort ausgeführt wird. Die ursprüngliche VM ist nicht verwendbar ist gekennzeichnet spezialisierte.

**Auflösung:**

Um diesen Fehler zu beheben, löschen Sie das aktuelle Bild aus dem Portal und [von der aktuellen VHDs](virtual-machines-windows-classic-capture-image.md) dieselbe Einstellung wie für das Betriebssystem (generalized/spezialisiert)

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problem: Benutzerdefinierte / Gallery / Marketplace-Bild; Fehler beim Reservieren
Dieser Fehler tritt in Situationen, wenn neue VM-Anforderung an einen Cluster, die keinen verfügbaren Speicherplatzes gesendet wird für die Anfrage oder virtueller Speicher angefordert wird nicht unterstützt. Es ist nicht möglich, Serien VMs im gleichen Clouddienst mischen. So schlägt erstellen Sie einen neuen virtuellen Computer Größe wie der Cloud-Dienst unterstützt werden soll, Compute-Anforderung fehl.

Einen Fehler durch eine von zwei Situationen kann auftreten, je nach Nebenbedingungen Cloud-Dienst, mit den neuen virtuellen Computer erstellen.

**Ursache 1:** Cloud-Dienst zu einem bestimmten Cluster fixiert oder einer Gruppe verbunden und daher zu einem bestimmten Cluster standardmäßig fixiert. Neue computeressource anfordert, Gruppe versucht, im selben Cluster, in dem die vorhandenen Ressourcen befinden. Jedoch kann eines Clusters entweder nicht unterstützt die angeforderte VM-Größe oder nicht genügend Speicherplatz, wodurch ein Fehler. Dies gilt, ob neuen Ressourcen über einen neuen Clouddienst oder einen vorhandenen Cloud-Dienst erstellt werden.

**Lösung 1:**

- Neue Clouddienst erstellen und einen Bereich oder eine bereichsbasierte virtuelles Netzwerk zugeordnet.
- Erstellen Sie einen neuen virtuellen Computer im neuen Cloud-Dienst.
  Wenn Sie beim Erstellen eines neuen Cloud-Diensts einen Fehler erhalten, zu einem späteren Zeitpunkt wiederholen Sie oder ändern Sie den Bereich für den Clouddienst.

> [AZURE.IMPORTANT] Wenn einen neuen virtuellen Computer in einem vorhandenen Clouddienst erstellen möchten, aber konnte nicht und musste einen neue Cloud-Dienst für Ihren neuen virtuellen Computer erstellen können Sie Ihre virtuellen Computer im gleichen Clouddienst konsolidieren. Dazu löschen Sie VMs in der Cloud-Dienst und von Datenträgern im neuen Cloud-Dienst erfassen. Allerdings ist es wichtig zu bedenken, dass neue Cloud-Dienst hat einen neuen Namen und VIP, müssen Sie für alle Abhängigkeiten aktualisieren, die derzeit diese Informationen für den Cloud-Dienst.

**Ursache 2:** Cloud-Dienst ist ein virtuelles Netzwerk zu einer Gruppe Affinität verknüpft er beabsichtigt, einen bestimmten Cluster fixiert ist zugeordnet. Alle neuen computeressource anfordert, Gruppe sind daher versucht, im selben Cluster, in dem die vorhandenen Ressourcen befinden. Jedoch kann eines Clusters entweder nicht unterstützt die angeforderte VM-Größe oder nicht genügend Speicherplatz, wodurch ein Fehler. Dies gilt, ob neuen Ressourcen über einen neuen Clouddienst oder einen vorhandenen Cloud-Dienst erstellt werden.

**Lösung 2:**

- Erstellen eines neuen regionalen virtuelles Netzwerks.
- Erstellen Sie die neue VM in neues virtuelles Netzwerk.
- Mit neues virtuelles Netzwerk [vorhandenen virtuellen Netzwerk verbinden](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) . Weitere Informationen zu [regionalen virtuellen Netzwerken](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). Alternativ können Sie [Migrieren Affinität Gruppenbasierte virtuelle Netzwerk zu einem regionalen virtuellen Netzwerk](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), und erstellen Sie den neuen virtuellen Computer.

## <a name="next-steps"></a>Nächste Schritte
Wenn Probleme beim Starten von beendet Windows VM oder Ändern einer vorhandenen Windows-VM in Azure, finden Sie unter [Problembehandlung bei klassischen Bereitstellungsaspekte für Neustart oder das Ändern von vorhandenen Windows virtuellen Computer in Azure](windows/classic/virtual-machines-windows-classic-restart-resize-error-troubleshooting.md).
