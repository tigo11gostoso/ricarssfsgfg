# Rocket Cars

![build](../../actions/workflows/build.yml/badge.svg)
 — mod Fabric 1.21.1 (física estilo Rocket League)

## Como compilar
(Em alternativa, o GitHub Actions compila o `.jar` e disponibiliza-o em *Actions → build → Artifacts* (também podes lançá-lo à mão com *Run workflow*).)

1. Precisas de **JDK 21** e Gradle 8.8+. Abre a pasta no IntelliJ IDEA (importa como projeto Gradle) **ou** corre `gradle wrapper --gradle-version 8.8` e depois `./gradlew build`.
2. O `.jar` fica em `build/libs/`. Põe-no em `mods/` com **Fabric Loader 0.16+** e **Fabric API 0.102.0+1.21.1**.
3. Para testar já: `./gradlew runClient`.

## Como jogar
- Item **Rocket Car** (separador Ferramentas do criativo, ou receita). Clica num bloco para o colocar. **Botão direito** no carro para entrar, **Shift** para sair, **bater** para o recolher.
- **W/S** acelerar/travar/marcha-atrás (no ar: pitch) · **A/D** virar (no ar: yaw) · **Espaço** saltar (segura para saltar mais alto; 2.º toque = double jump; com W/A/S/D = flip direcional)
- **Ctrl esq.** boost · **Alt esq.** handbrake/powerslide (no ar: air roll com A/D) · **Z / X** air roll esquerda/direita (configuráveis)
- **Blocos de ouro** são boost pads (recarregam o boost).
- Flip-cancel: logo a seguir a um flip, carrega no pitch oposto.

## Física (src/main/java/com/rlcars/physics) — 100% independente do Minecraft
Todos os números estão em `RL.java` (unidades do RL × `U = 0.02` blocos). Muda `U` para carros maiores/mais rápidos.
Testes (só precisa de JDK 21): `./physics-test/run.sh` — verifica aceleração, boost, travagem, viragem, salto, flips, air control, aterragens e paredes. O GitHub Actions corre-os a cada push.

## Limitações honestas
- **Não foi compilado contra o Minecraft** (sem rede/Gradle onde o escrevi). A física foi compilada e testada; o código de ligação ao jogo foi escrito com cuidado para 1.21.1 mas pode precisar de pequenos ajustes de nomes de API.
- Constantes do RL vindas de medições da comunidade, de memória; os valores de flip/dodge são aproximações (ajusta em `RL.java`).
- Física a 120 Hz mas o input é lido a 20 Hz (tick do Minecraft); a renderização interpola.
- Colisões só com blocos (não com mobs/outros carros nem bola). Não há "ball cam". Paredes: o assist sobe paredes altas (≥2 blocos); um quarter-pipe de escadas funciona melhor que uma aresta a 90°.
- O condutor não gira com o carro (só o banco); a câmara de 3.ª pessoa segue o carro, mas mexer o rato dá um pequeno solavanco.
