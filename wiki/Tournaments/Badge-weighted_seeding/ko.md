---
tags:
  - badge weighting system
  - BWS
  - rank restricted
  - rank restriction
  - rank-restricted
  - tournament seed
  - tournament seeding
---

# Badge-weighted seeding

**Badge-weighted seeding** (***BWS***)은 [토너먼트](/wiki/Tournaments)에서의 [시드배정](https://en.wikipedia.org/wiki/Seed_(sports))과 각 플레이어의 [프로필 배지](/wiki/Community/Profile_badge) 수와 [글로벌 순위](/wiki/Ranking#performance-points-ranking)를 고려하여 제한하는 시스템입니다. 원래 ::{ flag=US }:: [DigitalHypno](https://osu.ppy.sh/users/4384207)가 설계한 목표는 "플레이어에게 더 정확한 시드 배정과 토너먼트 배지를 기반으로 랭크 제한을 적용하자" 라는 것이었습니다,[^hippo-cup-bws] 플레이어의 국가 랭킹을 직접 사용하는 일반적인 시드 배정과 비교됩니다.

BWS의 원칙은 플레이어가 과거에 토너먼트에 참여하여 배지를 획득한 경우 더 높은 시드에 배정되는 것입니다. 이렇게 하면 비슷한 순위의 다른 플레이어 대비 같은 시드에 무한정 머물수 없게 됩니다.[^digitalhypno-discord-1][^digitalhypno-discord-2] In a set of tournaments that all use BW, players that start at similar ranks are expected to tend toward BWS seeds that better reflect their likelihood to win matches against similarly seeded players.[^digitalhypno-discord-3][^digitalhypno-discord-4]

BWS was first used at the end of 2018 for [Hippo Cup 2](https://osu.ppy.sh/community/forums/topics/848153). Since then, it has been used in many [community tournaments](/wiki/Tournaments#community), and stands as one of the main seeding methods currently in use, alongside global ranks and qualifier rounds.

## Technical

The original and most common method used to compute players' seeds in BWS is the following bounded decay function:

```
seed = global_rank ^ (0.9937 ^ (badge_count ^ 2))
```

- `badge_count` (≥ 0): Amount of badges on the player's profile that were earned as prizes for previous tournaments of the same [game mode](/wiki/Game_mode)
- `global_rank` (≥ 1): Player's [performance points rank](/wiki/Ranking#performance-points-ranking) on the global leaderboard corresponding to the tournament's [game mode](/wiki/Game_mode)

This function satisfies properties that are important to the purpose of BWS:

- A player's seed decreases in larger increments as they attain more badges, or in other words, each badge is worth more than the last.[^hippo-cup-bws] Note that in the formula above, this is only true until around 2 to 6 badges (depending on `global_rank`), at which there is an inflection point, and then the effect becomes the opposite.
- BWS seeds are always less than or equal to `global_rank`. They are equal if the player has no badges.
- BWS seeds have the same range as `global_rank`.

Some tournaments vary their implementation of BWS by using a different seed function,[^brtt-bws] but all share the same properties described above.

## Potential drawbacks

<!-- ok this section as-is is kinda weak and mostly anecdotal, these are all things I've heard before about BWS but there's no way I can find actual references about random things said in Discord or wherever. -clayton -->

- BWS can only be updated when players receive badges, and badges are typically only given as first-place awards at the end of tournaments, so the process of settling players into accurate seeds can be very slow.
- Badges awarded for rank-restricted tournaments continue to affect players' BWS seeds even after their ranks are outside of those rank ranges.[^badge-appeals] In general, it can be viewed as a drawback that all badges are treated equal, despite the many differing factors between tournaments that cause badge prizes to be more or less difficult to win.
  - Some more experimental versions of BWS include mechanisms to address this.[^oet-bws]
- Extra work is required from tournament staff to determine which badges are relevant to the tournament and compute BWS.

::{ flag=US }:: [DigitalHypno](https://osu.ppy.sh/users/4384207) has stated that BWS is "ideally not a permanent solution to the problem", and advocates instead for a matchmaking ladder (or similar) to be supported by the [game client](/wiki/Client).[^digitalhypno-discord-5]

## References

[^badge-appeals]: ["Badge Appeals" forum post](https://osu.ppy.sh/community/forums/topics/1066357) by ::{ flag=US }:: [Kron05](https://osu.ppy.sh/users/10505107)
[^brtt-bws]: "BWS" section of [*Baku's Random Team Tournament #3* forum post](https://osu.ppy.sh/community/forums/topics/973512) by ::{ flag=DE }:: [Bakugo-](https://osu.ppy.sh/users/4990127)
[^digitalhypno-discord-1]: [Discord message (1)](https://discord.com/channels/841454370888351784/843627338839490560/987908575215120414) from ::{ flag=US }:: [DigitalHypno](https://osu.ppy.sh/users/4384207) in the [*osu! University* server](https://discord.gg/QubdHdnBVg)
[^digitalhypno-discord-2]: [Discord message (2)](https://discord.com/channels/841454370888351784/843627338839490560/987908667833737227) from ::{ flag=US }:: [DigitalHypno](https://osu.ppy.sh/users/4384207) in the [*osu! University* server](https://discord.gg/QubdHdnBVg)
[^digitalhypno-discord-3]: [Discord message (3)](https://discord.com/channels/841454370888351784/843627338839490560/987909537124204584) from ::{ flag=US }:: [DigitalHypno](https://osu.ppy.sh/users/4384207) in the [*osu! University* server](https://discord.gg/QubdHdnBVg)
[^digitalhypno-discord-4]: [Discord message (4)](https://discord.com/channels/841454370888351784/843627338839490560/987909775851388948) from ::{ flag=US }:: [DigitalHypno](https://osu.ppy.sh/users/4384207) in the [*osu! University* server](https://discord.gg/QubdHdnBVg)
[^digitalhypno-discord-5]: [Discord message (5)](https://discord.com/channels/841454370888351784/843627338839490560/987910347371458591) from ::{ flag=US }:: [DigitalHypno](https://osu.ppy.sh/users/4384207) in the [*osu! University* server](https://discord.gg/QubdHdnBVg)
[^hippo-cup-bws]: "What is BWS" section of [*Hippo Cup 2* forum post](https://osu.ppy.sh/community/forums/topics/848153) by ::{ flag=US }:: [this1neguy](https://osu.ppy.sh/users/1797189)
[^oet-bws]: [osu! European Tournament 2021 § BWS format](/wiki/Tournaments/o!ET/2021#bws-format)
