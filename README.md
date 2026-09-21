<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="docs/banner-dark.png">
    <img src="docs/banner-light.png" alt="Resonata Studio" width="440">
  </picture>
</div>

<p align="center"><strong>Resonata Studio</strong> — Estação de Trabalho Completa para Cantores Virtuais (Web & Desktop)</p>
<p align="center">Importe MIDI, insira letras e deixe a voz virtual cantar por você!</p>

![Prévia da Interface do Resonata Studio](docs/screenshot.png)

Versão de demonstração online: [https://singer.haruyuki.cn/](https://singer.haruyuki.cn/) (devido a restrições de recursos de servidor, a versão online pode apresentar lentidão ou instabilidade; recomenda-se utilizar a versão local). O banco de voz padrão na demonstração é o da [泠鸢yousa](https://github.com/yousa-ling-official-production/yousa-ling-diffsinger-v1); respeite os termos de uso do banco.

Grupo de comunidade (QQ): [1095642281](https://qm.qq.com/q/bu34h3wR9e)

## Principais Recursos

### Canto com Cantores Virtuais
Baseado no motor de síntese de canto [OpenUtau](https://github.com/stakira/OpenUtau), suporta o carregamento dos principais bancos de voz UTAU/DiffSinger, permitindo que você componha melodias e letras diretamente no navegador para que a voz virtual cante.

### Formas Flexíveis de Uso
Suporte à execução via código-fonte na web ou instalação como cliente desktop nativo. Tanto na versão web quanto no desktop, é possível gerar links de compartilhamento para utilizar em outros dispositivos ou enviar para outras pessoas. Ao abrir o link em qualquer navegador, você tem acesso completo ao projeto e aos seus bancos de voz locais sem precisar instalar nada no outro dispositivo.

### Conversão de Timbre de Voz
Suporte à tecnologia de conversão de voz [SeedVC](https://github.com/Plachtaa/seed-vc), permitindo converter a voz cantada para o timbre desejado (requer a execução local do [SeedVC](https://github.com/Plachtaa/seed-vc)).

### Editor Piano Roll
Interface intuitiva de *Piano Roll*, com suporte à importação de arquivos MIDI e edição manual, oferecendo controle fino sobre afinação (*pitch*), duração e divisão multitrack.

### Edição de Letras e Fonemas
Suporte à inserção de letras em japonês, chinês e outros idiomas, com painel de preenchimento rápido inteligente para associar automaticamente as sílabas às notas.

### Acompanhamento Instrumental Multifaixa
Instrumentos integrados como piano, violino, bateria, guitarra e baixo com suporte a arranjo e mixagem multitrack, criando um acompanhamento instrumental completo.

### Mixagem e Efeitos
Reverberação por canal, controle de volume, equalização de 4 bandas, compressão e cadeia master de masterização com medição LUFS.

### Exportação Sem Perdas (Lossless)
Exportação precisa de faixas selecionadas ou do projeto inteiro em formato WAV de alta fidelidade para produção rápida de prévias e versões finais.

### Suporte Multiplataforma
Compatível com macOS, Windows e Linux.

## Início Rápido

### Executando pelo Aplicativo Desktop

Para usuários sem experiência com linha de comando, a melhor opção é baixar o instalador nas [Releases](https://github.com/dorayakito/WebUtau/releases/latest). Após instalar, configure seus bancos de voz no diretório indicado:

- No **macOS**: `~/webutau/voicebanks`
- No **Windows**: pasta `/voicebanks` dentro do diretório de instalação do programa

Coloque as pastas descompactadas dos bancos de voz nesses diretórios (uma subpasta para cada cantor).

### Executando a Versão Web a partir do Código-Fonte

Recomendado para desenvolvedores.

#### Pré-requisitos

- [Node.js](https://nodejs.org/) LTS
- [Git](https://git-scm.com/)
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

#### Instalação e Inicialização

```bash
git clone https://github.com/dorayakito/WebUtau.git
cd WebUtau
npm install
```

Coloque os bancos de voz em `server/voicebanks/` (cada cantor em uma subpasta individual).

- No **macOS / Linux**: execute `./dev-mac.sh`
- No **Windows**: execute `dev.bat`

Abra o navegador e acesse `http://localhost:3000` (a porta exata será informada no terminal).

<details>
<summary><strong>Conversão de Timbre SeedVC (Opcional)</strong></summary>

Requer [Python 3.10](https://www.python.org/downloads/release/python-31011/), preferencialmente com GPU NVIDIA (GTX 1060+).

```bash
git clone https://github.com/Plachtaa/seed-vc.git external/seed-vc
cd external/seed-vc
python -m venv .venv
# No Windows:
.venv\Scripts\activate
# No macOS/Linux:
source .venv/bin/activate

pip install torch==2.4.1+cu124 torchvision==0.19.1+cu124 torchaudio==2.4.1+cu124 --index-url https://download.pytorch.org/whl/cu124
pip install -r requirements.txt
pip install fastapi uvicorn python-multipart
cd ../..
# Para iniciar o serviço SeedVC:
scripts\start-seedvc-service.bat  # ou equivalente no Linux/macOS
```

> Em sistemas sem GPU NVIDIA dedicada, utilize `pip install torch torchvision torchaudio`.

</details>

## Sobre Nós

O **Resonata Studio** é mantido pelo **Grupo de Desenvolvimento Haruhi Suzumiya**, com desenvolvimento principal por [Marigold1122](https://github.com/Marigold1122).

O **Grupo de Desenvolvimento Haruhi Suzumiya** é afiliado à [**Haruhi Fan Club**](https://space.bilibili.com/201296348), dedicado à criação de projetos livres que enriquecem o ecossistema criativo.

Contato e candidaturas: haruhifanclub@outlook.com

## Stack Tecnológica

- **Frontend:** Vanilla JavaScript + Vite + Web Audio API + Tone.js + Kuromoji + Wanakana
- **Desktop:** Tauri v2 (Rust)
- **Backend:** .NET 8 + ASP.NET Core (baseado no núcleo do [OpenUtau](https://github.com/stakira/OpenUtau))
- **Conversão de Voz:** Python + PyTorch + SeedVC
