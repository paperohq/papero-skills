# Papero skills

Three skills for AI assistants that use the [Papero](https://papero.ai/) connector. Each one makes the assistant check scholarly records instead of answering from memory, which is where invented references come from.

| Skill | What it does |
|---|---|
| [verify-references](skills/verify-references/SKILL.md) | Checks a reference list you paste in: which entries match a real record, which have a DOI that belongs to another paper, which are marked retracted, which cannot be found. |
| [find-papers-for-a-claim](skills/find-papers-for-a-claim/SKILL.md) | Finds real papers for one sentence you want to cite, and says whether each one supports it. |
| [check-document-citations](skills/check-document-citations/SKILL.md) | Reads a document stored in your Papero account and reports sources that are marked retracted or not found, citations that do not fit their sentence, and claims with no citation. Checking the sources needs Papero Plus; on Free it lists the claims with no citation. |

## What you need

1. A Papero account. The Free plan works: [sign up](https://papero.ai/signup?plan=free).
2. The Papero connector added to your assistant. Its address is `https://app.papero.ai/mcp`, and you sign in with your Papero account. Steps for Claude, ChatGPT and Claude Code are at [papero.ai/connect](https://papero.ai/connect).

The skills are plain `SKILL.md` files in the Agent Skills format. They were written for Claude. Other assistants that support skills and remote MCP connectors may be able to use them too.

## Install

### Claude Code

This repository is also a Claude Code plugin that adds the connector and the three skills together:

```
/plugin marketplace add paperoai/papero-skills
/plugin install papero@papero-skills
```

Then type `/mcp`, choose `plugin:papero:papero` under Plugin MCPs and sign in.

### Claude (claude.ai and Claude Desktop)

Add the connector first, as described at [papero.ai/connect](https://papero.ai/connect). Then download this repository, zip one skill folder (for example `skills/verify-references`) and upload it under Skills in your settings. Repeat for each skill you want.

### Anywhere else

Copy the folders under `skills/` to wherever your assistant reads skills from.

## Try it

- "Here is my reference list. Are these all real papers?" followed by the list.
- "I need a source for this sentence: students who sleep less than six hours before an exam recall less of what they studied."
- "Check the citations in my Papero document on climate migration before I submit it."

## Limits

- **Paper searches count against your plan.** Each search uses one of your Papero paper searches: 20 a day on Free, 1,000 a month on Plus. Looking a paper up by DOI, PMID, arXiv ID or ISBN does not. The skills check how many searches you have left, ask before using more than a few, and say how many they used.
- **Documents on Free.** The connector reads your document's text on any plan. On Free, the details of a document's references stay hidden, as they do in the app, so `check-document-citations` can only look for claims with no citation. Checking the sources needs Plus. See [pricing](https://papero.ai/pricing).
- **Formatting.** Reference lists can be formatted in nine styles (APA 7, MLA 9, Chicago author-date, Harvard, IEEE, Vancouver, AMA 11, Nature, ACS), up to 20 references at a time, on every plan. The Papero app itself has over 10,000 styles.
- **"Not found" is not proof.** OpenAlex, the index behind the search, covers journal articles best. Books, chapters, reports and very recent work are found less often. The skills say so in their reports.
- **Abstracts, not full text.** Whether a paper supports a sentence is judged from its abstract. Read what you cite.

## Read-only, and you stay in control

The connector cannot change or delete anything in Papero, and it does not run Papero's AI features. You sign in on Papero's own page, so the assistant never receives your password or an API key. The assistant receives the answers to the tools it calls, which can include the text of a document you ask it to read; what its provider does with them is covered by that provider's terms. You can disconnect at any time in the Papero app under Settings, Integrations, Connected apps. Details are in Papero's [privacy policy](https://papero.ai/privacy).

To check a short list without an assistant or an account, the free [reference checker](https://papero.ai/tools/reference-checker) on papero.ai takes up to ten references at a time, five checks a day.

## Questions

Write to contact@papero.ai.

## License

MIT. See [LICENSE](LICENSE).
