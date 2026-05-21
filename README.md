<div align="center">

```
┌──────────────────────────────────────────────────────────────────────┐
│  ABUUDIII :: COMPUTE DIE                       [ HBM3 · L2 · 4 NoC ] │
├──────────────────────────────────────────────────────────────────────┤
│  ┌────┬────┬────┬────┬────┬────┬────┬────┐                           │
│  │ SM │ SM │ SM │ SM │ SM │ SM │ SM │ SM │   warp   = 32 threads     │
│  ├────┼────┼────┼────┼────┼────┼────┼────┤   sched  = round-robin    │
│  │ SM │ SM │ SM │ ██ │ ██ │ SM │ SM │ SM │   occ.   = 87 %           │
│  ├────┼────┼────┼────┼────┼────┼────┼────┤                           │
│  │ SM │ SM │ ██ │ ██ │ ██ │ ██ │ SM │ SM │   ██ = active kernel      │
│  ├────┼────┼────┼────┼────┼────┼────┼────┤                           │
│  │ SM │ SM │ SM │ ██ │ ██ │ SM │ SM │ SM │                           │
│  └────┴────┴────┴─┬──┴─┬──┴────┴────┴────┘                           │
│                   ▼    ▼                                             │
│             [ L2 cache ]  ◄─────►  [ HBM3 · 6.4 TB/s ]               │
└──────────────────────────────────────────────────────────────────────┘
```

<a href="https://github.com/Abuudiii">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=18&duration=2800&pause=900&color=58A6FF&center=true&vCenter=true&width=620&lines=%24+./abuudiii+--init;loading+symbols...+done.;Software+%2F+Systems+%2F+Low-level+enthusiast." alt="Typing SVG" />
</a>

</div>

---

## ╭─ /proc/self/maps  ::  about

```c
0xFFFFFFFFFFFF  ┌─────────────────────────┐
                │   kernel space          │  <PRIVILEGED INTERESTS / MISSION>
                ├─────────────────────────┤  ← %rsp
                │   stack         ▼       │  <RECENT WORK / WHAT I JUST SHIPPED>
                │     │                   │
                │     ▼                   │
                │                         │
                │     ▲                   │
                │     │                   │
                │   heap          ▲       │  <CURRENTLY LEARNING / GROWING>
                ├─────────────────────────┤
                │   .bss                  │  <UNINITIALIZED — TBD / WISHLIST>
                │   .data                 │  <CONSTANTS — PRINCIPLES I HOLD>
                │   .rodata               │  <READ-ONLY — THINGS I BELIEVE>
                │   .text                 │  <ENTRY — WHAT I DO DAY-TO-DAY>
0x000000400000  └─────────────────────────┘  ← entry point
```

```ini
[identity]
name      = <YOUR NAME>
role      = <YOUR ROLE>
location  = <CITY, COUNTRY>
ask_me    = <TOPICS YOU LOVE>
fun_fact  = <SOMETHING QUIRKY>
```

## ╭─ stack  ::  linked libraries

<div align="center">

