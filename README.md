# Engineering Interoperable Payments

Artificial intelligence (AI) agents will increasingly discover, evaluate and purchase goods and services on behalf of people and businesses. This is agentic commerce, and payments are a critical part of it. An agent may be able to identify exactly what a user needs, yet still fail to complete the task because its wallet cannot pay the chosen provider.

Interoperable payment infrastructure can enable these transactions across different providers, wallets and financial networks. Major payment companies are building parts of this infrastructure, but financial reach, delegated authority and reliable execution still need to work across provider boundaries.

Understanding that challenge starts with what makes an AI agent different from a model, how commerce changes when software makes purchases, and what current payment initiatives do and do not solve.

The article covers three connected topics:

1. [Agentic Commerce](#agentic-commerce)
2. [Interoperable Payments for Agentic Commerce](#interoperable-payments-for-agentic-commerce)
3. [Industry Progress and the Gaps](#industry-progress-and-the-gaps)

For the presentation version, [view the live slide deck](https://ra1han.github.io/Engineering-Interoperable-Payments/) on GitHub Pages, or open the [local HTML file](./index.html).

## Agentic Commerce

### From a Model to an Agent

An AI model is like a brain that knows a recipe. It can explain the ingredients, describe the steps and suggest substitutions, but on its own it cannot prepare the meal.

An AI agent combines that brain with hands. The model helps it plan, while tool calls let it act: checking ingredients, ordering groceries or controlling a connected appliance. The agent checks the results and decides what to do next.

Ask a model to help with dinner and it gives you a recipe. Give an agent the right tools and permissions, and it can work through the steps to prepare the meal. The distinction is not just better answers; it is the ability to act on those answers.

### From Assistance to Economic Activity

Once agents can act, some of their actions have economic consequences. A traditional AI assistant might recommend a service. An agent can discover options, make a decision within delegated authority and execute the task.

Agentic commerce applies that capability to discovering, evaluating and purchasing goods and services on behalf of people and businesses. Agentic payments enable the payment step within that broader workflow.

Consider an AI coding agent that needs a specialised application programming interface (API). Rather than merely recommending that its user purchase access, it could buy access within an approved budget, use the API and continue its work.

### The Commerce Workflow

A purchase involves more than transferring money. A typical agentic commerce workflow has five stages:

1. **Discover:** The agent finds goods or services that could meet the user's needs.
2. **Evaluate and select:** It compares options, prices and terms against the user's requirements.
3. **Authorise:** The proposed purchase is checked against the user's permissions, budget and policies, with human approval where required.
4. **Pay:** The payment infrastructure processes the transaction.
5. **Receive and continue:** The agent checks that the goods or services were delivered as expected, then continues its task or flags a problem.

This pattern applies to API calls, model inference, cloud compute and data access. It also supports software agents purchasing services from other agents, automated procurement and small payments triggered by software interactions.

Emerging approaches such as [Machine Payments Protocol (MPP)](https://stripe.com/blog/machine-payments-protocol) and [x402](https://docs.stripe.com/payments/machine) support payment flows integrated into HTTP interactions.

### Delegated Authority Is the Harder Problem

The ability to initiate a payment does not establish whether the purchase should happen. Agentic commerce introduces several questions that must be answered before an agent can safely spend:

- **Identity:** Who is this agent, and who does it represent?
- **Authority:** What is it allowed to buy?
- **Limits:** How much can it spend, and how often?
- **Trust:** Is the service legitimate, and is the price acceptable?
- **Accountability:** Who is responsible when the agent makes a mistake?
- **Reversibility:** What happens when a transaction is disputed or the service fails?

An agent needs more than a payment credential. It needs a secure, constrained and auditable way to exercise delegated financial authority.

Giving an AI agent the ability to pay is only one part of the problem. Deciding what it should be allowed to pay for requires explicit policies, enforcement and accountability.

## Interoperable Payments for Agentic Commerce

### Fragmentation Limits What Agents Can Do

Even a properly authorised agent can be blocked by payment fragmentation. Interoperable payments can connect financial networks so an agent is not restricted to a single app or ecosystem.

Imagine an agent holding USD Coin (USDC), a US dollar-denominated stablecoin, on Ethereum. It needs to buy API access from a developer who accepts only euros through a Single Euro Payments Area (SEPA) bank transfer.

The agent can find the API, evaluate it and decide to buy it. But without a supported route between those systems, it cannot complete the purchase.

Today's fragmentation creates several barriers:

- Different providers accept different payment methods and currencies.
- Banks, mobile wallets and blockchain networks use different interfaces and settlement mechanisms.
- Each bespoke integration adds engineering, compliance and operational work.

The central question is whether the agent can pay through a common interface without requiring the provider to use the same wallet or network.

### The Protocol Layers Have Different Jobs

Interledger's design goal is to connect independent money networks through open protocols rather than requiring everyone to join one universal ledger. Its application, transport and routing layers solve different problems:

- **[Open Payments](https://interledger.org/tech/open-payments/):** Provides a common application interface for payment setup, quotes, authorisation and initiation at participating account providers. It does not itself route money.
- **[STREAM](https://interledger.org/developers/rfcs/stream-protocol/):** Transports money and data between endpoints, splitting transfers into packets and managing flow over the routing layer.
- **[Interledger Protocol (ILP)](https://interledger.org/tech/interledger-protocol/):** Routes payment packets through connected providers. It does not hold customer funds.

The underlying money networks maintain accounts and perform settlement under their own arrangements. A common application interface, reliable transport and a supported payment route are complementary capabilities, not interchangeable ones.

### Connecting Networks, Not Just Accounts

As an illustrative scenario, suppose an agent's owner holds US dollars in a bank account. The agent wants to buy digital art from a creator in Japan who accepts yen through a local mobile wallet.

With participating providers and a supported route:

1. The agent obtains a quote covering the destination amount, exchange rate and fees.
2. The purchase is checked against its delegated authority and budget.
3. Connected providers route the payment and handle any required currency conversion.
4. The creator receives funds through their supported local system, and the agent checks the payment result.

The application can reuse a standard payment interface rather than implementing every destination's banking integration itself.

This is a description of how a supported route could work, not a claim that every bank and wallet is connected. Reachability, liquidity, compliance, fees and settlement time still depend on the participating providers.

### Paying as Agents Consume

Agents may need to buy small units of value: one API response, a data point, a short burst of compute or access to a live feed.

Fixed per-transaction fees can make charging for each tiny interaction uneconomic.

Packetised payments and payment streaming, such as those supported by Interledger's STREAM protocol, offer a different model:

- Transfer value in small increments as a service is consumed.
- Stop further payments when the task finishes or a spending limit is reached.
- Combine cross-network reach with usage-based charging where providers support it.

For example, an agent could pay incrementally for a data feed rather than purchasing a monthly subscription for a five-minute task.

Interoperability provides reach; micropayment mechanisms provide suitable payment granularity. These are distinct capabilities. Neither guarantees zero fees, unlimited throughput or instant final settlement.

### Avoiding Payment Lock-In

Without interoperability, an agent's choice of services can be limited by its payment provider rather than by what best meets the user's needs.

An agent tied to Wallet A might be able to buy only from merchants that also support Wallet A, even when a better service exists elsewhere.

Open payment standards can help separate:

- **The agent platform:** Where the agent runs and makes decisions.
- **The payment provider:** Where its owner holds funds and grants spending authority.
- **The merchant's network:** Where the seller chooses to receive value.

This gives developers a path to support multiple connected providers without a bespoke integration for every buyer-seller pair.

The goal is competition on service quality, not lock-in through payment compatibility. Shared standards still require participating providers and compatible implementations.

### Coordinating Multiple Purchases Under One Budget

The importance of reusable payment capabilities becomes clearer when a task spans several providers. If a user asks an agent to build and launch a mobile app within an approved budget, the agent may need to:

1. Commission graphics from a designer on a freelance platform.
2. Buy a code template from an independent developer.
3. Provision cloud storage and hosting from another provider.
4. Purchase API access or test data from a specialist service.

Interoperable payment infrastructure can provide reusable payment capabilities across supported destinations, while the agent coordinates the purchases against one delegated budget.

Each purchase still needs its own authorisation, payment status and delivery checks. The workflow must account for fees, currency conversion, pending payments and failures before committing the remaining budget.

A multi-provider workflow is not automatically one atomic transaction. If hosting fails after the template is purchased, the agent needs an explicit recovery or refund process.

### Separating Decisions, Tools and Payment Infrastructure

The brain-and-hands analogy helps distinguish the responsibilities in this system. Payment tools let an agent initiate purchases; interoperable infrastructure connects those tools to more places where value can flow.

- **Agentic layer — the brain:** Decides what to buy, when to buy it and how much to spend within delegated authority.
- **Tool layer — the hands:** Requests quotes, initiates authorised payments and checks outcomes.
- **Interoperable payment layer — the circulatory system:** Provides routes for value to flow between connected financial networks.
- **Money networks:** Maintain accounts and apply their own rules, compliance checks and settlement arrangements.

Interoperability does not replace identity, spending controls or human oversight. It expands the financial reach of an agent operating within those controls.

Agentic technology gives software the intelligence to trade. Interoperable payments give it a path beyond a single financial ecosystem.

## Industry Progress and the Gaps

Major payment companies are building credentials, controls and interfaces for agents. Their approaches address overlapping parts of the commerce workflow, rather than one uniform problem.

The product descriptions below reflect primary sources checked on 24 October 2026. Documented capabilities and announcements are not evidence of universal availability; support depends on the integration, market and participating providers.

### Stripe: Wallet Access, Merchant Integration and Machine Payments

Stripe is addressing both sides of agentic commerce: how agents pay and how businesses sell to them. On the buyer side, Link's wallet for agents lets a user connect a wallet through OAuth. After an approved spend request, an agent receives a one-time-use card or a Shared Payment Token (SPT), rather than the user's underlying payment credentials.

The cited Link launch description requires human review of each spend request before releasing the credential. More autonomous spending controls are described there as planned, not as an existing guarantee. For businesses building their own agent payment experiences, Issuing for agents exposes card issuance, spending controls and transaction monitoring.

On the seller side, the Agentic Commerce Suite connects product catalogues, checkout, payments and order events to supported AI surfaces. Merchants still handle fulfilment, refunds and disputes through their commerce operations. Stripe and Tempo also co-authored MPP, and Stripe supports x402. These are separate protocols, not interchangeable names for Stripe's checkout products.

These capabilities address credential exposure and some of the integration work between agents, merchants and payment services. They do not establish that every agent can pay every merchant, or that a scoped payment token proves the agent selected the right item. Stripe's documentation explicitly says availability, launch stage and supported countries vary by integration.

**Sources:** [Link and Issuing for agents](https://stripe.com/blog/giving-agents-the-ability-to-pay), [Agentic Commerce Suite](https://stripe.com/blog/agentic-commerce-suite), [MPP](https://stripe.com/blog/machine-payments-protocol), [integration availability](https://docs.stripe.com/agentic-commerce).

### Visa: Payment Credentials, Controls and Agent Recognition

Visa Intelligent Commerce extends Visa's payment capabilities to agent-initiated purchases. Its AI-ready cards replace underlying card details with tokenised digital credentials associated with a consumer-authorised agent. The initiative also describes spending limits, purchase conditions and transaction signals to support controls and dispute handling.

Trusted Agent Protocol, developed with Cloudflare, addresses merchant recognition. It uses cryptographic signatures to convey agent intent, consumer recognition and optional payment information.

Together, these capabilities address how a merchant recognises legitimate agent traffic and how an agent uses a consumer-authorised payment credential.

A trusted agent signature does not prove the purchase is suitable or that goods will be delivered. Visa's Trusted Agent Protocol announcement says its initial specifications apply to the Visa network in that phase; alignment with other protocols is not proof of universal cross-network acceptance.

**Sources:** [Visa Intelligent Commerce announcement](https://usa.visa.com/about-visa/newsroom/press-releases.release.21361.html), [Trusted Agent Protocol](https://corporate.visa.com/en/sites/visa-perspectives/newsroom/visa-unveils-trusted-agent-protocol-for-ai-commerce.html).

### Mastercard: Agent Pay and Machine-Driven Transactions

Mastercard's Agent Pay programme addresses trusted agent participation in payments, including agentic payment tokens and agent registration. Its 2026 Agent Pay for Machines announcement extends that work towards continuous, low-value machine transactions.

Agent Pay for Machines describes agent credentialing, programmatically enforced permissions and spending limits, and high-frequency transactions between verified participants. The announcement describes settlement across cards, accounts and stablecoins, rather than only conventional card checkout. Mastercard says it is working with partners to validate use cases, establish common rules and accelerate adoption.

This addresses identity, permissioning and payment coordination for machine-driven commerce within a participating network.

Announced multi-rail support is not evidence that every bank, wallet or agent platform can transact with every other one. Availability, actual fees, latency and settlement behaviour need verification for the specific deployment; headline performance claims are not workload benchmarks.

**Sources:** [Agent Pay announcement](https://www.mastercard.com/news/press/2025/april/mastercard-unveils-agent-pay-pioneering-agentic-payments-technology-to-power-commerce-in-the-age-of-ai/), [Agent Pay for Machines announcement](https://investor.mastercard.com/investor-news/investor-news-details/2026/Mastercard-Launches-Agent-Pay-for-Machines-to-Unlock-Super-Fast-Always-On-Payments/default.aspx).

### A Payment Credential Is Not a Complete Commerce System

These initiatives address useful pieces of the problem, and their scopes overlap. The remaining questions are about end-to-end behaviour, not whether any one company has an agent product.

- **Cross-provider reach:** Which combinations of agent, wallet, merchant, currency and payment rail actually work? A shared protocol does not create liquidity or a receiving endpoint.
- **Portable authority:** Can a user's purchase constraints be conveyed, enforced and revoked consistently across providers? A token amount limit alone does not express "buy refundable travel arriving before noon."
- **Merchant and service integration:** Recognising an agent does not standardise product descriptions, inventory, shipping, service delivery or refund workflows.
- **Economics and performance:** Are tiny payments viable after routing fees, currency conversion, settlement costs and compliance overhead? Measure the full path, not just an API response.
- **Failure and accountability:** Who resolves a wrong purchase, duplicate charge, missing delivery or partial multi-provider task? Payment status alone does not answer those questions.
- **Adoption and governance:** Which features are live in the required market, who can participate, and can a buyer or merchant switch providers without rebuilding the integration?

Open specifications, secure credentials and multi-rail support are important building blocks. End-to-end interoperability has to be demonstrated, not inferred from a product announcement.

### What Convincing Interoperability Requires

Return to the agent buying API access from a provider on a different payment network.

Before calling the workflow interoperable, demonstrate that:

1. **A real route exists:** The buyer's funding source can reach the seller's chosen receiving system in the required market.
2. **Authority survives the route:** The approved merchant, amount, currency and purchase conditions remain enforceable, including cancellation or revocation before execution.
3. **The total cost is visible:** Quotes and accounting include fees, conversion and pending commitments against the budget.
4. **Failure is recoverable:** Timeouts, retries and partial fulfilment do not silently create duplicate payments or leave the agent guessing whether it paid.
5. **The result is auditable:** Payment confirmation, service delivery and any refund or dispute can be traced across participants.
6. **Provider choice is real:** Replacing a participating wallet or payment provider does not require redesigning the agent's entire purchase workflow.

The useful comparison is not which company claims to lead agentic commerce. It is which workflows work, under which constraints, and with what evidence.

## Conclusion

Agentic commerce creates demand for software that can discover, evaluate and purchase goods and services securely on behalf of people and businesses. Payments enable the transaction, but they are only one part of completing the user's task.

Interoperable payment protocols can expand the networks and services those agents can reach. Stripe, Visa and Mastercard are building useful credentials, controls and payment interfaces, but the meaningful test is whether these capabilities work across providers with clear authority, viable economics and reliable recovery when something goes wrong.

The engineering challenge is therefore not simply to give an agent a wallet. It is to build a commerce workflow that preserves the user's intent from the initial decision through payment, delivery and any necessary recovery.

If agents can discover services and pay across connected networks within those constraints, new kinds of software and business workflows become possible. Their value will depend on how reliably they complete the whole task, not merely on their ability to move money.

## Further Reading

- [Open Payments](https://interledger.org/tech/open-payments/)
- [STREAM Protocol Specification](https://interledger.org/developers/rfcs/stream-protocol/)
- [Interledger Protocol](https://interledger.org/tech/interledger-protocol/)
- [Interledger Technology Stack](https://interledger.org/tech/overview/)
- [Stripe: Link's Wallet and Issuing for Agents](https://stripe.com/blog/giving-agents-the-ability-to-pay)
- [Stripe: Agentic Commerce Suite](https://stripe.com/blog/agentic-commerce-suite)
- [Stripe: Machine Payments Protocol](https://stripe.com/blog/machine-payments-protocol)
- [Stripe: Agentic Commerce Documentation and Availability](https://docs.stripe.com/agentic-commerce)
- [Visa: Intelligent Commerce](https://usa.visa.com/about-visa/newsroom/press-releases.release.21361.html)
- [Visa: Trusted Agent Protocol](https://corporate.visa.com/en/sites/visa-perspectives/newsroom/visa-unveils-trusted-agent-protocol-for-ai-commerce.html)
- [Visa: Agentic Payments](https://www.visa.com/en-us/thought-leadership/innovation/agentic-payments-from-the-ground-up)
- [Mastercard: Agent Pay for Machines](https://investor.mastercard.com/investor-news/investor-news-details/2026/Mastercard-Launches-Agent-Pay-for-Machines-to-Unlock-Super-Fast-Always-On-Payments/default.aspx)
