# From player decisions to implementation

[Project overview](../README.md) · [Selected portfolio](../portfolio/Selected.pdf?raw=true) · [Full case study](../portfolio/Full-case-study.md) · [Build the project](Building.md)

The active implementation is `Unity/`. The historical TypeScript project at the root is preserved, but is not the source of the current Windows campaign. C# uses the older internal name `Mana` for Spirit and `Bable` for some systems.

## Four sockets and a real trade-off

**Player question:** keep Harvest's cheaper purchases, or make room for Sun's longer attacks? Inspection stays available on the route; changing powers requires an altar.

1. [`RuneRepositoryView.ActivateCell`](../Unity/Assets/Scripts/Bable/RuneRepositoryView.cs) checks editing permission, rejects a fifth power and exposes the remove/equip transition. `Transfer` animates an accepted exchange.
2. [`RuneAttunement.CanChange`](../Unity/Assets/Scripts/Bable/RuneAttunement.cs) checks grounded altar proximity, story state and active guardian encounters. Practice deliberately permits editing anywhere.
3. [`RuneInventory`](../Unity/Assets/Scripts/Runes/RuneInventory.cs) separates collected runes from four active slots. Read `TryActivateToEmptySlot`, `TryDeactivateSlot` and `EquipAt`.
4. [`GameSession.RecalculateDerivedStats`](../Unity/Assets/Scripts/Core/GameSession.cs#L324) rebuilds modifiers from the active slots. Removing Harvest removes its price multiplier; adding Sun changes reach.
5. [`RuneDefinition.EffectDescription`](../Unity/Assets/Scripts/Runes/RuneDefinition.cs) provides the player's mechanical explanation. Exact magnitudes live in the [rune definition assets](../Unity/Assets/Resources/Bable/Runes).

The homepage keeps Star, Flight and Moon equipped throughout. Harvest's multiplier is 0.8; Sun's range multiplier is 1.4. Neither adds Spirit capacity. The trade-off comes from four sockets, not a new effect invented for the page.

## One Spirit, three commitments

**Player question:** spend the next unit on health, a crossing, or an opening? An unaffordable cast must not silently succeed; cancelling a Dash charge should not charge the player.

- [`GameSession.TrySpendMana`](../Unity/Assets/Scripts/Core/GameSession.cs#L192) is the shared spend operation. `GrantBossMana` grants capacity once per guardian identity.
- [`PlayerHealChannelController.Update`](../Unity/Assets/Scripts/Characters/Player/PlayerHealChannelController.cs) requires a grounded, stationary, uninterrupted three-second hold before spending one Spirit and healing one health.
- [`PlayerCombatController.Update` and `PerformCrystalDash`](../Unity/Assets/Scripts/Characters/Player/PlayerCombatController.cs) separate charging from launch payment. Early release cancels; another release is required before recharging.
- [`BossEncounter.Died`](../Unity/Assets/Scripts/Bable/BossEncounter.cs) connects a death to the unique capacity reward and its guidance message.
- [`BabelPlayer.asset`](../Unity/Assets/Data/Characters/Player/BabelPlayer.asset) contains actual player values. Read serialized definitions as well as C# defaults.

This implements a decision, not proof that one Spirit is an optimal price. [Validation](Validation.md) separates mechanical checks from balance observation.

## Break a route, not every wall

**Player question:** can the familiar cracked barrier now become a route? A single cast should excavate successive fractured stones without destroying hidden blocks beyond ordinary masonry.

[`PlayerCombatController`](../Unity/Assets/Scripts/Characters/Player/PlayerCombatController.cs#L123) contains `PerformShockwave`, `ShockwaveSequence`, `TraceShockwave` and `MuzzlePathClear`. It spends once, releases from the hand, grows along a cardinal axis, repeats damage ticks and traces the nearest blocking face each physics step. Sun changes range, not terrain obstruction.

[`BreakableWall.HitByShockwave` / `Break`](../Unity/Assets/Scripts/Bable/BreakableWall.cs) update collision and the tilemap, emit feedback and record removal through [`CampaignStore`](../Unity/Assets/Scripts/Bable/CampaignStore.cs). `RefreshFractureArt` applies the shared fractured material.

## Read the threat, then answer it

**Player question:** when is a guardian vulnerable, and how does height change its response?

[`BossBrain`](../Unity/Assets/Scripts/Bable/BossBrain.cs) considers distance, height, cooldowns and recent attacks, then separates wind-up, action and recovery. Nero changes phase at half health. [`BossProfile`](../Unity/Assets/Scripts/Bable/BossProfile.cs) holds shared parameters. [`HealthComponent`](../Unity/Assets/Scripts/Combat/HealthComponent.cs) and [`HitRecoil`](../Unity/Assets/Scripts/Combat/HitRecoil.cs) distinguish accepted damage from blocked contact. The complete portfolio explains all five guardian designs.

## Plan without a constantly moving view

**Player question:** where can I go next, and what remains uncertain around the maze's next turn?

[`CameraFollow2D`](../Unity/Assets/Scripts/World/CameraFollow2D.cs) tracks only movement beyond a rectangular dead zone. [`PassageVisibility`](../Unity/Assets/Scripts/World/PassageVisibility.cs) keeps its historical name but now only chooses authored regional zoom; it creates no global black fog. Guardian arenas are excluded from the maze close-up.

[`BablePlayerBuilds.Both`](../Unity/Assets/Editor/BablePlayerBuilds.cs) builds campaign and standalone practice from one tree. Gameplay, animations and profiles stay shared; entry points, scenes and save identities differ. See the [build guide](Building.md).