![C](https://img.shields.io/badge/-C-A8B9CC?style=for-the-badge&logo=c&logoColor=black)
![C++](https://img.shields.io/badge/-C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![Rust](https://img.shields.io/badge/-Rust-000000?style=for-the-badge&logo=rust&logoColor=white)
![Python](https://img.shields.io/badge/-Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![CUDA](https://img.shields.io/badge/-CUDA-76B900?style=for-the-badge&logo=nvidia&logoColor=white)
![ROCm](https://img.shields.io/badge/-ROCm-ED1C24?style=for-the-badge&logo=amd&logoColor=white)
![Linux](https://img.shields.io/badge/-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![GDB](https://img.shields.io/badge/-GDB-A42E2B?style=for-the-badge&logo=gnu&logoColor=white)
![Docker](https://img.shields.io/badge/-Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/-Git-F05032?style=for-the-badge&logo=git&logoColor=white)

</div>

## ╭─ scheduler  ::  what's running

```
                  t →
T0  <FOCUS A>   ━━●━━━━━━━━●━━━━━━━━━●━━━━━━━━━━━ acquire
T1  <FOCUS B>   ━━━━●━━━━━━│━━━━●━━━━│━━━━━━━━━━━ wait
T2  <FOCUS C>   ━━━━━━●━━━━│━━━━━━●━━│━━━━━━━━━━━ wait
T3  <FOCUS D>   ━━━━━━━━●━━│━━━━━━━━●│━━━━━━━━━━━ wait
                           ▼          ▼
                        [mutex]    [mutex]
                           │          │
                        ┌──┴──┐    ┌──┴──┐
                        ▼     ▼    ▼     ▼
                       CAS  futex barrier  cv.notify
```

> _Each lane is something I'm actively working on. Replace the `<FOCUS *>`
>  labels with current projects, side quests, or research threads._

## ╭─ pipeline  ::  in flight

```
   cycle →     1     2     3     4     5     6     7
            ┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
   IDEA     │ p₁  │ p₂  │ p₃  │ p₄  │ p₅  │ p₆  │ p₇  │
            ├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
   DESIGN   │     │ p₁  │ p₂  │ p₃  │ p₄  │ p₅  │ p₆  │
            ├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
   BUILD    │     │     │ p₁  │ p₂  │▓p₃▓│ p₄  │ p₅  │   ← stall (debugging)
            ├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
   TEST     │     │     │     │ p₁  │ p₂  │     │ p₄  │
            ├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
   SHIP     │     │     │     │     │ p₁  │ p₂  │     │
            └─────┴─────┴─────┴─────┴─────┴─────┴─────┘
                                          hazard ↑  bubble
```

| project | stage  | notes                          |
|---------|--------|--------------------------------|
| `p₁`    | SHIP   | <PROJECT NAME / ONE-LINER>     |
| `p₂`    | SHIP   | <PROJECT NAME / ONE-LINER>     |
| `p₃`    | BUILD  | <PROJECT NAME — stalled, WHY>  |
| `p₄`    | TEST   | <PROJECT NAME / ONE-LINER>     |
| `p₅`    | BUILD  | <PROJECT NAME / ONE-LINER>     |

## ╭─ telemetry  ::  github stats

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=Abuudiii&show_icons=true&hide_border=true&theme=tokyonight&include_all_commits=true&count_private=true" />
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Abuudiii&layout=compact&hide_border=true&theme=tokyonight&langs_count=8" />

<br/>

<img src="https://github-readme-streak-stats.herokuapp.com/?user=Abuudiii&hide_border=true&theme=tokyonight" alt="streak" />

</div>

## ╭─ trace  ::  contribution graph

<!-- snake animation: needs Platane/snk workflow in .github/workflows -->
<div align="center">
  <img src="https://raw.githubusercontent.com/Abuudiii/Abuudiii/output/github-contribution-grid-snake-dark.svg" alt="contribution snake" />
</div>

## ╭─ syscall  ::  connect

<div align="center">

<a href="mailto:YOUR_EMAIL_HERE">
  <img src="https://img.shields.io/badge/-mail-EA4335?style=for-the-badge&logo=gmail&logoColor=white" />
</a>
<a href="https://www.linkedin.com/in/YOUR_HANDLE">
  <img src="https://img.shields.io/badge/-linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" />
</a>
<a href="https://YOUR-WEBSITE.com">
  <img src="https://img.shields.io/badge/-web-000000?style=for-the-badge&logo=googlechrome&logoColor=white" />
</a>

<br/><br/>

<img src="https://komarev.com/ghpvc/?username=Abuudiii&style=flat-square&color=58A6FF&label=visitors" />

</div>

<div align="center">
<sub><code>$ exit 0</code></sub>
</div>
