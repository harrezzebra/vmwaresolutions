---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-03"

---

# Zerto

Wenn Sie feststellen, dass ein vSphere ESXi-Host während der Korrekturphase nicht in den Wartungsmodus wechseln kann, kann es daran liegen, dass er von Zerto gestoppt wird. Wenn Sie Zerto seit der ersten Bereitstellung aktualisiert haben, führen Sie die folgenden Schritte aus, um dies zu korrigieren. Wenn Sie keine Aktualisierung vorgenommen haben, befolgen Sie die Anweisungen im Abschnitt [How to place a host with an associated VRA into maintenance mode](https://www.zerto.com/myzerto/knowledge-base/place-host-into-maintenance-mode-with-vra/).

1. Melden Sie sich bei der Zerto-Webbenutzerschnittstelle an.
2. Wählen Sie **Site Settings** im Dropdown-Menü aus.
3. Wählen Sie die Registerkarte **Policies** aus und stellen Sie sicher, dass **Allow Zerto to always enter hosts to maintenance mode during remediation** ausgewählt ist.
4. Melden Sie sich bei Zerto ab.

### Zugehörige Links

* [VMware HCX on IBM Cloud Solution](https://www.ibm.com/cloud/garage/files/HCX_Architecture_Design.pdf)
* [VMware Solutions on IBM Cloud Digital Technical Engagement](https://ibm-dte.mybluemix.net/ibm-vmware) (Demos)
