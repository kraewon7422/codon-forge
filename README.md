# Codon Forge

A browser puzzle game about gene expression. Start from DNA and make a protein yourself: pick the template
strand, find the promoter, splice out introns, cap the mRNA, then run the ribosome codon by codon. Every
level uses the real rules, and most use **real human gene sequences checked against NCBI**.

**▶ Play it: https://kraewon7422.github.io/codon-forge/codon-forge.html**

One HTML file, no build step, no libraries. A Korean guide follows the English one below.

New players get a 30-second taste first: be the ribosome for the first four codons of insulin. The home page is a
3-D DNA helix you can spin; its six stretches are the six chapters. Every level shows where it sits in
DNA → pre-mRNA → mRNA → protein, and which real gene it uses.

## Why I made it

My earlier game, [Protein Origami](https://github.com/kraewon7422/protein-origami), is about how a chain of
amino acids folds. This one asks the question before that: where does the chain come from? I wanted to
do each step of gene expression by hand, with real genes, so that the rules (antiparallel strands, GU…AG,
wobble, Kozak) stop being things to memorise and become things you use.

## Play

Open `codon-forge.html` in any modern browser (desktop or phone). Progress is saved in the browser.

| Chapter | What you do | Real genes used |
|---|---|---|
| 1 · Central dogma | pair bases, write the reverse complement, transcribe, sort prokaryote vs eukaryote | OXT, LYZ, GFP |
| 2 · Transcription | pick the template strand, find the TATA box and +1, handle a gene on the other strand | TP53, MB |
| 3 · RNA processing | cut introns with decoy GU/AG sites, find the branch point, cap and poly-A | **HBB intron 1 (130 nt)** |
| 4 · Translation | run the ribosome: A/P/E sites, wobble, inosine, release factor | UBB, GFP chromophore, collagen, insulin |
| 5 · Start-site traps | scanning from the cap, Kozak context, leaky scanning, uORFs | INS 5′ UTR |
| 6 · Mutation lab | classify and repair real disease mutations | HBB sickle cell, CFTR ΔF508, β-thalassaemia IVS1-1, BRCA1 185delAG |

- **Stars:** ★ finish · ★ at most one mistake · ★ no hint (the hint in translation levels is the codon table).
- **Protein codex:** each level unlocks a card for its protein (11 in total): role, a fact, the full sequence,
  and mass.
- **Sandbox:** paste any DNA or FASTA. All six reading frames are translated and ORFs are drawn as bars.
- **Time attack:** 60 seconds of "which tRNA reads this codon?", including wobble and inosine. Every 5 in a row adds 2 seconds.
- **Keys:** letters type bases · `1`–`9` pick an option or tRNA · `Space` translocates · `H` hint · `Esc` back.
- Korean and English (`KO · EN` button).

## The rules in the game

| Step | Rule |
|---|---|
| Transcription | the template is read 3′→5′, RNA grows 5′→3′. TATA box ≈ 25–30 nt above +1, +1 = the A of the initiator (YYANWYY) |
| 5′ splice site | GU, with at least 3 of 5 consensus positions (AG\|GURAGU) |
| 3′ splice site | AG with a polypyrimidine tract (≥ 8 of the 12 nt before it are C/U) and a branch-point A (yUnAy) 18–40 nt upstream |
| Poly-A | cut right after a CA, 10–30 nt past AAUAAA |
| Wobble | anticodon 5′ base C→G, A→U, U→A/G, G→U/C, I→U/C/A |
| Start | the first AUG from the cap that is not in a weak Kozak context (no purine at −3 and no G at +4 = weak, skipped) |

These are textbook consensus rules, simplified so they can be checked. Real splicing and start-site choice
depend on more signals than these.

## Sequences

All real sequences were fetched from NCBI on 2026-11-03, and the built-in tests check that each CDS
translates to the matching protein record.

| Gene | Record | Used for |
|---|---|---|
| INS | NM_000207.3 → NP_000198.1 | 5′ UTR scanning, A-chain end + stop |
| HBB | NM_000518.5 → NP_000509.1, intron 1 from NC_000011.10 | splicing, sickle cell, β-thalassaemia |
| CFTR | NM_000492.4 c.1507–1536 | ΔF508 |
| BRCA1 | NM_007294.4 c.49–123 | 185delAG (p.Glu23ValfsTer17) |
| UBB, TP53, MB, OXT, LYZ | NM_018955.4, NM_000546.6, NM_005368.3, NM_000915.4, NM_000239.3 | early chapters, codex |
| COL1A1 | NM_000088.4 codons 142–151 | Gly-Pro-Pro repeats (inosine) |
| GFP | M62653.1 codons 61–70 | the Ser65-Tyr66-Gly67 chromophore (wobble) |

Short pieces of genes are cut out so they fit on a phone. The game says so on each level. Sequences that are
not real (promoters, decoy introns, Kozak and uORF puzzles) are labelled "synthetic teaching sequence".

## Protein Origami link

Result cards, the codex and the sandbox have a **Fold it** button that opens the chain in
[Protein Origami](https://kraewon7422.github.io/protein-origami/protein-origami.html) through its `?seq=` link.
Each residue becomes H if its Kyte–Doolittle hydropathy is above 0 (I V L F C M A) and P otherwise. Origami folds
4–48 beads, so long proteins send a meaningful piece: the 9-residue oxytocin hormone, the 30-residue insulin
B chain, or otherwise residues 1–40.

## Tests

Open `codon-forge.html?test=1`. 39 tests run in the page, including:

- genetic code (64 codons, 61 sense, codon counts per amino acid), wobble table, reverse complement
- real sequences translate to their NCBI proteins; HBB intron 1 is found at exactly 130 nt with its branch point 37 nt from the 3′ end
- each mutation is classified correctly (HbS missense, ΔF508 in-frame, IVS1-1 splice site, 185delAG frameshift with the stop at codon 39)
- six-frame ORF finder, ribosome A→P→E state machine, stop codons reject tRNAs
- every level has exactly one answer and is solvable, and the UI plays all 24 levels to 3 stars in both languages
- every base and amino-acid label passes 4.5:1 contrast, the intro plays M-A-L-W, and every Origami link is a valid 4–48 bead chain

## Licence

MIT

---

# Codon Forge (한국어)

유전자 발현 퍼즐 게임이에요. DNA에서 출발해 단백질을 직접 만들어요. 주형 가닥을 고르고, 프로모터를 찾고,
인트론을 잘라내고, 캡을 붙이고, 리보솜을 코돈 하나씩 돌려요. 규칙은 모두 실제 생물학 규칙이고, 대부분의
레벨이 **NCBI에서 확인한 실제 사람 유전자 서열**을 써요.

**▶ 플레이: https://kraewon7422.github.io/codon-forge/codon-forge.html**

HTML 파일 하나로 돼 있고, 빌드나 라이브러리가 없어요.

처음 열면 30초 맛보기로 인슐린의 첫 코돈 4개를 직접 번역해 봐요. 첫 화면은 돌려 볼 수 있는 3D DNA 나선이고,
나선의 여섯 구간이 여섯 장이에요. 레벨마다 DNA → pre-mRNA → mRNA → 단백질 중 어디를 하고 있는지와 어떤
실제 유전자인지 위에 보여 줘요.

## 만든 이유

먼저 만든 [Protein Origami](https://github.com/kraewon7422/protein-origami)는 아미노산 사슬이 어떻게 접히는지를
다뤄요. 이번엔 그 앞의 질문, "그 사슬은 어디서 오나?"를 다뤄요. 역평행, GU…AG, 워블, Kozak 같은 규칙을
외우는 대신 직접 써 보면서 익히려고 만들었어요.

## 하는 법

브라우저(PC·휴대폰)에서 `codon-forge.html`을 열면 돼요. 진행 상황은 브라우저에 저장돼요.

- **6장 24레벨:** 중심 원리 → 전사 → RNA 가공 → 번역 → 개시의 함정 → 돌연변이 실험실
- **별:** ★ 완성 · ★ 실수 1번 이하 · ★ 힌트 안 씀 (번역 레벨의 힌트는 코돈표)
- **단백질 도감:** 레벨을 깨면 그 레벨의 실제 단백질 카드(11종)가 열려요. 역할, 재미있는 사실, 전체 서열, 질량이 담겨 있어요.
- **Protein Origami에서 접기:** 결과 카드·도감·샌드박스의 버튼으로 만든 사슬을 [Protein Origami](https://kraewon7422.github.io/protein-origami/protein-origami.html)에서 바로 접어 봐요. 긴 단백질은 의미 있는 조각(옥시토신 9개, 인슐린 B 사슬 30개, 그 외 1–40번)을 보내요.
- **샌드박스:** DNA나 FASTA를 붙여넣으면 6개 읽기틀을 모두 번역해 ORF를 막대로 보여줘요.
- **타임 어택:** 60초 동안 "이 코돈을 읽는 tRNA는?" (워블·이노신 포함). 5개 연속 정답마다 +2초
- **키:** 글자 = 염기 입력 · `1`–`9` 선택 · `Space` 전위 · `H` 힌트 · `Esc` 뒤로
- 한국어 / 영어 (`KO · EN` 버튼)

## 서열과 정확성

실제 서열은 2026-11-03에 NCBI에서 받았고, 내장 테스트가 각 CDS의 번역이 NCBI 단백질과 같은지 확인해요.
휴대폰에 맞게 유전자의 일부만 잘라 쓴 레벨은 화면에 그렇게 표시돼 있어요. 실제가 아닌 서열(프로모터,
미끼 인트론, Kozak·uORF 퍼즐)은 "교육용 합성 서열"로 표시돼 있어요. 게임 규칙은 교과서의 공통 서열 규칙을
확인할 수 있게 단순화한 것이에요.

## 테스트

`codon-forge.html?test=1`을 열면 39개 테스트가 페이지 안에서 돌아요. 24개 레벨을 두 언어로 모두 별 3개로
깨는 UI 자동 플레이도 포함돼 있어요.

## 라이선스

MIT
