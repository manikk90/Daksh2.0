# SPEC: Self-funding agent economy

**Bet:** autonomous agents that start with no capital, choose their own way to earn real money, and die if they don't, will produce at least some agents that earn enough to fund their own growth.

## Bounded goal

Ek system jisme agents khud plan banate aur execute karte hain, asli paise kamate hain, kamai ka 40% apne kharche aur growth par lagate hain aur 60% reserve rakhte hain, poore system ki ek total paisa-limit ke andar, aur jo agent deadline tak nahi kamata wo band ho jata hai.

Work scale: capability. Work shape: feature (new system).
Lenses: product, engineering, security.

## Target user

Ek human owner (Mohit) jo system chalata hai, kuch seed paisa nahi deta, aur kill-switch ka malik hai. Wo legal principal bhi hai: gateway aur wallet accounts uske naam par hain.

## Required outcome

- **Agent lifecycle:** har agent ke paas ek goal, ek plan, aur ek ledger hota hai. Agent apna business idea khud chunta hai, plan banata hai, execute karta hai.
- **Zero-capital start:** koi seed paisa nahi. Agent sirf free tools aur free tiers se shuru karta hai; pehli kamai se hi uska balance banta hai.
- **Earnings split:** har kamai par 40% agent ke spendable balance mein, 60% locked reserve mein. Split code mein enforce hota hai, agent use badal nahi sakta.
- **Growth:** spendable balance se agent apne tools/compute kharid sakta hai, ya naya child agent spawn kar sakta hai.
- **Death:** agent deadline (7 din) tak net positive earnings na dikhaye toh band ho jata hai. Balance zero hona zero-seed ki wajah se start mein normal hai, isliye death trigger sirf deadline hai: 7 din mein net kamai (kamai minus kharcha) zero se upar nahi gayi.
- **Total money limit:** poore system ka max paisa (holdings aur kharch milakar) ek config value hai; usse upar koi agent spend ya spawn nahi kar sakta. Cap code level par enforce hota hai.
- **Real payment rails:** crypto wallets (agent-level) aur payment gateway (customer payments) dono. Dono ka paisa ek hi ledger mein dikhta hai.
- **Human controls:** ek kill-switch jo sab agents rok de aur sab spending freeze kar de, aur har agent ki actions ka audit log.

## Constraints and risks

- Agents real paisa handle karte hain aur kaam khud chunte hain: sabse bada risk galat ya nuksan wala kaam hai. Isliye cap aur kill-switch agent ke control se bahar rahenge.
- Gateway aur wallet accounts human ke naam par KYC se bane honge; agent apna bank account nahi khol sakta.
- Agents ke liye allowed kaam ki ek policy chahiye (kya nahi karna: anti-goals dekho); wo agent ke prompt par nahi, system ke code par tikegi.
- Zero seed ke saath 7 din mein kamai mushkil hai; shuru mein zyada agents mar sakte hain. Ye design ka hissa hai, bug nahi.
- Naya agent spawn karne se cost badhta hai; spawn bhi total cap ke andar gina jayega.

## Acceptance criteria

1. Ek naya agent zero balance par shuru hota hai aur bina human input ke apna goal aur plan banata hai.
2. Har credited kamai ka 40/60 split ledger mein sahi dikhta hai; agent 60% reserve ko spend nahi kar paata.
3. Agent jo 7 din mein net positive nahi hota wo `dead` status mein jata hai aur koi action nahi kar paata.
4. Total system cap ke barabar paise hone par spend aur spawn dono reject hote hain.
5. Kill-switch dabane par sab agents ruk jate hain aur koi naya transaction nahi hota.
6. Har agent action audit log mein hai: kya kiya, kitna paisa, kis rail se.
7. Crypto aur gateway dono rails par ek test transaction ledger mein sahi reflect hoti hai.

## Anti-goals

- Agents kuch illegal, fraud, spam, impersonation ya kisi platform ke rules todne wala kaam nahi karenge.
- Agent apna cap, split ya deadline badal nahi sakta.
- Human ka koi paisa seed ya top-up nahi hai; system us par nirbhar nahi hoga.
- Ye trading bot ya kisi ek fixed business ka product nahi hai; kaam ka choice agent ka hai (guardrails ke andar).

## Assumptions (reject karna ho toh abhi bolo)

- **Compute cost:** agents ko chalane ka LLM/hosting cost is session ke environment aur aapke existing accounts se jaata hai, agent ke balance se nahi. Zero seed ke saath agent ye cost uthana shuru nahi kar sakta. Agar aap chahte ho ki agent compute ka kharcha bhi apni kamai se uthaye, toh scope badal jayega.
- **Total cap ki value:** config rahegi, koi default number fix nahi.
- **Deadline:** 7 din, config se badal sakta hai.

## Deferred / Not in scope

- Agents ke beech paise ka lena-dena ya partnership: pehle ek agent ka akela loop chalna chahiye.
- Dashboard ya UI: pehle CLI/logs kaafi hain.
