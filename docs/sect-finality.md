---
title: -chap-num- Finality
---

import Pseudocode from '@site/src/components/Pseudocode';
import initiateGrandpa from '!!raw-loader!@site/src/algorithms/initiateGrandpa.tex';
import playGrandpaRound from '!!raw-loader!@site/src/algorithms/playGrandpaRound.tex';
import derivePrimary from '!!raw-loader!@site/src/algorithms/derivePrimary.tex';
import bestFinalCandidate from '!!raw-loader!@site/src/algorithms/bestFinalCandidate.tex';
import grandpaGhost from '!!raw-loader!@site/src/algorithms/grandpaGhost.tex';
import bestPrevoteCandidate from '!!raw-loader!@site/src/algorithms/bestPrevoteCandidate.tex';
import attemptToFinalizeAtRound from '!!raw-loader!@site/src/algorithms/attemptToFinalizeAtRound.tex';
import finalizable from '!!raw-loader!@site/src/algorithms/finalizable.tex';
import processCatchupRequest from '!!raw-loader!@site/src/algorithms/processCatchupRequest.tex';
import processCatchupResponse from '!!raw-loader!@site/src/algorithms/processCatchupResponse.tex';

## -sec-num- Introduction {#id-introduction-4}

The Polkadot Host uses GRANDPA Finality protocol to finalize blocks. Finality is obtained by consecutive rounds of voting by the validator nodes. Validators execute GRANDPA finality process in parallel to Block Production as an independent service. In this section, we describe the different functions that GRANDPA service performs to successfully participate in the block-finalization process.

###### Definition -def-num- GRANDPA Voter {#defn-grandpa-voter}
:::definition

A **GRANDPA Voter**, ${v}$, represented by a key pair ${\left({{K}_{{v}}^{{\text{pr}}}},{v}_{{\text{id}}}\right)}$ where ${{k}_{{v}}^{{\text{pr}}}}$ represents an *ed25519* private key, is a node running a GRANDPA protocol and broadcasting votes to finalize blocks in a Polkadot Host-based chain. The **set of all GRANDPA voters** for a given block B is indicated by ${\mathbb{{V}}}_{{B}}$. In that regard, we have \[To do: change function name, only call at genesis, adjust V_B over the sections\]

$$
{\mathbb{{V}}}={\tt{grandpa\_authorities}}{\left({B}\right)}
$$

