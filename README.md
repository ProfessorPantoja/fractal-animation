# 🌊 Tinta Viva

Uma **simulação de fluidos de verdade** rodando na GPU do navegador — tinta colorida que
escorre, redemoinha e se mistura como fumaça líquida. Não é um efeito pré-pronto: são as
equações de Navier-Stokes (método dos fluidos estáveis de Jos Stam) resolvidas em tempo
real em WebGL2, com advecção semi-lagrangiana, confinamento de vorticidade e projeção de
pressão por iterações de Jacobi.

**Página principal:** `index.html` (o fluido)
**Bônus:** `mosaico.html` (experimento anterior — mosaico de espirais estilo Ultra Fractal)

## Como usar

Abra o `index.html` em qualquer navegador moderno (precisa de WebGL2). Não precisa de
servidor nem de instalar nada. Em celulares a resolução da simulação é reduzida
automaticamente para manter a fluidez.

## Controles

| Controle | Efeito |
|---|---|
| **Mouse / dedo** (arraste) | empurra a tinta — clique segurado injeta mais cor |
| `B` | explosão de splats coloridos aleatórios |
| `C` | troca a paleta (arco-íris → oceano → fogo → prata) |
| `↑` / `↓` | mais / menos redemoinhos (força da vorticidade) |
| `←` / `→` | rastro some mais rápido / dura mais |
| `Espaço` | pausa |
| `A` | liga/desliga o piloto automático (dois "pincéis fantasmas" em curvas de Lissajous) |
| `H` | mostra / esconde a ajuda |

## Como funciona (resumo do pipeline por quadro)

1. **Vorticidade** — calcula o rotacional do campo de velocidade e injeta força de volta
   nos redemoinhos, compensando a dissipação numérica (é o que mantém o fluido "vivo").
2. **Projeção de pressão** — resolve ∇²p = ∇·v com ~20 iterações de Jacobi e subtrai o
   gradiente, tornando o campo incompressível (é o que faz parecer líquido).
3. **Advecção** — o próprio campo de velocidade transporta a si mesmo e a tinta
   (semi-lagrangiano: cada pixel olha "de onde eu vim?").
4. **Splats** — mouse, toque e os emissores automáticos injetam tinta + força.
5. **Display** — sombreamento por gradiente (relevo sutil) e tone mapping suave para a
   tinta acumulada saturar sem estourar.
