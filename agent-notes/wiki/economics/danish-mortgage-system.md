---
source: agent
compiled_from:
  - agent-notes/raw/economics/2026-03-20-danish-fix-for-us-mortgage-lock-in.md
  - agent-notes/raw/economics/2009-09-26-danish-mortgage-model.md
  - agent-notes/raw/economics/2023-03-22-in-praise-of-danish-mortgage-system.md
compiled_at: 2026-04-05
model: claude-opus-4-6
confidence: medium
---

# Danish Mortgage System

Denmark's mortgage market operates on a **correspondence principle** (also called the "match-funding principle"): every mortgage is directly backed by a tradeable bond with matching cash-flow properties. As JYSKE Bank describes it, "for every loan made by the mortgage bank, a new bond is issued with matching cash-flow properties." This clean separation means mortgage banks function more like clearinghouses than traditional lenders — they assume credit risk but not interest rate risk. The division of labor has kept the Danish system remarkably stable: the Danish Mortgage Bond Market dates to **1797**, has **zero defaults** on record, and currently holds approximately €402 billion in value, making it Europe's largest mortgage bond market.

## The Repurchase Option

The system's most distinctive feature is **market-rate prepayment**. Unlike in the U.S., where borrowers can only prepay at par (the full face value of the loan), Danish borrowers can buy back their corresponding bond at its current market price. This is symmetric: when rates fall, the bond trades above par and prepayment is expensive (just as in the U.S.); but when rates rise, the bond trades below par, and borrowers can extinguish their mortgage at a discount.

Concretely: a $500k mortgage originated at 3% drops to roughly $358k in bond-market value if rates rise to 6%. The borrower can purchase the bond at that price and walk away from the mortgage — a powerful exit valve that simply doesn't exist in American housing finance. As Tabarrok notes (crediting Patrick McKenzie's observation), since home values also tend to decline when rates rise, the repurchase option provides a **natural insurance** hedge: the borrower's mortgage liability shrinks in tandem with their asset value.

Cowen characterizes the repurchase option as creating "a new contingent claims market for homeowners who do not understand how to use interest rate futures and options" — in effect, implicit insurance against negative equity baked into the mortgage product itself. The process requires several weeks' advance notice to mortgage credit institutions, which then designate specific bonds via lottery for purchase.

## U.S. Mortgage Lock-In

The absence of this mechanism in the U.S. creates severe **rate lock-in**. Homeowners who locked in low rates during 2020–2021 face a steep implicit cost to move: selling means giving up a 3% mortgage and taking on a 6–7% one. Tabarrok highlights research by Fonseca and Liu showing that a 1 percentage point gap between locked-in and current rates reduces household mobility by 9% overall, and by 16% in the 2022–2024 period.

This lock-in ripples through the economy: reduced labor mobility, constrained housing supply (owners stay put), and misallocation of housing stock (empty-nesters in family homes, growing families in starter homes).

## Empirical Evidence from Denmark

Berger, Jeong, Marx, Olesen, and Tourre (2026) compare Danish and U.S. mobility patterns directly. Their key finding: Danish household mobility is largely insensitive to the gap between existing mortgage rates and prevailing market rates — the lock-in effect that dominates U.S. housing decisions essentially vanishes when borrowers have the repurchase option.

The cost of grafting this feature onto U.S. mortgages would be modest — an estimated **18 basis points** increase in mortgage rates on average. The net benefit flows overwhelmingly to borrowers, with minimal impact on lender returns.

## Implications

The Danish system suggests that U.S. mortgage lock-in is a policy choice, not an inevitable feature of housing finance. The correspondence principle and bond-backed prepayment have been operational in Denmark for over 200 years, providing a well-tested template. The primary obstacle to adoption in the U.S. is structural: Fannie Mae and Freddie Mac's dominance in securitization and the political economy of mortgage market reform.

## Institutional Design

Beyond the repurchase option, Cowen (drawing on Pozen's *Too Big to Save?*) highlights several structural features that underpin Danish mortgage stability:

- **Skin in the game**: originators retain financial interest even after securitization, unlike the U.S. originate-to-distribute model that fueled the 2008 crisis.
- **Transparency and simplicity**: emphasis on plain vanilla products rather than complex structured instruments.
- **Speedy repossession**: swift property recovery for defaults reduces lender risk and keeps credit flowing.
- **Designated institutions**: only explicitly designated mortgage credit institutions can originate, creating a regulated and accountable market structure.

## Sources

- Cowen, Tyler (2009). "The Danish Mortgage Model." <https://marginalrevolution.com/marginalrevolution/2009/09/the-danish-mortgage-model.html> — [[2009-09-26-danish-mortgage-model|local copy]]
- Tabarrok, Alex (2023). "In Praise of the Danish Mortgage System." <https://marginalrevolution.com/marginalrevolution/2023/03/in-praise-of-the-danish-mortgage-system.html> — [[2023-03-22-in-praise-of-danish-mortgage-system|local copy]]
- Tabarrok, Alex (2026). "A Danish Fix for U.S. Mortgage Lock-in." <https://marginalrevolution.com/marginalrevolution/2026/03/a-danish-fix-for-u-s-mortgage-lock-in.html> — [[2026-03-20-danish-fix-for-us-mortgage-lock-in|local copy]]