where ${\tt{grandpa\_authorities}}$ is a function entrypoint of the Runtime described in [Section -sec-num-ref-](chap-runtime-api#sect-rte-grandpa-auth). We refer to ${\mathbb{{V}}}_{{B}}$ as ${\mathbb{{V}}}$ when there is no chance of ambiguity.

Analogously we say that a Polkadot node is a **non-voter node** for block ${B}$, if it does not own any of the key pairs in ${\mathbb{{V}}}_{{B}}$.

:::
###### Definition -def-num- Authority Set Id {#defn-authority-set-id}
:::definition

The **authority set Id** ($\text{id}_{{{\mathbb{{V}}}}}$) is an incremental counter which tracks the amount of authority list changes that occurred ([Definition -def-num-ref-](sect-finality#defn-consensus-message-grandpa)). Starting with the value of zero at genesis, the Polkadot Host increments this value by one every time a **Scheduled Change** or a **Forced Change** occurs. The authority set Id is an unsigned 64-bit integer.

:::
###### Definition -def-num- GRANDPA State {#defn-grandpa-state}
:::definition

The **GRANDPA state**, $\text{GS}$, is defined as:

$$
\text{GS}\:={\left\lbrace{\mathbb{{V}}},\text{id}_{{{\mathbb{{V}}}}},{r}\right\rbrace}
$$

**where**  
- ${\mathbb{{V}}}$: is the set of voters.

- $\text{id}_{{{\mathbb{{V}}}}}$: is the authority set ID ([Definition -def-num-ref-](sect-finality#defn-authority-set-id)).

- ${r}$: is the voting round number.

:::
###### Definition -def-num- GRANDPA Vote {#defn-vote}
:::definition

A **GRANDPA vote** or simply a vote for block ${B}$ is an ordered pair defined as

$$
{V}{\left({B}\right)}\:={\left({H}_{{h}}{\left({B}\right)},{H}_{{i}}{\left({B}\right)}\right)}
$$

where ${H}_{{h}}{\left({B}\right)}$ and ${H}_{{i}}{\left({B}\right)}$ are the block hash ([Definition -def-num-ref-](chap-state#defn-block-header-hash)) and the block number ([Definition -def-num-ref-](chap-state#defn-block-header)).

:::
###### Definition -def-num- Voting Rounds {#defn-voting-rounds}
:::definition

Voters engage in a maximum of two sub-rounds of voting for each round ${r}$. The first sub-round is called **pre-vote** and the second sub-round is called **pre-commit**.

By ${{V}_{{v}}^{{{r},\text{pv}}}}$ and ${{V}_{{v}}^{{{r},\text{pc}}}}$ we refer to the vote cast by voter ${v}$ in round ${r}$ (for block ${B}$) during the pre-vote and the pre-commit sub-round respectively.

Voting is done by means of broadcasting voting messages ([Section -sec-num-ref-](chap-networking#sect-msg-grandpa)) to the network. Validators inform their peers about the block finalized in round ${r}$ by broadcasting a commit message ([Play-Grandpa-Round](sect-finality#algo-grandpa-round)).

:::
###### Definition -def-num- Vote Signature {#defn-sign-round-vote}
:::definition

${\text{Sign}_{{{v}_{{i}}}}^{{{r},\text{stage}}}}$ refers to the signature of a voter for a specific message in a round and is formally defined as:

$$
{\text{Sign}_{{{v}_{{i}}}}^{{{r},\text{stage}}}}\:=\text{Sig}_{{\text{ed25519}}}{\left(\text{msg},{r},\text{id}_{{{\mathbb{{V}}}}}\right)}
$$

**where**  
- $\text{msg}$: is a byte array containing the message to be signed ([Definition -def-num-ref-](sect-finality#defn-vote)).

- ${r}$: is an unsigned 64-bit integer is the round number.

- $\text{id}_{{{\mathbb{{V}}}}}$: is an unsigned 64-bit integer indicating the authority set Id ([Definition -def-num-ref-](sect-finality#defn-authority-set-id)).

:::
###### Definition -def-num- Justification {#defn-grandpa-justification}
:::definition

The **justification** for block ${B}$ in round ${r}$, ${J}^{{{r},\text{stage}}}{\left({B}\right)}$, is a vector of pairs of the type:

$$
{\left({V}{\left({B}'\right)},{\text{Sign}_{{{v}_{{i}}}}^{{{r},\text{stage}}}}{\left({B}'\right)},{v}_{{\text{id}}}\right)}
$$

in which either

${B}'\ge{B}$

or ${{V}_{{{v}_{{i}}}}^{{{r},\text{pc}}}}{\left({B}'\right)}$ is an equivocatory vote.

In all cases, ${\text{Sign}_{{{v}_{{i}}}}^{{{r},\text{stage}}}}{\left({B}'\right)}$ is the signature ([Definition -def-num-ref-](sect-finality#defn-sign-round-vote)) of voter ${v}_{{\text{id}}}\in{\mathbb{{V}}}_{{B}}$ broadcasted during either the pre-vote (stage = pv) or the pre-commit (stage = pc) sub-round of round r. A **valid justification** must only contain up-to-one valid vote from each voter and must not contain more than two equivocatory votes from each voter.

:::
###### Definition -def-num- Finalizing Justification {#defn-finalizing-justification}
:::definition

We say ${J}^{{{r},\text{pc}}}{\left({B}\right)}$ **justifies the finalization** of ${B}'\ge{B}$ **for a non-voter node** ${n}$ if the number of valid signatures in ${J}^{{{r},\text{pc}}}{\left({B}\right)}$ for ${B}'$ is greater than $\frac{{2}}{{3}}{\left|{\mathbb{{V}}}_{{B}}\right|}$.

Note that ${J}^{{{r},\text{pc}}}{\left({B}\right)}$ can only be used by a non-voter node to finalize a block. In contrast, a voter node can only be assured of the finality ([Definition -def-num-ref-](sect-finality#defn-finalized-block)) of block ${B}$ by actively participating in the voting process. That is by invoking [Play-Grandpa-Round](sect-finality#algo-grandpa-round).

The GRANDPA protocol dictates how an honest voter should vote in each sub-round, which is described by [Play-Grandpa-Round](sect-finality#algo-grandpa-round). After defining what constitutes a vote in GRANDPA, we define how GRANDPA counts votes.

:::
###### Definition -def-num- Equivocation {#defn-voter-equivocation}
:::definition

Voter ${v}$ **equivocates** if they broadcast two or more valid votes to blocks during one voting sub-round. In such a situation, we say that ${v}$ is an **equivocator** and any vote ${{V}_{{v}}^{{{r},\text{stage}}}}{\left({B}\right)}$ cast by ${v}$ in that sub-round is an **equivocatory vote**, and

$$
{\mathcal{{E}}}^{{{r},\text{stage}}}
$$

represents the set of all equivocators voters in sub-round *stage* of round ${r}$. When we want to refer to the number of equivocators whose equivocation has been observed by voter ${v}$ we refer to it by:

$$
{{\mathcal{{E}}}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}
$$

The Polkadot Host must detect equivocations committed by other validators and submit those to the Runtime as described in [Section -sec-num-ref-](chap-runtime-api#sect-grandpaapi_submit_report_equivocation_unsigned_extrinsic).

A vote ${{V}_{{v}}^{{{r},\text{stage}}}}={V}{\left({B}\right)}$ is **invalid** if

- ${H}{\left({B}\right)}$ does not correspond to a valid block.

- ${B}$ is not an (eventual) descendant of a previously finalized block.

- ${{M}_{{v}}^{{{r},\text{stage}}}}$ does not bear a valid signature.

- $\text{id}_{{{\mathbb{{V}}}}}$ does no match the current ${\mathbb{{V}}}$.

- ${{V}_{{v}}^{{{r},\text{stage}}}}$ is an equivocatory vote.

:::
###### Definition -def-num- Set of Observed Direct Votes {#defn-observed-direct-votes}
:::definition

For validator ${v}$, **the set of observed direct votes for Block ${B}$ in round ${r}$**, formally denoted by ${\text{VD}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}{\left({B}\right)}$ is equal to the union of:

- set of *valid* votes ${{V}_{{{v}_{{i}}}}^{{{r},\text{stage}}}}$ cast in round ${r}$ and received by ${v}$ such that ${{V}_{{{v}_{{i}}}}^{{{r},\text{stage}}}}={V}{\left({B}\right)}$.

:::
###### Definition -def-num- Set of Total Observed Votes {#defn-observed-votes}
:::definition

We refer to **the set of total votes observed by voter ${v}$ in sub-round *stage* of round ${r}$** by ${{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}$.

The **set of all observed votes by ${v}$ in the sub-round stage of round ${r}$ for block ${B}$**, **${{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}$** is equal to all of the observed direct votes cast for block ${B}$ and all of the ${B}$’s descendants defined formally as:

$$
{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}{\left({B}\right)}\:=\bigcup_{{{v}_{{i}}\in{\mathbb{{V}}},{B}<{B}'}}{\text{VD}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}{\left({B}'\right)}
$$

The **total number of observed votes for Block ${B}$ in round ${r}$** is defined to be the size of that set plus the total number of equivocator voters:

$$
{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}{\left({B}\right)}\:={\left|{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}{\left({B}\right)}\right|}+{\left|{{\mathcal{{E}}}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}\right|}
$$

Note that for genesis state we always have $\#{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{pv}}}}{\left({B}\right)}={\left|{\mathbb{{V}}}\right|}$.

:::
###### Definition -def-num- Set of Total Potential Votes {#defn-total-potential-votes}
:::definition

Let ${{V}_{{\text{unobs}{\left({v}\right)}}}^{{{r},\text{stage}}}}$ be the set of voters whose vote in the given stage has not been received. We define the **total number of potential votes for Block ${B}$ in round ${r}$** to be:

$$
\#{{V}_{{\text{obs}{\left({v}\right)},\text{pot}}}^{{{r},\text{stage}}}}{\left({B}\right)}\:={\left|{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}{\left({B}\right)}\right|}+{\left|{{V}_{{\text{unobs}{\left({v}\right)}}}^{{{r},\text{stage}}}}\right|}+\text{Min}{\left(\frac{{1}}{{3}}{\left|{\mathbb{{V}}}\right|},{\left|{\mathbb{{V}}}\right|}-{\left|{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{stage}}}}{\left({B}\right)}\right|}-{\left|{{V}_{{\text{unobs}{\left({v}\right)}}}^{{{r},\text{stage}}}}\right|}\right)}
$$

:::
###### Definition -def-num- Current Pre-Voted Block {#defn-grandpa-ghost}
:::definition

The current **pre-voted** block ${{B}_{{v}}^{{{r},\text{pv}}}}$ also know as GRANDPA GHOST is the block chosen by [GRANDPA-GHOST](sect-finality#algo-grandpa-ghost):

$$
{{B}_{{v}}^{{{r},\text{pv}}}}\:=\text{GRANDPA-GHOST}{\left({r}\right)}
$$

Finally, we define when a voter ${v}$ sees a round as completable, that is when they are confident that ${{B}_{{v}}^{{{r},\text{pv}}}}$ is an upper bound for what is going to be finalized in this round.

:::
###### Definition -def-num- Completable Round {#defn-grandpa-completable}
:::definition

We say that round ${r}$ is **completable** if ${\left|{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{pc}}}}\right|}+{{\mathcal{{E}}}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{pc}}}}>\frac{{2}}{{3}}{\mathbb{{V}}}$ and for all ${B}'>{{B}_{{v}}^{{{r},\text{pv}}}}$:

$$
{\left|{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{pc}}}}\right|}-{{\mathcal{{E}}}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{pc}}}}-{\left|{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{pc}}}}{\left({B}'\right)}\right|}>\frac{{2}}{{3}}{\left|{\mathbb{{V}}}\right|}
$$

Note that in practice we only need to check the inequality for those ${B}'>{{B}_{{v}}^{{{r},\text{pv}}}}$ where ${\left|{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},\text{pc}}}}{\left({B}'\right)}\right|}>{0}$.

:::
###### Definition -def-num- GRANDPA Consensus Message {#defn-consensus-message-grandpa}
:::definition

$\text{CM}_{{g}}$, the consensus message for GRANDPA, is of the following format:

$$
\text{CM}_{{g}}={\left\lbrace\begin{matrix}{1}&{\left(\text{Auth}_{{C}},{N}_{{\text{delay}}}\right)}\\{2}&{\left({m},\text{Auth}_{{C}},{N}_{{\text{delay}}}\right)}\\{3}&\text{A}_{{i}}\\{4}&{N}_{{\text{delay}}}\\{5}&{N}_{{\text{delay}}}\end{matrix}\right.}
$$

**where**

|  |  |
|--|--|
| **$N_{\text{delay}}$** | is an unsigned 32-bit integer indicating how deep in the chain the announcing block must be before the change is applied. |
| **1** | Implies **scheduled change**: Schedule an authority set change after the given delay of ${N_{\text{delay}} := \|\text{SubChain}(B,B')\|}$ where ${B'}$ is the block where the change is applied. The earliest digest of this type in a single block will be respected, unless a force change is present, in which case the force change takes precedence. |
| **2** | Implies **forced change**: Schedule a forced authority set change after the given delay of ${N_{\text{delay}} := \|\text{SubChain}(B,m + B')\|}$ where ${B'}$ is the block where the change is applied. The earliest digest of this type in a block will be respected. <br/><br/> Forced changes are explained further in [Section -sec-num-ref-](sect-finality#sect-finality-forced-changes). |
| **3** | Implies **on disabled**: An index to the individual authority in the current authority list ([Definition -def-num-ref-](chap-sync#defn-authority-list)) that should be immediately disabled until the next authority set changes. When an authority gets disabled, the node should stop performing any authority functionality from that authority, including authoring blocks and casting GRANDPA votes for finalization. Similarly, other nodes should ignore all messages from the indicated authority which pertain to their authority role. |
| **4** | Implies **pause**: A signal to pause the current authority set after the given delay of ${N_{\text{delay}} := \|\text{SubChain}(B,B')\|}$ where ${B'}$ is a block where the change is applied. Once applied, the authorities should stop voting. |
| **5** | Implies **resume**: A signal to resume the current authority set after the given delay of ${N_{\text{delay}} := \|\text{SubChain}(B,B')\|}$ where ${B'}$ is the block where the change is applied. Once applied, the authorities should resume voting. |

:::
## -sec-num- Initiating the GRANDPA State {#id-initiating-the-grandpa-state}

In order to participate coherently in the voting process, a validator must initiate its state and sync it with other active validators. In particular, considering that voting is happening in different distinct rounds where each round of voting is assigned a unique sequential round number ${r}_{{v}}$, it needs to determine and set its round counter ${r}$ equal to the voting round ${r}_{{n}}$ currently undergoing in the network. The mandated initialization procedure for the GRANDPA protocol for a joining validator is described in detail in [Initiate-Grandpa](sect-finality#algo-initiate-grandpa).

The process of joining a new voter set is different from the one of rejoining the current voter set after a network disconnect. The details of this distinction are described further in this section.

### -sec-num- Voter Set Changes {#id-voter-set-changes}

A GRANDPA voter node which is initiating GRANDPA protocol as part of joining a new authority set is required to execute [Initiate-Grandpa](sect-finality#algo-initiate-grandpa). The algorithm mandates the initialization procedure for GRANDPA protocol.

:::info
The GRANDPA round number reset to 0 for every authority set change.
:::

Voter set changes are signaled by Runtime via a consensus engine message ([Section -sec-num-ref-](chap-sync#sect-consensus-message-digest)). When Authorities process such messages they must not vote on any block with a higher number than the block at which the change is supposed to happen. The new authority set should reinitiate GRANDPA protocol by executing [Initiate-Grandpa](sect-finality#algo-initiate-grandpa).

###### Algorithm -algo-num- Initiate Grandpa {#algo-initiate-grandpa}
:::algorithm
<Pseudocode
    content={initiateGrandpa}
    algID="initiateGrandpa"
    options={{ "lineNumber": true }}
/>

where ${B}_{{\text{last}}}$ is the last block which has been finalized on the chain ([Definition -def-num-ref-](sect-finality#defn-finalized-block)). ${r}_{{\text{last}}}$ is equal to the latest round the voter has observed that other voters are voting on. The voter obtains this information through various gossiped messages including those mentioned in [Definition -def-num-ref-](sect-finality#defn-finalized-block). ${r}_{{\text{last}}}$ is set to *0* if the GRANDPA node is initiating the GRANDPA voting process as a part of a new authority set. This is because the GRANDPA round number resets to *0* for every authority set change.
:::

## -sec-num- Rejoining the Same Voter Set {#id-rejoining-the-same-voter-set}

When a voter node rejoins the network after a disconnect from the voter set and with the condition that there has been no change to the voter set at the time of the disconnect, the node must continue performing the GRANDPA protocol at the same state as before getting disconnected from the network, ignoring any possible progress in GRANDPA finalization. Following reconnection, the node eventually gets updated to the current GRANDPA round and synchronizes its state with the rest of the voting set through the process called Catchup ([Section -sec-num-ref-](sect-finality#sect-grandpa-catchup)).

## -sec-num- Voting Process in Round ${r}$ {#id-voting-process-in-round-r}

For each round ${r}$, an honest voter ${v}$ must participate in the voting process by following [Play-Grandpa-Round](sect-finality#algo-grandpa-round).

###### Algorithm -algo-num- Play Grandpa Round {#algo-grandpa-round}
:::algorithm
<Pseudocode
    content={playGrandpaRound}
    algID="playGrandpaRound"
    options={{ "lineNumber": true }}
/>

**where**  
- ${T}$ is sampled from a log-normal distribution whose mean and standard deviation are equal to the average network delay for a message to be sent and received from one validator to another.

- $\text{Derive-Primary}$ is described in [Derive-Primary](sect-finality#algo-derive-primary).

- The condition of *completablitiy* is defined in [Definition -def-num-ref-](sect-finality#defn-grandpa-completable).

- $\text{Best-Final-Candidate}$ function is explained in [Best-Final-Candidate](sect-finality#algo-grandpa-best-candidate).

- $\text{Attempt-To-Finalize-At-Round}{\left({r}\right)}$ is described in [Attempt-To-Finalize-At-Round](sect-finality#algo-attempt-to–finalize).

- $\text{Finalizable}$ is defined in [Finalizable](sect-finality#algo-finalizable).
:::

###### Algorithm -algo-num- Derive Primary {#algo-derive-primary}
:::algorithm
<Pseudocode
    content={derivePrimary}
    algID="derivePrimary"
    options={{ "lineNumber": true }}
/>

where ${r}$ is the GRANDPA round whose primary is to be determined.
:::

###### Algorithm -algo-num- Best Final Candidate {#algo-grandpa-best-candidate}
:::algorithm
<Pseudocode
    content={bestFinalCandidate}
    algID="bestFinalCandidate"
    options={{ "lineNumber": true }}
/>

where $\#{{V}_{{\text{obv}{\left({v}\right)},{p}{o}{t}}}^{{{r},{p}{c}}}}$ is defined in [Definition -def-num-ref-](sect-finality#defn-total-potential-votes).
:::

###### Algorithm -algo-num- GRANDPA GHOST {#algo-grandpa-ghost}
:::algorithm
<Pseudocode
    content={grandpaGhost}
    algID="grandpaGhost"
    options={{ "lineNumber": true }}
/>

**where**  
- ${B}_{{\text{last}}}$ is the last block which has been finalized on the chain ([Definition -def-num-ref-](sect-finality#defn-finalized-block)).

- $\#{{V}_{{\text{obs}{\left({v}\right)}}}^{{{r},{p}{v}}}}{\left({B}\right)}$ is defined in [Definition -def-num-ref-](sect-finality#defn-observed-votes).
:::

###### Algorithm -algo-num- Best PreVote Candidate {#algo-best-prevote-candidate}
:::algorithm
<Pseudocode
    content={bestPrevoteCandidate}
    algID="bestPrevoteCandidate"
    options={{ "lineNumber": true }}
/>
:::

###### Algorithm -algo-num- Attempt To Finalize At Round {#algo-attempt-to–finalize}
:::algorithm
<Pseudocode
    content={attemptToFinalizeAtRound}
    algID="attemptToFinalizeAtRound"
    options={{ "lineNumber": true }}
/>
:::

###### Algorithm -algo-num- Finalizable {#algo-finalizable}
:::algorithm
<Pseudocode
    content={finalizable}
    algID="finalizable"
    options={{ "lineNumber": true }}
/>

where the condition for *completability* is defined in [Definition -def-num-ref-](sect-finality#defn-grandpa-completable).
:::

Note that we might not always succeed in finalizing our best final candidate due to the possibility of equivocation. We might even not finalize anything in a round (although [Play-Grandpa-Round](sect-finality#algo-grandpa-round) prevents us from moving to the round ${r}+{1}$ before finalizing the best final candidate of round ${r}-{1}$) The example in [Definition -def-num-ref-](sect-finality#defn-unfinalized-candidate) serves to demonstrate a situation where the best final candidate of a round cannot be finalized during its own round:

###### Definition -def-num- Unfinalized Candidate {#defn-unfinalized-candidate}
:::definition

Let us assume that we have 100 voters and there are two blocks in the chain (${B}_{{1}}<{B}_{{2}}$). At round 1, we get 67 pre-votes for ${B}_{{2}}$ and at least one pre-vote for ${B}_{{1}}$ which means that $\text{GRANDPA-GHOST}{\left({1}\right)}={B}_{{2}}$.

Subsequently, potentially honest voters who could claim not seeing all the pre-votes for ${B}_{{2}}$ but receiving the pre-votes for ${B}_{{1}}$ would pre-commit to ${B}_{{1}}$. In this way, we receive 66 pre-commits for ${B}_{{1}}$ and 1 pre-commit for ${B}_{{2}}$. Henceforth, we finalize ${B}_{{1}}$ since we have a threshold commit (67 votes) for ${B}_{{1}}$.

At this point, though, we have ${\mathtt{\text{Best-Final-Candidate}}}{\left({r}\right)}={B}_{{2}}$ as $\#{{V}_{{\text{obs}{\left({v}\right)},\text{pot}}}^{{{r},\text{stage}}}}{\left({B}_{{2}}\right)}={67}$ and ${2}>{1}$.

However, at this point, the round is already completable as we know that we have ${\mathtt{\text{GRANDPA-GHOST}}}{\left({1}\right)}={B}_{{2}}$ as an upper limit on what we can finalize and nothing greater than ${B}_{{2}}$ can be finalized at ${r}={1}$. Therefore, the condition of [Play-Grandpa-Round](sect-finality#algo-grandpa-round) is satisfied and we must proceed to round 2.

Nonetheless, we must continue to attempt to finalize round *1* in the background as the condition of [Attempt-To-Finalize-At-Round](sect-finality#algo-attempt-to–finalize) has not been fulfilled.

This prevents us from proceeding to round 3 until either:

- We finalize ${B}_{{2}}$ in round 2, or

- We receive an extra pre-commit vote for ${B}_{{1}}$ in round 1. This will make it impossible to finalize ${B}_{{2}}$ in round 1, no matter to whom the remaining pre-commits are going to be cast for (even with considering the possibility of 1/3 of voter equivocating) and therefore we have ${\mathtt{\text{Best-Final-Candidate}}}{\left({r}\right)}={B}_{{1}}$.

Both scenarios unblock [Play-Grandpa-Round](sect-finality#algo-grandpa-round), ${\mathtt{\text{Last-Finalized-Block}}}\ge{\mathtt{\text{Best-Final-Candidate}}}{\left({r}-{1}\right)}$ albeit in different ways: the former with increasing the ${\mathtt{\text{Last-Finalized-Block}}}$ and the latter with decreasing ${\mathtt{\text{Best-Final-Candidate}}}{\left({r}-{1}\right)}$.

:::
## -sec-num- Forced Authority Set Changes {#sect-finality-forced-changes}

In a case of emergency where the Polkadot network is unable to finalize blocks, such as in an event of mass validator outage, the Polkadot governance mechanism must enact a forced change, which the Host must handle in a specific manner. Given that in such a case finality cannot be relied on, the Host must detect the forced change ([Definition -def-num-ref-](sect-finality#defn-consensus-message-grandpa)) in a (valid) block and apply it to all forks.

The ${m}\in{C}{M}_{{g}}$, which is specified by the governance mechanism, defines the starting block at which ${N}_{{\text{delay}}}$ is applied. This provides some degree of probabilistic consensus to the network with the assumption that the forced change was received by most participants and that finality can be continued.

###### Image -img-num- Applying a scheduled change {#img-scheduled-change}

![](/img/scheduled-change.png)

###### Image -img-num- Applying a forced change {#img-forced-change}

![](/img/forced-change.png)

## -sec-num- Block Finalization {#sect-block-finalization}

###### Definition -def-num- Justified Block Header {#defn-justified-block-header}
:::definition

The Justified Block Header is provided by the consensus engine and presented to the Polkadot Host, for the block to be appended to the blockchain. It contains the following parts:

- **block_header** the complete block header ([Definition -def-num-ref-](chap-state#defn-block-header)) and denoted by $\text{Head}{\left({B}\right)}$.

- **justification**: as defined by the consensus specification indicated by $\text{Just}{\left({B}\right)}$ as defined in [Definition -def-num-ref-](sect-finality#defn-grandpa-justification).

- **authority Ids**: This is the list of the Ids of authorities, which have voted for the block to be stored and is formally referred to as ${A}{\left({B}\right)}$. An authority Id is 256-bit.

:::
###### Definition -def-num- Finalized {#defn-finalized-block}
:::definition

A Polkadot relay chain node ${n}$ should consider block ${B}$ as **finalized** if any of the following criteria hold for ${B}'\ge{B}$:

- ${{V}_{{\text{obs}{\left({n}\right)}}}^{{{r},\text{pc}}}}{\left({B}'\right)}>\frac{{2}}{{3}}{\left|{\mathbb{{V}}}_{{{B}'}}\right|}$.

- It receives a ${{M}_{{v}}^{{{r},\text{Fin}}}}{\left({B}'\right)}$ message in which ${J}^{{r}}{\left({B}\right)}$ justifies the finalization ([Definition -def-num-ref-](sect-finality#defn-grandpa-justification)).

- It receives a block data message for ${B}'$ with $\text{Just}{\left({B}'\right)}$ ([Definition -def-num-ref-](sect-finality#defn-justified-block-header)) which justifies the finalization.

for:

- Any round ${r}$ if the node ${n}$ is *not* a GRANDPA voter.

- Only for round ${r}$ for which the node ${n}$ has invoked [Play-Grandpa-Round](sect-finality#algo-grandpa-round) and round ${r}+{1}$ if ${n}$ is a GRANDPA voter and has already caught up to its peers according to the process described in Section [Section -sec-num-ref-](sect-finality#sect-grandpa-catchup).

Note that all Polkadot relay chain nodes are supposed to process GRANDPA commit messages regardless of their GRANDPA voter status.

:::
### -sec-num- Catching up {#sect-grandpa-catchup}

When a Polkadot node (re)joins the network, it requests the history of state transitions in the form of blocks, which it is missing.

Nonetheless, the process is different for a GRANDPA voter node. When a voter node joins the network, it needs to gather the justification ([Definition -def-num-ref-](sect-finality#defn-grandpa-justification)) of the rounds it has missed. Through this process, they can safely join the voting process of the current round, on which the voting is taking place.

#### -sec-num- Sending the catch-up requests {#sect-sending-catchup-request}

When a Polkadot voter node has the same authority list as a peer voter node who is reporting a higher number for the *finalized round* field, it should send a catch-up request message ([Definition -def-num-ref-](chap-networking#defn-grandpa-catchup-request-msg)) to the reporting peer. This will allow the node to to catch up to the more advanced finalized round, provided that the following criteria hold:

- The peer node is a GRANDPA voter, and:

- The last known finalized round for the Polkadot node is at least 2 rounds behind the finalized round for the peer.

#### -sec-num- Processing the catch-up requests {#id-processing-the-catch-up-requests}

Only GRANDPA voter nodes are required to respond to the catch-up requests. Additionally, it is only GRANDPA voters who are supposed to send catch-up requests. As such GRANDPA voters could safely ignore the catch-up requests from non-voter nodes. When a GRANDPA voter node receives a catch-up request message, it needs to execute [Process-Catchup-Request](sect-finality#algo-process-catchup-request). Note: a voter node should not respond to catch-up requests for rounds that are actively being voted on, those are the rounds for which [Play-Grandpa-Round](sect-finality#algo-grandpa-round) is not concluded.

###### Algorithm -algo-num- Process Catchup Request {#algo-process-catchup-request}
:::algorithm
<Pseudocode
    content={processCatchupRequest}
    algID="processCatchupRequest"
    options={{ "lineNumber": true }}
/>

**where**  
- ${{M}_{{{i},{v}}}^{{\text{Cat}-{q}}}}{\left(\text{id}_{{{\mathbb{{V}}}}},{r}\right)}$ is the catch-up message received from peer ${i}$ ([Definition -def-num-ref-](chap-networking#defn-grandpa-catchup-request-msg)).

- $\text{id}_{{{\mathbb{{V}}}}}$ ([Definition -def-num-ref-](sect-finality#defn-authority-set-id)) is the voter set id with which the serving node is operating

- ${r}$ is the round number for which the catch-up is requested for.

- ${\mathbb{{P}}}$ is the set of immediate peers of node ${v}$.

- ${\mathtt{\text{Last-Completed-Round}}}$ is initiated in [Initiate-Grandpa](sect-finality#algo-initiate-grandpa) and gets updated by [Play-Grandpa-Round](sect-finality#algo-grandpa-round).

- ${{M}_{{{v},{i}}}^{{\text{Cat}-{s}}}}{\left(\text{id}_{{{\mathbb{{V}}}}},{r}\right)}$ is the catch-up response ([Definition -def-num-ref-](chap-networking#defn-grandpa-catchup-response-msg)).
:::

#### -sec-num- Processing catch-up responses {#id-processing-catch-up-responses}

A Catch-up response message contains critical information for the requester node to update their view on the active rounds which are being voted on by GRANDPA voters. As such, the requester node should verify the content of the catch-up response message and subsequently updates its view of the state of the finality of the Relay chain according to [Process-Catchup-Response](sect-finality#algo-process-catchup-response).

###### Algorithm -algo-num- Process Catchup Response {#algo-process-catchup-response}
:::algorithm
<Pseudocode
    content={processCatchupResponse}
    algID="processCatchupResponse"
    options={{ "lineNumber": true }}
/>

where ${{M}_{{{v},{i}}}^{{\text{Cat}-{s}}}}{\left(\text{id}_{{{\mathbb{{V}}}}},{r}\right)}$ is the catch-up response received from node ${v}$ ([Definition -def-num-ref-](chap-networking#defn-grandpa-catchup-response-msg)).
:::
