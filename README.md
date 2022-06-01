**Configuração do Ambiente de Desenvolvimento**
**Lucas Sleyder Machado Dicencio - 11911EAU023**

    Configuração do ambiente para primeiros passos de funcionamento e depuração de um **STM32F411 Blackpill**, tudo isso levando em conta o sistema **Cortex-M**. Ao fim para a conferir o funcionamento do mesmo, será feito o LED do kit de desenvolvimento piscar.

- Roteiros A e B

    Configurado o ambiente de Windows Subsystem for Linux 2, havia instalado uma primeira versão antes e foi necessario atualização do mesmo, após isso, foi configurado compilador GCC e o git, após isso foi configurado a toolchain, por fim foi instalado o depurador OpenOCD e as ferramentas da st. Para realizar o reconhecimento do ST Link foi instalado o USBIP no WSL e o mesmo foi conectado no computador para fazer sua configuração no subsystem.

- Lab 02
    
    **main.c**

    Responsavel para setar o estado de clock do **GPIOC**, portanto assim que escolhido o pino do LED, que neste caso foi o pino **PC13**, foi consultado o datasheet para definir o endereço do registrador que é responsável por habilitar a porta. 

    Com o pino **PC13** habilitado, foi colocado no main, a função dentro do laço que realiza o set e o reset no pino que faz o LED piscar. 

    **Makefile**

    Parte do main.c é sua compilação, para facilitar o processo, o **Makefile** é responsável por automatizar o processo com diversas ferramentas. Para o basico é preciso escolher um target, prerequisites e recipe. Recipe sendo a linha de código responsável pela compilação, o target o arquivo gerado e o prerequisites o arquivo base, os dois ultimos são usados para fazer comparação se há necessidade de realizar atualização na compilação. Como citado, outras ferramentas utilizadas foram as definições de variáveis que facilitam na alteração de opções de compilação.

- Lab 03

    **startup.c**

    Esse é o arquivo responsável por definir as constantes e posições iniciais na memória, assim como definição dos vetores de interrupção. Então, após o Stack Pointer, vem o vetor de interrupção, reset_handler, que a função de transferir o conteudo do .data da FLASH para a SRAM, chama a função main e inicia o .bss em zero.

    Aqui também é definido todos os vetores de interrupção para orientar onde ira a memória FLASH na linkedição. Esses vetores são definidos como uma função fraca, que após serão tratadas de forma default para simplificar o processo.

    **stm32f411-rom.ld**

    Arquivo onde é feito a linkedição e geração do mapa de memória. Então toda definição de todos endereação de memória necessários para startup.c é realizada aqui, com todas as especificações colocadas aqui.  