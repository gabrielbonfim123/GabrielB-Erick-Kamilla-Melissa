Nome dos Autores: Erick, Gabriel B, Melissa, Kamilla.

 Explicação do Código - Sistema de Impressão com DLL

Este código Java implementa uma interface de controle para impressoras térmicas da marca **Elgin**, utilizando JNA (Java Native Access) para comunicação com uma biblioteca DLL nativa do Windows.

 Arquitetura Principal

O programa utiliza **JNA** para carregar e chamar funções de uma DLL (`E1_Impressora01.dll`) que controla fisicamente a impressora. A interface `ImpressoraDLL` mapeia todas as funções disponíveis na biblioteca nativa.

 Componentes Principais

Interface ImpressoraDLL
Declara todos os métodos disponíveis na DLL, incluindo:
- Gerenciamento de conexão (abrir/fechar)
- Impressão de texto, QR Code e código de barras
- Controle de gaveta de dinheiro
- Emissão de sinais sonoros
- Impressão de documentos fiscais XML (SAT)
- Controle de posicionamento e corte de papel

Gerenciamento de Conexão
O código mantém controle do estado da conexão através da variável `conexaoAberta`. O usuário precisa configurar quatro parâmetros:
- **Tipo de conexão** (USB, Serial, etc.)
- **Modelo da impressora** (I9, I8, etc.)
- **Nome da conexão** (USB, COM1, etc.)
- **Parâmetro adicional** (geralmente 0)

Funcionalidades Implementadas

Impressão de Texto: Captura texto do usuário e imprime com estilo centralizado (posição 1, estilo 4), seguido de corte automático do papel.

Impressão de QR Code: Gera QR Codes com tamanho 6 e nível de correção de erros 4.

Impressão de Código de Barras: Configurado para imprimir automaticamente um código CODE128 fixo (`{A012345678912`) sem interação do usuário. Os parâmetros definem altura (100), largura (2) e posição do HRI - texto legível (3).

Impressão de XML SAT: Abre um diálogo de seleção de arquivo para escolher XMLs de documentos fiscais SAT e os envia para impressão. O SAT é o Sistema Autenticador e Transmissor de Cupons Fiscais Eletrônicos usado no Brasil.

Controle de Gaveta: Oferece duas opções - gaveta Elgin padrão ou controle customizado por pino com tempos configuráveis.

Sinal Sonoro: Emite bipes na impressora (4 vezes, com 5ms de intervalo).

Fluxo de Uso

1. O usuário configura os parâmetros de conexão
2. Abre a conexão com a impressora
3. Executa operações desejadas (impressões, abrir gaveta, etc.)
4. Fecha a conexão ao encerrar

O menu interativo em loop permite realizar múltiplas operações sem reiniciar o programa. Todas as operações verificam se a conexão está aberta antes de executar, garantindo segurança no uso da DLL.
