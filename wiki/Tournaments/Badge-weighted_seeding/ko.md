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

BWS의 원칙은 플레이어가 과거에 토너먼트에 참여하여 배지를 획득한 경우 더 높은 시드로 배정하는 것입니다. 이렇게 하면 비슷한 순위의 다른 플레이어 대비 같은 시드에 무한정 머물수 없게 됩니다.[^digitalhypno-discord-1][^digitalhypno-discord-2] 배지 가중치를 이용하는 모든 토너먼트에서, 비슷한 순위에서 시작하는 플레이어는 비슷한 시드를 받은 플레이어와의 경기에서 승리할 가능성을 더 잘 반영하는 BWS 순위를 선호하는 경향이 있을 것으로 예상합니다.[^digitalhypno-discord-3][^digitalhypno-discord-4]

BWS는 2018년 후반 [Hippo Cup 2](https://osu.ppy.sh/community/forums/topics/848153)에서 처음 사용되었습니다. 그 이후로 많은 [커뮤니티 토너먼트](/wiki/Tournaments#community)에서 사용되었으며, 글로벌 순위 및 퀄리파이어 라운드와 함께 현재 사용되는 주요 시드배정 방법중 하나입니다.

## Technical

BWS에서 플레이어의 시드를 계산하는데 가장 일반적인 방법은 다음과 같은 식을 사용합니다.

```
시드 = 세계 순위 ^ (0.9937 ^ (배지 개수 ^ 2))
```

- `배지 개수` (≥ 0): 동일한 [게임 모드](/wiki/Game_mode) 토너먼트에서 상품으로 획득한 플레이어 프로필의 배지 수입니다.
- `세계 순위` (≥ 1): 토너먼트의 [게임 모드](/wiki/Game_mode)에 대응하여 글로벌 리더보드에 있는 플레이어의 [퍼포먼스 포인트 순위](/wiki/Ranking#performance-points-ranking)입니다.

이 기능은 BWS의 중요한 목표를 충족합니다:

- 플레이어의 시드는 더 많은 배지를 획득할수록 더 크게 감소하게 됩니다. 즉, 각 배지는 이전 배지보다 더 많은 비중을 차지하게 됩니다. [^hippo-cup-bws] 위 공식에서는 대략 2까지만 적용되며, 변곡점인 6개의 배지(`세계 순위`에 따라 편차가 있음)에 도달하면 효과는 반대로 됩니다.
- BWS 시드는 항상 `세계 순위`와 작거나 같아야 합니다. 배지가 없는 경우에 서로 동일하게 됩니다.
- BWS 시드는 `세계 순위`와 동일한 범위를 가집니다.

일부 토너먼트에선 다른 시드 기능을 사용하여 BWS 구현을 다양하게 하지만,[^brtt-bws] 위에 있는 설명을 모두 공유하게 됩니다.

## 잠재적인 단점

<!-- ok this section as-is is kinda weak and mostly anecdotal, these are all things I've heard before about BWS but there's no way I can find actual references about random things said in Discord or wherever. -clayton -->

- BWS는 플레이어가 배지를 받을 때에만 갱신이 가능하며, 배지는 일반적으로 토너먼트가 끝날 때 1등 상품으로만 지급되므로 플레이어를 정확한 시드에 배정하는 과정이 매우 느릴 수 있습니다.
- 순위를 제한하는 토너먼트에서 수여받는 배지는 해당 순위를 벗어나더라도 BWS 시드에 영향을 미치게 됩니다.[^badge-appeals] 기본적으로, 모든 배지를 동일하게 취급한다는 점은 단점으로 볼 수 있으며 토너먼트에서 배지를 획득하기에 다소 어려워지는 다양한 요인들이 있습니다.
  - 실험적인 BWS에는 이 문제를 해결할 수 있는 매커니즘이 포함되어 있습니다.[^oet-bws]
- 토너먼트와 관련된 배지의 범위를 결정하고 BWS를 계산할려면 토너먼트 스태프의 추가 작업이 필요합니다.

::{ flag=US }:: [DigitalHypno](https://osu.ppy.sh/users/4384207)가 BWS는 "이 문제에 대한 영구적인 해결책은 아니다"라고 했으며, 대신에 [게임 클라이언트](/wiki/Client)에서 지원하는 래더 시스템(또는 유사하게)을 지원하는것을 옹호했습니다.[^digitalhypno-discord-5]

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
