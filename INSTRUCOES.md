# Fantasy Collection - instalacao

Voce recebeu 2 arquivos:

- **FantasyCollection.zip** - o resource pack (ja convertido pro formato do Minecraft 26.2, `pack_format 88`).
- **FantasyCollection-1.0.0.jar** - o plugin que envia o pack aos jogadores e entrega as 11 armas.

SHA-1 do FantasyCollection.zip: `be28d4c9bc8e070d849add9238af219468484757`

---

## Passo 1 - Hospedar o resource pack

O Minecraft baixa o pack de uma **URL publica com link DIRETO** (a URL tem que
apontar pro arquivo .zip, nao pra uma pagina de download). Opcoes comuns:

- Um site/host seu com o .zip acessivel por HTTP(S).
- GitHub: suba o .zip num repositorio e use o link "Download raw" (termina em `.zip`).
- Qualquer serdor de resource pack que devolva link direto.

> Nao serve link do Dropbox/Drive de pagina. Se usar Dropbox, troque o final
> `?dl=0` por `?dl=1`. Google Drive normalmente nao funciona como link direto.

Guarde a URL final.

## Passo 2 - Instalar o plugin

1. Suba `FantasyCollection-1.0.0.jar` na pasta `/plugins` do servidor BattleRoyale.
2. Reinicie o servidor (ou de `/reload confirm`, mas reiniciar e melhor).
   Isso cria a pasta `plugins/FantasyCollection/` com os arquivos de config.

## Passo 3 - Apontar a URL no config

Edite `plugins/FantasyCollection/config.yml`:

```yaml
resource-pack:
  url: "https://SEU-LINK-DIRETO/FantasyCollection.zip"
  sha1: "be28d4c9bc8e070d849add9238af219468484757"
  force: true
  prompt: "&7Baixe o pacote de texturas do &bFantasy Collection&7."
  send-on-join: true
```

- O `sha1` ja vem preenchido pro .zip que te enviei. **Se voce recompactar ou
  alterar o .zip, deixe `sha1: ""`** que o plugin baixa e calcula sozinho.
- `force: true` obriga o jogador a aceitar (recusar = kick). Coloque `false` se
  quiser deixar opcional (ai o jogador pode desligar com `/fantasy pack off`).

Depois rode no console/jogo: `/fantasy reload`

## Passo 4 - Testar

- Entre no servidor: o pack deve baixar automaticamente.
- Pegue uma arma: `/fantasy give thunderous_sword`
- Veja todas: `/fantasy list`

---

## Comandos

| Comando | O que faz | Permissao |
|---|---|---|
| `/fantasy give <item> [jogador] [qtd]` | Da uma arma | `fantasy.give` |
| `/fantasy list` | Lista as 11 armas | - |
| `/fantasy send [jogador]` | Reenvia o pack | `fantasy.send` |
| `/fantasy pack [on/off]` | Liga/desliga receber o pack (so se `force: false`) | - |
| `/fantasy reload` | Recarrega a config | `fantasy.admin` |

Alias: `/fc`. Todos os comandos tem tab complete.

## Itens e CustomModelData

Cada arma e uma `DIAMOND_SWORD` com um CustomModelData (101 a 111):

| id | CMD | id | CMD |
|---|---|---|---|
| bane_of_end | 101 | null_sword | 107 |
| bloodflame | 102 | shattered_mirror | 108 |
| chainblade | 103 | spectral_blade | 109 |
| crystallic_scythe | 104 | sword_of_the_stars | 110 |
| haunted_edge | 105 | thunderous_sword | 111 |
| null_greataxe | 106 | | |

Se quiser dar sem o plugin (comando vanilla no 26.2):

```
/give @p minecraft:diamond_sword[minecraft:custom_model_data={floats:[111]}]
```

Outro plugin (kit, loja) que aplique o mesmo CustomModelData numa diamond_sword
tambem mostra a textura, desde que o jogador tenha o pack.

---

## Observacoes importantes

- O pack foi convertido pro formato do **Minecraft 26.2** (o formato antigo do
  arquivo original, `pack_format 13`, nao renderiza em clientes 1.21.4+). Ele
  funciona para clientes nativos 26.x. Clientes bem antigos entrando por
  ViaVersion podem nao ver as texturas, porque resource pack e por versao do cliente.
- O plugin nasce compativel com **Folia** (usa os schedulers por entidade/async).
- O servidor tem so 1 porta liberada (a do jogo), por isso o pack precisa ser
  hospedado externamente - o plugin nao tem como servir o arquivo sozinho.
- Creditos dos modelos: Legacy Creators (phytormc.com).
