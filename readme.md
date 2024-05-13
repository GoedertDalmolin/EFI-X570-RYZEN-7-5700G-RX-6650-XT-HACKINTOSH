# (IN PROGRESS)

# Guia Hackintosh Asus Tuf X570-PLUS/BR + Ryzen 7 5700G + RX 6650 XT


# Resumo:

| Componente       | Versão                                     |
|------------------|--------------------------------------------|
| MacOS            | 14.4.1 (Sonoma)                            |
| OpenCorePkg      | [1.0.0](https://github.com/acidanthera/OpenCorePkg/releases/tag/1.0.0) |
| Motherboard      | Asus TUF Gaming X570-Plus/BR               |
| Bios             | [5013](https://www.asus.com/br/motherboards-components/motherboards/tuf-gaming/tuf-gaming-x570-plus-br/helpdesk_bios?model2Name=TUF-GAMING-X570-PLUS-BR) (2024/04/04)                                       |
| CPU              | AMD Ryzen 7 5700G                          |
| GPU              | AMD Radeon RX 6650 XT                      |


# Passo a Passo:

1 - Obter as especificações do computador

Separe componente por componente, cada hardware tem sua propria configuração.

Recomendo utilizar o software Aida64 Extreme.

No meu caso:

| Componente       | Modelo                                | Especificação                                                                              |
|------------------|---------------------------------------|--------------------------------------------------------------------------------------------|
| Motherboard      | Asus TUF Gaming X570-Plus/BR         | 3 PCI-E x1, 2 PCI-E x16, 2 M.2, 4 DDR4 DIMM, Audio, Video, Gigabit LAN                     |
| CPU              | AMD Ryzen 7 5700G                    | OctalCore 4519 MHz (45.75 x 99)                                                           |
| GPU              | AMD Radeon RX 6650 XT                | Navi 23 - 8176 MB                                                                          |
| Memory Ram       | 4x Asgard 8 GB DDR4-3200            | VMA45UG-MEC1U2AW2 SDRAM (18-22-22-42 @ 1600 MHz) (16-20-20-38 @ 1422 MHz)                 |
| Disk Drive | CUSO CSN 500 NVMe M.2                | M.2/80 - 465 GB                                                                            |
| Audio Adapter    | Realtek S1200A                       |                                                                                            |
| Network Adapter  | Realtek® L8200A (LAN Turbo LAN Utility) | Realtek Gaming GbE Familly Controller                                                                                         |

2 - Atualizar a BIOS:

É extremamente recomendado que atualize a bios, uma vez que sempre é liberado novas atualizações com correções de erros e proteções aos componentes.

Baixe a bios no site oficial da Asus - [Download Here](https://www.asus.com/br/motherboards-components/motherboards/tuf-gaming/tuf-gaming-x570-plus-br/helpdesk_bios?model2Name=TUF-GAMING-X570-PLUS-BR).

No meu caso eu atualizei a Bios para a versão 5013 (2024/04/04).

# 3 - Configurar Parametros da BIOS:

Recomendo resetar as configurações da Bios e seguir este passo a passo.

Open Bios >> Default Option or Press F5.

Restart PC.

# Disable Bios Config
- Advanced Mode (F7) >> Boot >> Fast Boot = Disabled.
- Advanced Mode (F7) >> Boot >> Secure Boot >> OS Type = Other OS (This disable secure boot).
- Advanced Mode (F7) >> Advanced >> PCI Subsystem Settings >> Resize Bar Suport = Disabled.
- Advanced Mode (F7) >> Advanced >> Onboard Devices Configuration >> Serial Port Configuration >> Serial Port = Disabled.
- Advanced Mode (F7) >> Boot >> CSM (Compatibillity Support Module) >> Launch CSM = Disabled.


# Enable Bios Config
- Advanced Mode (F7) >> Advanced >> PCI Subsystem Settings >> Above 4G Decoding = Enabled.
- Advanced Mode (F7) >> Advanced >>  USB Configuration >> XHCI Hand-Off = Enabled.
- Advanced Mode (F7) >> Advanced >> SATA Configuration >> Sata Mode = AHCI.


(Optional to Force Memory Ram use 3200MHz)
- Advanced Mode (F7) >> Ai Tweaker >> Ai Overclock Tuner = D.O.C.P.
- Advanced Mode (F7) >> Ai Tweaker >> D.O.C.P. = DDR4-3200.


Save Changes & Exit (F10).

# Ferramentas Necessarias

- [Python 3.12.3](https://www.python.org/downloads/) (Obs: Add Python to Path)
- [ProperTree 0.2.9](https://github.com/corpnewt/ProperTree)
- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
- [iASL Compiler Windows Binary Tools](https://www.intel.com/content/www/us/en/developer/topic-technology/open/acpica/download.html).



# Kexts Necessarias (Release Only)
Baixe as Seguintes Kexts:

| Nome                                    | Versão | Descrição                                                                                                                                                                                  |
|-----------------------------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [AMD Ryzen CPU Power Management](https://github.com/trulyspinach/SMCAMDProcessor/releases)          | 0.7.2  | Para o AMD Power Gadget.                                                                                                                                                                   |
| [SMC AMD Processor](https://github.com/trulyspinach/SMCAMDProcessor/releases)                      | 0.7.2  | Para o AMD Power Gadget.                                                                                                                                                                   |
| [Apple MCE Reporter Disabler](https://github.com/acidanthera/bugtracker/files/3703498/AppleMCEReporterDisabler.kext.zip)            | 1.2.0  | Useful starting with Catalina to disable the AppleMCEReporter kext which will cause kernel panics on AMD CPUs and dual-socket systems.                                                     |
| [Lilu](https://github.com/acidanthera/Lilu/releases)                                    | 1.6.7  | Para corrigir diversos processos e atua em paralelo com VirtualSMC WhateverGreen.                                                                                                                |
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases)                              | 1.3.2  | Emulates the SMC chip found on real macs, without this macOS will not boot. Alternative is FakeSMC which can have better or worse support, most commonly used on legacy hardware. |
| [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases)                           | 1.6.6  | Used for graphics patching, DRM fixes, board ID checks, framebuffer fixes, etc; all GPUs benefit from this kext.                                                                          |
| [Apple ALC](https://github.com/acidanthera/AppleALC/releases/tag/1.9.0)                               | 1.9.0  | Para funcionar o som do dispositivo.                                                                                                                                                      |
| [RTL8111_driver_for_OS_X](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases)                | 2.4.2  | Para corrigir erros da placa de rede e internet.                                                                                                                                          |
| [NVMe Fix](https://github.com/acidanthera/NVMeFix/releases)                               | 1.1.1  | Para corrigir erros de gerenciamento de energia do ssd nvme.                                                                                                                              |
| [RestrictEvents](https://github.com/acidanthera/RestrictEvents/releases)                         | 1.1.3  | Para corrigir erros do processador.                                                                                                                                                       |
| [SMCRadeonSensors](https://github.com/ChefKissInc/SMCRadeonSensors/releases)                       | 2.0.0  | Para corrigir obter dados da temperatura da placa de video.                                                                                                                               |
| [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock/releases)                            | 1.1.5  | Para desbloquear conteudos como Sidecar, NightShift, AirPlay, Universal Control and Continuity Camera support dentro do MacOS.                                                             |


# Open Core Pkg

Faça download da versão release 1.0.0 do [OpenCore](https://github.com/acidanthera/OpenCorePkg/releases/tag/1.0.0).

Copiando a pasta base do OpenCore

- Extraia o arquivo: OpenCore-1.0.0-RELEASE.
- Acesse: "OpenCore-1.0.0-RELEASE\X64".
- Copie a pasta "EFI" e cole em outro lugar.

Copiando o config.plist base:

- Acesse: "OpenCore-1.0.0-RELEASE\Docs".
- Copie o arquivo: Sample.plist.
- Acesse a pasta "EFI" que salvamos anteriormente.
- Acesse: "/OC/".
- Cole o arquivo e renomeie para "config.plist".


Colocando as Kexts necessarias dentro da EFI:

- Copie todas as kexts que baixamos e extraimos anteriormente.
- Acesse dentro da nossa EFI: "EFI\OC\Kexts".
- Cole todas as kexts lá dentro.

No final você tera o seguinte resultado:

![Arquivos Kext](.github/pasta-kexts.png)


# Gerando o dump das ACPIs do seu computador

- Acesse a pasta iasl que baixamos anteriormente la nas ferramentas.
- Abra o terminal nesse diretório como administrador.
- Execute o seguinte comando: "acpidump.exe -b -n DSDT -z"
- Note que no mesmo diretório foi gerado o arquivo "dsdt.dat".
- Renomeie esse arquivo para: "Asus-X570-Tuf-5013.aml".
- Copie e cole esse arquivo dentro da nossa EFI no caminho: "EFI\OC\ACPI".

# Atualizando a EFI com as novas Kexts/ACPI

- Abra o ProperTree: "ProperTree-master\ProperTree.bat".
- Acesse: File > Open > Selecione o config.plist dentro de "EFI\OC\config.plist".
- Busque por SecureBootModel e mude para Disabled.
- Busque por XhciPortLimit e mude para true.
- Busque por SetupVirtualMap e mude para false.
- Busque por ProvideCurrentCpuInfo e mude para true.

# Mapeando os cores do processador

Este processo é exclusivo para maquinas com amd.

Acesse a pagina dos patchs para mapear os [cores](https://github.com/AMD-OSX/AMD_Vanilla).

Baixe apenas o arquivo [patches.plist](https://github.com/AMD-OSX/AMD_Vanilla/blob/master/patches.plist).

Abra esse arquivo baixado com o ProperTree.
Copie todos os filhos encontrados no "Patch" dentro de "Kernel".
Cole dentro de sua EFI no arquivo config.plist no mesmo caminho anterior "Patch" e "Kernel".

Após isso encontre os 4 filhos de "Patch" com o comentario algrey - Force cpuid_cores_per_package.

E substitua o valor do campo Replace para o indicado na [documentação](https://github.com/AMD-OSX/AMD_Vanilla?tab=readme-ov-file#read-me-first) conforme seu processador.

Lembre de salvar apos alterar cada registro.

# Adicionando suporte a GPU

- Abra o arquivo "config.plist" da sua EFI com o ProperTree.
- Acesse: Root > NVRAM > Add > (Key com final "...9F82) >> boot-args
- Insira agdpmod=pikera.

O boot args deve ficar dessa forma: "-v keepsyms=1 agdpmod=pikera"

- Dentro do config.plist execute o File > OC Clean SnapShot.
- Salve e feche o arquivo.


# Removendo arquivos desnecessarios da EFI
Acesse a pastas Drivers no caminho: "EFI\OC\Drivers"

- Apague o arquivo "OpenVariableRuntimeDxe.efi".
- Apague o arquivo "OpenUsbKbDxe.efi".

- Abra o ProperTree: "ProperTree-master\ProperTree.bat".
- Alterar o Misc > Boot > Picker Mode > External.
- Alterar o Misc > Security > Valut > Optional.
- Alterar o Misc > Boot > HideAuxiliary > False.
- Alterar o Misc > Boot > PollAppleHotKeys > True;

Por fim:
- Acesse: File > Open > Selecione o config.plist dentro de "EFI\OC\config.plist".
  
# SSDT Time

Abra o SSDT Time.
- Insira a letra: P (Dump DSDT) e pressione Enter.
- Insira o numero: 1 (Fix HPET) e pressione Enter até voltar ao menu novamente.
- Insira o numero: 2 (Fake EC) e pressione Enter até voltar ao menu novamente.
- Insira o numero: 4 (USB X) e pressione Enter até voltar ao menu novamente.
- Insira o numero: 5 (Plugin Type) e pressione Enter até voltar ao menu novamente.
- Insira o numero: 7 (RTCAWAC) e pressione Enter até voltar ao menu novamente.
- Insira o numero: 8 (USB Reset) e pressione Enter até voltar ao menu novamente.

Por fim:
- Insira a letra: q (Quit) e pressione Enter para sair.

Acesse a pasta "Results" no caminho "SSDTTime-master\Results":
- Copie todos os arquivos com o final ".aml";
- Cole os arquivos dentro da sua EFI no caminho: "EFI\OC\ACPI";

Novamente dentro da pasta "Results" no caminho "SSDTTime-master\Results":
- Abra o arquivo "patches_OC.plist" com o ProperTree.
- Copie as tags Patch e Delete (Caso existir) para o seu config.plist no mesmo lugar.
- Dentro do config.plist execute o File > OC Clean SnapShot.
- Salve e feche o arquivo.

# GenSMBios

- Abra o GenSMBios.
- Insira o numero: 2 (Select config.plist) e pressione enter.
- Arraste o seu arquivo config.plist para dentro da janela do terminal.
- Pressione Enter.
- Insira o numero: 3 (Generate SMBIOS) e pressione enter.
- Insira o seguinte texto: iMacPro1,1
- Pressione Enter

Por fim:
- Insira a letra: q (Quit) e pressione Enter para sair.

# Verificando se o config.plist está correto
- Acesse o seguinte caminho da release baixada do open core: "OpenCore-1.0.0-RELEASE\Utilities\ocvalidate"
- Abra o terminal nesse diretório.
- Insira o seguinte comando: "ocvalidate "CAMINHO-CONFIG.PLIST""
- Substitua "CAMINHO-CONFIG.PLIST" pelo caminho do arquivo config.plist.

# Baixando a Imagem de Recovery do MacOS

Dentro da pasta do OpenCore que extraimos anteriormente existe uma ferramenta para isso.
- Portanto acesse o caminho: "OpenCore-1.0.0-RELEASE\Utilities\macrecovery";
- Abra o terminal nesse diretório.
- Execute o seguinte comando para baixar o sonoma: "python ./macrecovery.py -b Mac-A61BADE1FDAD7B05 -m 00000000000000000 download"

Obs: Caso queira outras versões obtenha o comando por meio do arquivo: "recovery_urls.txt".

# Gerando o Pendrive Bootavel

- Copie sua EFI na qual configurou anteriormente para dentro do Pendrive desejado.
- Copie a pasta "com.apple.recovery.boot" contendo a imagem do mac recovery.
- Cole a pasta copiada no diretorio do seu Pendrive.

Seu pendrive por fim deve conter o seguinte:


![Arquivos Pendrive](.github/arquivos-pendrive.png)

# Realizando o FakeId da GPU não suportada

Faça o download da [SSDT-BRG0.aml](https://github.com/luchina-gabriel/youtube-files/blob/main/Fake-GPUID.zip)

# Referencias:
- [OpenCore Official Guide](https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html).
- Youtube Channel: [Universo Hackintosh](https://www.youtube.com/@UniversoHackintosh)
- Github Repository: [Guide to Install MacOS on Ryzen Setup](https://github.com/luchina-gabriel/BASE-EFI-AMD-RYZEN-THREADRIPPER-PUBLIC)
- Discord Server: [Universo Hackintosh](https://discord.com/invite/VYugKNbUqz)




  
