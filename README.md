# ligar-pc
### Como um computador e inicializado
## 1. Alimentação e inicialização do hardware
<p>Detalhes sobre a fonte de alimentação PSU - Unidade de fonte de alimentação:</p>
<p>Quando o botão de ligar é pressionado, a PSU executa um procedimento chamado "Power Good Signal" ou "Sinal de boa potência".</p>
<p>Isso garante que todas as tensões (12V, 5V, 3.3V) estejam estáveis.</p>
<p>Até que a PSU envie o "Power Good Signal" para a placa-mãe, o processador e outros componentes permanecem inativos.</p>
<p>Ativação da CPU: Após receber energia, o processador inicia automaticamente a execução de instruções.</p> <p>Ele começa a buscar instruções no endereço de memória fixo (geralmente o endereço 0xFFFFFFF0).</p>

## 2. Execução do POST ("Power-On Self-Test" ou "Teste automático de inicialização")
<p>Como o POST funciona tecnicamente:</p>
<p>O código do POST está embutido no firmware da BIOS/UEFI.</p>
<p>A CPU lê esse código e executa rotinas que verificam componentes essenciais.</p>
<p>Checagem de hardware:</p>
<p>RAM: Testa cada módulo para garantir que a memória está acessível e funcional.</p>
<p>Teclado: Envia comandos básicos (como "self-test" ou "autoteste") ao controlador do teclado.</p>
<p>Placa de vídeo: Verifica se o sistema tem uma GPU funcional conectada.</p>
<p>Erros comuns e diagnósticos:</p>
<p>Sons de "bipes" indicam erros específicos:</p>
<p>Exemplo: 1 bip longo + 2 curtos pode indicar problemas com a placa de vídeo.</p>
<p>Manual da placa-mãe descreve esses códigos.</p>
<p>Para erros críticos, o POST pode travar ou exibir mensagens de erro na tela.</p>

## 3. Carregamento do BIOS/UEFI
<p>O que acontece no BIOS/UEFI:</p>
<p>Inicializa controladores de dispositivos básicos, como controladores SATA/PCIe e USB.</p>
<p>Define os parâmetros do processador (frequência, multiplicador) e configura a inicialização da RAM (latência e temporização).</p>
<p>Diferenças entre BIOS e UEFI:</p>
<p>BIOS (mais antigo):</p>
<p>Capacidade limitada a 1MB de memória (modo real).</p>
<p>Funciona em sistemas baseados em MBR.</p>
<p>Menos flexível para sistemas modernos.</p>
<p>UEFI (mais novo):</p>
<p>Suporte para discos maiores que 2TB (usando GPT).</p>
<p>Interface gráfica, suporte a mouse e maior capacidade de personalização.</p>
<p>Melhor desempenho e segurança (como o Secure Boot).</p>

## 4. Localização do dispositivo de boot
<p>Como o BIOS/UEFI busca dispositivos:</p>
<p>Ele segue a ordem de boot definida pelo usuário ou padrão de fábrica.</p>
<p>Examina o setor de boot (512 bytes iniciais do dispositivo) para localizar o código de inicialização.</p>
<p>Tipos de tabelas de partição:</p>
<p>MBR (Master Boot Record):</p>
<p>Armazena o bootloader e a tabela de partições nos primeiros 512 bytes.</p>
<p>Limitação: Suporte para até 4 partições primárias e tamanhos de disco até 2TB.</p>
<p>GPT (GUID Partition Table):</p>
<p>Suporte para até 128 partições em discos maiores que 2TB.</p>
<p>Mais seguro, pois possui tabelas de backup.</p>

## 5. Execução do Bootloader
<p>O papel do bootloader:</p>
<p>Um programa simples que é responsável por carregar o kernel do sistema operacional.</p>
<p>Tipos de bootloaders:</p>
<p>Windows Boot Manager: Gerencia a inicialização do Windows, armazenando suas configurações no arquivo BCD (Boot Configuration Data).</p>
<p>GRUB (Linux): Oferece um menu para selecionar diferentes sistemas operacionais ou modos de inicialização.</p>
<p>LILO (Linux, mais antigo): Um bootloader mais simples, substituído pelo GRUB.</p>
<p>Etapas de um bootloader típico:</p>
<p>Carrega a configuração do sistema (qual kernel carregar, parâmetros de inicialização).</p>
<p>Carrega o kernel do sistema operacional na memória.</p>
<p>Transfere o controle ao kernel.</p>

## 6. Carregamento do Kernel
<p>O que é o kernel?</p>
<p>O kernel é o núcleo do sistema operacional. Ele gerencia recursos como CPU, memória, dispositivos de entrada/saída e armazenamento.</p>
<p>Carregamento do kernel:</p>
<p>O kernel é lido do disco e descompactado na memória RAM.</p>
<p>Ele configura as estruturas de dados iniciais para gerenciar os recursos do sistema.</p>
<p>Linux vs. Windows:</p>
<p>No Linux, o kernel inicia processos auxiliares, como o init ou o systemd.</p>
<p>No Windows, o kernel carrega o subsistema HAL (Hardware Abstraction Layer) e serviços como o gerenciador de memória.</p>

## 7. Inicialização dos drivers do sistema
<p>Drivers essenciais:</p>
<p>Drivers de hardware são carregados para permitir que o sistema operacional comunique-se com dispositivos como discos rígidos, placas de rede, teclado e mouse.</p>
<p>Processo:</p>
<p>Em sistemas modernos, drivers são carregados dinamicamente conforme necessário.</p>
<p>No Windows, o kernel chama o serviço SMSS.exe para inicializar subsistemas e drivers.</p>
<p>No Linux, o udev detecta e inicializa dispositivos automaticamente.</p>

## 8. Execução de processos do sistema
<p>Serviços do sistema operacional:</p>
<p>Serviços básicos, como o gerenciador de rede, sistema de arquivos e gerenciadores de autenticação.</p>
<p>Inicialização de aplicativos:</p>
<p>Programas configurados para inicializar com o sistema são carregados nesta etapa.</p>
<p>No Windows, o "Startup" carrega aplicativos automaticamente configurados no Gerenciador de Tarefas.</p>
<p>No Linux, o systemd inicia serviços e processos em paralelo.</p>

## 9. Interface gráfica ou modo de texto
<p>Ambiente gráfico:</p>
<p>O servidor gráfico (como o X.org ou Wayland no Linux) é carregado e apresenta a interface gráfica ao usuário.</p>
<p>No Windows, a GUI do sistema é gerenciada pelo Explorer.exe.</p>
<p>Modo texto (opcional):</p>
<p>Em servidores ou sistemas minimalistas, o computador pode exibir apenas um terminal de texto.</p>
<p>Os usuários podem executar comandos diretamente no terminal para interagir com o sistema.</p>

## 10. Entrega ao usuário
<p>Finalização do boot:</p>
<p>Após carregar todos os serviços e a interface gráfica, o sistema operacional exibe a tela de login.</p>
<p>Uma vez autenticado, o sistema carrega o ambiente de trabalho do usuário, incluindo atalhos, barra de tarefas e arquivos pessoais.</p>
