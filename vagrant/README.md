# Vagrant
> Arquivos para configuração da demo usando o Vagrant.

## Requisitos

Para usar, é necessário ter instalado:

* vagrant
* virtualbox

E estar em um *host* Linux.

## Como usar
Para criar a máquina virtual, executar (dentro do diretório `vagrant/`):
```bash
vagrant up
```

Após alguns minutos, a máquina vai estar criada e configurada.   
Para acessar a máquina, execute:

```bash
vagrant ssh
```

## Cleanup
Para remover a máquina virtual criada:
```bash
vagrant destroy
```