# mugen-hogwarts-releases

Releases públicas do **launcher** do Hogwarts (`mugen-hogwarts`). Este repositório só tem binários, publicados nas [GitHub Releases](https://github.com/2hdsc/mugen-hogwarts-releases/releases). Não tem código-fonte aqui.

## Instalar e jogar

1. Baixe o binário do seu sistema na [última Release](https://github.com/2hdsc/mugen-hogwarts-releases/releases/latest):
   - Linux (x86_64): `mugen-hogwarts-linux-amd64`
   - Windows: `mugen-hogwarts-windows-amd64.exe`
   - Mac Apple Silicon (M1, M2, M3, M4): `mugen-hogwarts-darwin-arm64`
2. Instale o jogo. Ele vai para `~/Hogwarts` (Linux e Mac) ou `%LOCALAPPDATA%\Hogwarts` (Windows):

   **Linux**
   ```bash
   chmod +x mugen-hogwarts-linux-amd64
   ./mugen-hogwarts-linux-amd64 install          # ou: install --all (todos os personagens)
   ./mugen-hogwarts-linux-amd64 online --start
   ```
   No Ubuntu 22.04 ou mais novo, se faltar alguma biblioteca:
   `sudo apt install libgl1 libgtk-3-0 libasound2 libpulse0 libxss1`
   (no 24.04 os nomes são `libgtk-3-0t64` e `libasound2t64`).

   **Mac (Apple Silicon)**
   ```bash
   chmod +x mugen-hogwarts-darwin-arm64
   xattr -d com.apple.quarantine mugen-hogwarts-darwin-arm64
   ./mugen-hogwarts-darwin-arm64 install
   ./mugen-hogwarts-darwin-arm64 online --start
   ```
   Se o macOS ainda bloquear o jogo: Ajustes do Sistema → Privacidade e Segurança → "Abrir mesmo assim".

   **Windows**: abra o `mugen-hogwarts-windows-amd64.exe` com dois cliques. Ele pergunta se pode instalar e depois abre o jogo. No PowerShell: `.\mugen-hogwarts-windows-amd64.exe install`.

3. Mais personagens depois: `mugen-hogwarts update --all` (ou `--pack ID`). Rodar o `install` ou o `update` de novo só baixa o que mudou, e suas configurações em `save/` são mantidas.

## O que vem de onde

- O launcher sai neste repositório. Ele também confere se há versão nova (`mugen-hogwarts self-update --check`).
- O motor [Ikemen GO v1.0.0](https://github.com/ikemen-engine/Ikemen-GO) (MIT), os arquivos do jogo, os packs de personagens e cenários e o manifest ficam no **Cloudflare R2**. O `install` baixa tudo de lá e confere o sha256 de cada arquivo.
- O código-fonte do jogo e do launcher é privado, em [2hdsc/mugen-hogwarts](https://github.com/2hdsc/mugen-hogwarts).
- Até a v0.2.0 os binários se chamavam `hogwarts-<sistema>-<arquitetura>`.
