# mugen-hogwarts-releases

Releases públicas do **launcher** do Hogwarts (`mugen-hogwarts`). Este repositório só tem binários, publicados nas [GitHub Releases](https://github.com/2hdsc/mugen-hogwarts-releases/releases). Não tem código-fonte aqui.

## Instalar e jogar

1. Baixe o launcher do seu sistema na [última Release](https://github.com/2hdsc/mugen-hogwarts-releases/releases/latest):
   - Linux (x86_64): `mugen-hogwarts-linux-amd64`
   - Mac Apple Silicon (M1, M2, M3, M4): `mugen-hogwarts-darwin-arm64`
   - Windows: `mugen-hogwarts-windows-amd64.exe`
2. Instale e jogue. O jogo vai para `~/mugen-hogwarts` (Linux e Mac) ou `%LOCALAPPDATA%\mugen-hogwarts` (Windows).

   **Linux**
   ```bash
   curl -LO https://github.com/2hdsc/mugen-hogwarts-releases/releases/latest/download/mugen-hogwarts-linux-amd64
   chmod +x mugen-hogwarts-linux-amd64
   ./mugen-hogwarts-linux-amd64 install --all     # todos os personagens (sem --all vem só o básico)
   ./mugen-hogwarts-linux-amd64 online --start    # online: Host/Join no menu Network
   ~/mugen-hogwarts/hogwarts-linux                # offline
   ```
   No Ubuntu 22.04 ou mais novo, se faltar alguma biblioteca:
   `sudo apt install libgl1 libgtk-3-0 libasound2 libpulse0 libxss1`
   (no 24.04 os nomes são `libgtk-3-0t64` e `libasound2t64`).

   **Mac (Apple Silicon)**
   ```bash
   curl -LO https://github.com/2hdsc/mugen-hogwarts-releases/releases/latest/download/mugen-hogwarts-darwin-arm64
   chmod +x mugen-hogwarts-darwin-arm64
   xattr -d com.apple.quarantine mugen-hogwarts-darwin-arm64   # só precisa se baixou pelo navegador
   ./mugen-hogwarts-darwin-arm64 install --all
   ./mugen-hogwarts-darwin-arm64 online --start   # online
   ~/mugen-hogwarts/hogwarts-mac                  # offline (ou dois cliques em hogwarts-mac no Finder)
   ```
   Se o macOS ainda bloquear o jogo: Ajustes do Sistema → Privacidade e Segurança → "Abrir mesmo assim". O `install` já tira a quarentena da pasta do jogo. Mac Intel não é suportado: o Ikemen GO não publica motor para Intel (o `mugen-hogwarts-darwin-amd64` existe, mas o `install` não tem motor para baixar).

   **Windows**: abra o `mugen-hogwarts-windows-amd64.exe` com dois cliques. Sem argumentos ele faz o mesmo que `online --start`: pergunta se pode instalar e depois abre o jogo. Para jogar offline, abra `hogwarts-windows.exe` na pasta do jogo.

3. **Como chamar o launcher.** Daqui em diante os comandos aparecem como `mugen-hogwarts <comando>`. Troque pelo jeito que você o chama; os dois valem:
   - direto, na pasta onde baixou: `./mugen-hogwarts-linux-amd64 <comando>` (Mac: `./mugen-hogwarts-darwin-arm64`; Windows/PowerShell: `.\mugen-hogwarts-windows-amd64.exe`);
   - ou no PATH com o nome curto (opcional):
     ```bash
     mkdir -p ~/.local/bin
     mv mugen-hogwarts-linux-amd64 ~/.local/bin/mugen-hogwarts   # no Mac: mugen-hogwarts-darwin-arm64
     mugen-hogwarts <comando>
     ```
     No Ubuntu, `~/.local/bin` entra no PATH no próximo login (ou abra outro terminal). No Mac, antes rode `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc` e abra outro terminal.

   O nome do arquivo não muda nada, e as dicas que o launcher imprime já usam o jeito como você o chamou. `mugen-hogwarts help` lista tudo.

4. **Atualizar o jogo:** `mugen-hogwarts update` (`--all` ou `--pack ID` trazem mais personagens). Ele só baixa o que mudou, e suas configurações em `save/` são mantidas.

5. **Atualizar o launcher:** `mugen-hogwarts self-update` baixa a versão nova, confere com o `SHA256SUMS` e troca o próprio arquivo (seja qual for o nome). `self-update --check` só consulta. Até a v0.3.2 o `self-update` só mostrava o link: nessas versões, baixe a nova uma vez à mão.

6. **Desinstalar:** `mugen-hogwarts uninstall` mostra o que vai apagar e pergunta antes (`--yes` pula a pergunta).
   - Por padrão mantém `save/` (suas configurações e replays), o mesmo que `--keep-save`. `--purge` apaga a pasta inteira.
   - Só apaga uma pasta criada pelo `install` (com `save/installed-client.json`). Para outra pasta do jogo: `--game-dir DIR --force`.
   - O launcher não se apaga sozinho: no fim ele mostra o caminho do arquivo para você apagar.

Outros comandos: `mugen-hogwarts` sem nada é o mesmo que `online --start` (oferece instalar se faltar o jogo); `mugen-hogwarts hash` mostra o hash do build (os dois jogadores precisam do mesmo). Para uma pasta fora do padrão, acrescente `--game-dir DIR`.

Na pasta do jogo, o executável se chama `hogwarts-linux`, `hogwarts-mac` (abre o `Hogwarts.app`) ou `hogwarts-windows.exe`. É o motor oficial do Ikemen GO com outro nome. Instalações antigas ainda têm `Ikemen_GO_Linux`, `I.K.E.M.E.N-Go.app` ou `Ikemen_GO.exe`: o `update` troca para os nomes novos e apaga os antigos.

Instalações feitas até o launcher v0.3.1 em `~/Hogwarts` continuam funcionando ali: o launcher usa a pasta antiga e mostra como movê-la (`mv ~/Hogwarts ~/mugen-hogwarts`, com o jogo fechado).

## O que vem de onde

- O launcher sai neste repositório (ver o passo 5 para atualizá-lo).
- O motor [Ikemen GO v1.0.0](https://github.com/ikemen-engine/Ikemen-GO) (MIT), os arquivos do jogo, os packs de personagens e cenários e o manifest ficam no **Cloudflare R2**. O `install` baixa tudo de lá e confere o sha256 de cada arquivo.
- O código-fonte do jogo e do launcher é privado, em [2hdsc/mugen-hogwarts](https://github.com/2hdsc/mugen-hogwarts).
- Até a v0.2.0 os binários se chamavam `hogwarts-<sistema>-<arquitetura>`.
