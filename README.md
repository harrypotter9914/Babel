# Babel

Descend beneath a tower built as a refuge, then return with the powers to challenge its ruler. In this dark fantasy Metroidvania, the same Spirit can mend a wound, carry you across a gap, or break a sealed route.

**Game, gameplay, level and narrative design & programming by Yibo Wang (王奕博).** Personal project · Unity 6 · Windows · In development.

[![Read the selected design portfolio: 7 pages of gameplay, level and systems design](media/selected-portfolio.svg)](portfolio/Selected.pdf?raw=true)

**[Play free on itch.io](https://hajimi9914.itch.io/babel)** · **[Watch the gameplay & design film · 3m 15s](https://youtu.be/SPEH-DODZ7I)** · **[Follow the design into the source](docs/Code.md)**

[![Babel's official gold title above an illustrated Tower of Babel. Game design and programming by Yibo Wang.](media/babel-cover.jpg)](https://youtu.be/SPEH-DODZ7I)

*Cover illustration; the gameplay below is captured in-engine. Start with the seven-page portfolio for the quickest design overview.*

## Four sockets. A reason to return.

Eight recovered runes offer possibilities; only four can be active. You can inspect the repository anywhere, but campaign equipment changes require an altar outside an active guardian encounter. Preparation happens before the journey, rather than becoming a mid-fight menu solution.

In this example, **Star, Flight, Moon and Harvest** already fill the sockets. Sun cannot be added as a fifth power. I remove **Harvest**, which makes shop prices 20% lower, and equip **Sun**, which extends sword and shockwave reach by 40%.

![Actual campaign repository: four full sockets reject Sun, Harvest is removed, then Sun occupies the empty socket.](media/rune-choice.gif)

*The repository shows the constraint before the exchange, animates the transfer, and keeps the effect description beside the choice. The remaining three powers stay equipped.*

| Before: keep the discount | After: take more reach |
| --- | --- |
| ![Without Sun, the shockwave ends earlier along the forest path.](media/reach-before.jpg) | ![With Sun equipped, the shockwave reaches farther along the same forest path.](media/reach-after.jpg) |
| Harvest preserves gold for a later purchase. | Sun creates more distance between the player and a threat. |

The change affects the next action, not just an inventory number. It also gives up an economic advantage until the player returns to an altar. **The question is which four powers suit the next attempt, not how to equip everything.** [Read the implementation](docs/Code.md#four-sockets-and-a-real-trade-off).

## Spend one Spirit to change the route

Healing, Crystal Dash and Shockwave draw from the same resource. Healing needs a three-second stationary channel; Dash charges before spending one Spirit on launch. Shockwave also costs one Spirit, but persists for 2.5 seconds while the player can move.

![Actual Abaddon exit: a sword swing leaves the fractured seal intact; a sustained shockwave destroys the seal, then the player crosses the opening.](media/fractured-return.gif)

*One cast can break successive fractured blocks, so a passage does not charge the player for every brick. Ordinary masonry still stops the beam. Fracture art makes the material rule visible; the cost keeps opening a route connected to the next healing decision.*

**Why this changed:** the earlier short, one-block result made exploration too expensive. The longer cast makes the unlock useful on a return journey. Dash later gained a launch cost so repeated travel could not bypass the shared-resource decision. Each unique guardian victory adds one maximum Spirit; the current costs are implemented, while their balance still needs player observation.

## A familiar place becomes a new possibility

The route descends from the forest into buried rooms before folding back toward the tower. Abaddon's Shockwave opens fractured seals; Korah's Wall Jump turns shafts into routes; Azazel's Double Jump changes aerial timing; Bel's Crystal Dash crosses long passages. Nero tests that accumulated movement and combat vocabulary.

[![Scene overview of Babel with five guardian rooms numbered and the forest, buried labyrinth, ascent and upper trials labelled.](media/world-route.jpg)](media/world-route.jpg?raw=true)

*Unity scene overview with analysis labels, not the player's map screen. Numbers identify rooms, not a literal travel line. The player-facing map reveals explored space. Open the figure for detail.*

The important gate is not simply a locked wall. A premature floor opening can strand a player without the next ability. The revised approach preserves a way back, then lets the newly earned beam open the guardian's exit. Away from the lower-right maze, v0.57 keeps a wider, stable view so players can read the route; the maze retains closer framing and uncertainty. [See the route design and its testing limits](docs/Design.md).

## Explore the full design and source

| Go deeper | What to look for |
| --- | --- |
| [Full design case study · 12 pages](portfolio/Full-case-study.md) | Read every final portfolio page online, jump by theme, open figures at full size, or download the complete PDF. |
| [Level and systems design notes](docs/Design.md) | How altar commitments, ability gates and camera framing change what the player can plan. |
| [Guided code walkthrough](docs/Code.md) | Trace a rune exchange into derived stats, one Spirit into three actions, and a beam into persistent broken stone. |
| [Browse the active Unity source](Unity/Assets/Scripts) | Gameplay code in its original project directories, with shared definitions and guardian profiles. |
| [Build and validation guide](docs/Building.md) | Unity version, Git LFS, campaign/practice isolation, and the scope of verification. |

**Version note:** the source and newly captured examples are v0.57. The existing public itch.io download and final portfolio describe v0.56; v0.57 adds the camera framing revision. Both Windows players were rebuilt and smoke-tested before this page was published. These checks do not claim a new full campaign playthrough or a formal player study. [Verification details](docs/Validation.md).

Selected game and cover artwork is AI-assisted; dialogue uses synthetic voices. The film uses an authorized clone of my own voice. Capture setup, resource credits and reuse limitations are recorded in [Credits & media provenance](docs/Credits.md). No blanket license to reuse inherited third-party assets is implied.
