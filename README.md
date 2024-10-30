# Configuración inicial de sistemas con Ansible

Automatización de configuraciones iniciales mediante ansible.
Este es un repositorio con algunos archivos de configuración para evitar tener que configurar cada vez aplicaciones comunes.


## Instalar ansible

```bash
sudo apt-get install ansible
```

## CLONAR EN CARPETA TOOLS
Para que este proyecto funcione se debe clonar dentro de la carpeta **$HOME/git/tools** ya que algunos archivos de configuración utilizan rutas absolutas.

## Ejecución Local

```bash
ansible-playbook -i ansible.cfg local.yml
```

Si ese script no se utiliza desde root descomentar las opciones `become: true` para para que realice la instalación como sudo.

```bash 
ansible-playbook -i ansible.cfg local.yml --user=angel --extra-vars "ansible_sudo_pass=1234"
```

## Roles
Se crean lo siguientes roles.

### commons
Instala paquetes que son usualmente requeridos.

* vim

### git-tools
Instala Scripts que son utiles para la generación de archivos git

* gitignoregen
* gitattributesgen

Realiza configuraciones de git. Para esto configurar las variables en `local.yaml`

```yaml
vars:
    git_user_name: "Miguel Olave"
    git_user_email: "molavec@gmail.com"
    git_ui_color: "True"
```



### node
Instala node

Tasks:

* nodejs
* npm
* yarn

Handlers:

Se cambian las carpetas npm globales en el directorio Home
para evitar tener problemas con los premisos.

En computadores con multicuentas de desarrollador preferir carpeta
por defecto para modulos globales

Mas Info: http://npm.github.io/installation-setup-docs/installing/a-note-on-permissions.html

```bash
# define ubicación instalación modulos globales
npm config set prefix $HOME/.npm/node_modules
# define ubicación cache npm
npm config set cache $HOME/.npm/npm_cache
# añade carpeta $HOME/.npm/node_modules/bin al $PATH
echo '# binarios de node_modules \n[[ -d ~/.npm/node_modules/ ]] && path=("$HOME/.npm/node_modules/bin" $path)\n' > $HOME/.zshrc

```

**Nota:** Para gestionar veriones se puede utilizar nvm pero hay que instalarlo de forma manual. 

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

### Pasos finales de configuración
* Al finalizar el proceso de este rol, definir zsh como shell predefinida con 

```bash
chsh -s /usr/bin/zsh
```

* Los dotfiles están en `ansible/roles/zsh-config/files`

* Para que se pueda visualizar apropiadamente el shell se debe configurar en el terminal la fuente `MesloLGS NF Regular`.

* En Visual Studio Code Abrir `Preferencias -> Terminal -> font` colocar `MesloLGS-NF-Regular` o `"MesloLGS NF"` para utilizar esta fuente en el terminal