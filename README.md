# Configuración inicial de sistemas con Ansible

Automatización de configuraciones iniciales mediante ansible.
Este es un repositorio con algunos archivos de configuración para evitar tener que configurar cada vez aplicaciones comunes.

**Nota Importante:** Este proyecto funcione debe estar **$HOME/git/tools** para que funcione

## Instalar ansible

```bash
sudo apt-get install ansible
```

## Ejecución Local

```bash
ansible-playbook -i ansible.cfg local.yml
ansible-playbook -i ansible.cfg local.yml --user=angel --extra-vars "ansible_sudo_pass=1234"
```

## Roles
Se crean lo siguientes roles.

### Commons
Instala paquetes que son usualmente requeridos.

* vim

### git-tools
Instala Scripts que son utiles para la generación de archivos git.

* gitignoregen
* gitattributesgen

### video-tools
Instala scripts que son útiles para la edición de video con ffmpeg.

* avi2mp4
* mp4concat
* mp4splitter
* video2gif

### zsh-config
Instala archivos de configuración con [zsh](https://www.zsh.org) + [prezto](https://github.com/sorin-ionescu/prezto) + [powerlevel10k](https://github.com/romkatv/powerlevel10k)

Algunas recomendaciones que se siguen para esta configuración:

 * las variables de entornos se configuran en el archivo `.zshrc`
 * los alias se configuran en el archivo `.zshrc`
 * la configuración del estilo se define mediante `powerlevel10k`
 * los modulos y extensiones de manejan con `prezto`

**Nota:** Al finalizar el proceso de este rol, definir zsh como shell predefinida con `chsh -s /usr/bin/zsh`
**Nota:** Los dotfiles están en `ansible/roles/zsh-config/files`
**Nota:** Para que se pueda visualizar apropiadamente el shell se debe configurar en el terminal la fuente `MesloLGS NF Regular`.