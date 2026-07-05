# 🌀 Fractal Vivo

Uma animação interativa em WebGL inspirada em arte fractal feita no **Ultra Fractal** —
aquelas composições de quadrados derretidos com espirais, que mesmo estáticas já parecem se mover.
Aqui, elas se movem de verdade.

## Como usar

Basta abrir o `index.html` em qualquer navegador moderno. Não precisa de servidor,
não precisa instalar nada — é um arquivo único, tudo roda na GPU via WebGL.

## O que acontece

A imagem é gerada em tempo real por um *fragment shader*:

1. **Grade diagonal de células** — cada célula é um "quadrado arredondado" com anéis
   concêntricos de cor chapada (posterizada), como curvas de nível de tinta.
2. **Espiral no centro de cada célula** — uma rotação com decaimento exponencial
   (o clássico *swirl* do Ultra Fractal), cada uma girando devagar no seu próprio ritmo.
3. **Domain warping** — camadas de vórtices em escalas diferentes distorcem as
   coordenadas antes do padrão ser desenhado, criando o aspecto de mármore líquido.
4. **Gradiente térmico** — paleta fria (roxos, violeta, teal) que esquenta na diagonal
   para vermelhos, laranjas e amarelos.

A animação própria vem de animar os *parâmetros* do warp — as fases das espirais e a
deriva do campo — e não a imagem pronta.

## Controles

| Controle | Efeito |
|---|---|
| **Mover o mouse** | cria um vórtice que segue o cursor e arrasta a tinta (com inércia) |
| **Clicar / arrastar** | vórtice mais forte |
| `←` / `→` | diminui / aumenta a velocidade da animação (aceita valores negativos = tempo reverso) |
| `↑` / `↓` | zoom in / zoom out |
| `Espaço` | pausa / retoma a animação própria (o mouse continua funcionando) |
| `C` | gira a paleta de cores |
| `w` / `Shift+W` | mais / menos turbulência no fluxo |
| `H` | mostra / esconde a ajuda |
