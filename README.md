# Image Compressor JS 📸

Um utilitário robusto para compressão de imagens desenvolvido 100% em **JavaScript**. O projeto utiliza o poder das bibliotecas `compress-images` e `sharp` para otimizar arquivos mantendo a qualidade.

---

## 🛠️ Pré-requisitos e Instalação

Para que o compressor funcione corretamente, siga a ordem de instalação abaixo:

1. **Inicie o pacote npm** (caso ainda não tenha feito):
   ```bash
   npm init -y

    Instale a biblioteca principal:
    Bash

npm i compress-images

Instale as engines específicas (Essenciais para evitar erros de binários):
Bash

    npm install pngquant-bin@6.0.1 --save
    npm install gifsicle@5.2.1 --save

🚀 Como Funciona

O fluxo do sistema consiste em processar a imagem (via Sharp) e, após o sucesso dessa operação, executar a função de compressão.
A Função compress

A lógica deve ser encapsulada em uma função que recebe o caminho de entrada e o de saída. Por padrão, mantemos as engines de compressão ativas para garantir o melhor resultado.
JavaScript

const compressImages = require("compress-images");

function compress(inputPath, outputPath) {
  compressImages(
    inputPath, 
    outputPath, 
    { compress_force: false, statistic: true, autoupdate: true }, 
    false,
    { jpg: { engine: "mozjpeg", command: ["-quality", "60"] } },
    { png: { engine: "pngquant", command: ["--quality=20-50", "-o"] } },
    { svg: { engine: "svgo", command: "--multipass" } },
    { gif: { engine: "gifsicle", command: ["--colors", "64", "--use-col=web"] } },
    function (error, completed, statistic) {
      if (error) {
        console.error("Erro na compressão:", error);
      } else {
        console.log("--- Estatísticas ---");
        console.log(statistic);
        console.log("Concluído:", completed);
      }
    }
  );
}

Integração com Sharp

A função compress deve ser chamada no final da execução do Sharp, garantindo que o arquivo original já foi devidamente tratado antes de ser reduzido.
📋 Observações Técnicas

    Caminhos: O outputPath deve ser passado dinamicamente no momento da chamada da função.

    Versões: O uso das versões pngquant-bin@6.0.1 e gifsicle@5.2.1 é obrigatório para garantir a compatibilidade com o ambiente Node.js.

    Engines: Mantivemos as configurações de engine padrão para suportar múltiplos formatos simultaneamente.
