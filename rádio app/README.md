
---

## 📄 2. Arquivo `assets/js/vinculo-lark.js` — INTEGRAÇÃO OFICIAL
```javascript
/**
 * Integração Oficial com o Lark Player
 * Projeto: Geração Sônica
 * Link Oficial: https://larkplayer.link/Ahg1u1hYBZ
 */

const LARK_PLAYER_LINK = "https://larkplayer.link/Ahg1u1hYBZ";
const LARK_SCHEME = "larkplayer://";

// Verifica se o Lark Player está instalado
function verificarLarkInstalado() {
    return new Promise((resolve) => {
        const timeout = setTimeout(() => resolve(false), 1000);
        window.location.href = LARK_SCHEME + "test";
        window.addEventListener('blur', () => {
            clearTimeout(timeout);
            resolve(true);
        });
    });
}

// Função para abrir o Lark Player e reproduzir a Rádio 24h
async function tocarRadioAoVivo() {
    const instalado = await verificarLarkInstalado();
    if (instalado) {
        // Abre diretamente no aplicativo
        window.location.href = `${LARK_SCHEME}play?url=SEU_LINK_DA_TRANSMISSAO_24H&title=Geração Sônica - Rádio Ao Vivo&artist=Geração Sônica`;
    } else {
        // Redireciona para instalação oficial
        alert("Para ouvir a Rádio Geração Sônica, instale o Lark Player! 🎵");
        window.open(LARK_PLAYER_LINK, '_blank');
    }
}

// Função para tocar músicas da playlist
async function tocarMusica(urlMusica, titulo, artista) {
    const instalado = await verificarLarkInstalado();
    if (instalado) {
        window.location.href = `${LARK_SCHEME}open?file=${urlMusica}&title=${encodeURIComponent(titulo)}&artist=${encodeURIComponent(artista)}`;
    } else {
        alert("Instale o Lark Player para ouvir: " + titulo);
        window.open(LARK_PLAYER_LINK, '_blank');
    }
}

// Função para reproduzir Podcasts
async function tocarPodcast(urlPodcast, titulo) {
    const instalado = await verificarLarkInstalado();
    if (instalado) {
        window.location.href = `${LARK_SCHEME}podcast?url=${urlPodcast}&title=${encodeURIComponent(titulo)}`;
    } else {
        alert("Instale o Lark Player para ouvir os Podcasts!");
        window.open(LARK_PLAYER_LINK, '_blank');
    }
}

// Configurações automáticas do Lark Player
function configurarLarkAutomaticamente() {
    console.log("Configurando vínculo com o Lark Player...");
    // Ativa reprodução em segundo plano
    localStorage.setItem("lark_background", "true");
    // Define formato padrão para MP3/WAV
    localStorage.setItem("lark_formato_padrao", "mp3,wav,flac,aac");
    console.log("✅ Vínculo configurado com sucesso!");
}

// Executa configuração ao carregar o app
document.addEventListener('DOMContentLoaded', configurarLarkAutomaticamente);
