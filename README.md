# IRPF 2021 - Flatpak

## Abstract

[APP IN DEVELOPMENT]

Project to make possible to distribute the app Declaração do Imposto de Renda (IRPF 2021) on Flathub, making installation easier for a Linux distribution user.

This project is not linked to the official source of the program

As the app Declaração do Imposto de Renda is available in Brazilian Portuguese (pt-br) language and its main target is Brazilians, from now on this project description will be written in pt-br.

## Resumo
[APLICATIVO EM DESENVOLVIMENTO]

Projeto para tornar possível a distribuição da aplicação Declaração do Imposto de Renda (IRPF 2021) no Flathub, dando praticidade à instalação a um usuário de distribuição Linux.

Este projeto não é ligado a fonte oficial do programa

Como o progama Declaração do Imposto de Renda se encontra em português do Brasil (pt-br) e seu maior público alvo são os brasileiros, daqui em diante sua descrição seguirá nesta língua.

## Aviso Legal
A Receita federal do Brasil, SERPRO ou qualquer outra entidade governamental não possui qualquer envolvimento no desenvolvimento desta solução.

O software não possui garantia de qualquer tipo. [Mais informações (Licença)](https://github.com/farribeiro/irpf-flatpak/blob/master/LICENSE).

Espera-se que o usuário entenda como o programa funciona e confie no método e tecnologias utilizadas. 

## Objetivos  

**Objetivo geral:** 
Disponibilizar este app futuramente no flathub, para um maior alcance e facilidade para o cidadão brasileiro que utiliza Linux

**Objetivos específicos**  
Este projeto se propõe a automatizar o processo manual de um usuário comum:
- Instalar o ambiente Java, necessário para sua execução
- Baixar o instalador da aplicação IRPF de [fonte oficial](https://www.gov.br/receitafederal/pt-br/centrais-de-conteudo/download/pgd/dirpf)
- Realizar a Instalação
- Realizar a Execução

Enquanto isso:
- Manter o isolamento (sandboxing) da execução do programa ao sistema, de forma viável. 
- Utilizar o máximo de soluções de código aberto
- Não exigir privilégio de administrador durante a instalação e execução

## Requisitos

- Ter o flatpak instalado
- Certificar que o repositório do flathub esteja adicinado. Para esta etapa, caso já não esteja, talvez seja necessário perfil de administrador
```
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
- Possuir internet no momento da instalação
- Possuir internet no momento de envio do documento para o governo

## Instalação

Para estas etapas não é necessário perfil de administrador
```
# Instalar runtime do container
flatpak install flathub runtime/org.freedesktop.Platform//20.08

# Instalar SDK e extensão responsável pelo ambiente java
flatpak install flathub org.freedesktop.Sdk//20.08
flatpak install flathub org.freedesktop.Sdk.Extension.openjdk11//20.08

# entrar na pasta em que ficará o projeto (pode ser modificada)
cd ~/Dowmloads

# criar cópia do projeto localmente
git clone https://github.com/farribeiro/irpf-flatpak.git

# entrar na pasta do projeto
cd irpf-flatpak

# realizar instalação local do app
flatpak-builder --user --install --force-clean build-dir br.gov.rfb.irpf.yml
```

## Execução

- Utilizar as opções disponíveis de lançamento de programas da sua distriuição  
ou 
- Executar no terminal:
```
flatpak run br.gov.rfb.irpf 
```

## Observações

- Não foi encontrada nenhuma informação pública sobre as regras de distribuição da aplicação Declaração do Imposto de Renda. Portanto até que se tenha resposta, o aplicativo não será publicado no flathub.

- Por padrão o aplicativo apenas possui acesso a pasta `~/ProgramasRFB` fora do contêiner. É possível modificar este comportamento manualmente após instalado, utilizando o comando `flatpak override` ou ferramentas como o [FlatSeal](https://flathub.org/apps/details/com.github.tchx84.Flatseal).


- Para maiores informações sobre o funcionamento do app, verifique o [manifest](https://github.com/farribeiro/irpf-flatpak/blob/master/br.gov.rfb.irpf.yml) em conjunto com a [documentação do flatpak](https://docs.flatpak.org/)

