# Configuration, PII, and secret architecture: rationale and baseline

The lab's volume is growing faster than ad hoc practice can hold. Four
requirements drive the architecture:

1. **Repository deletion must be non-destructive.** Removing a local
   checkout must never destroy credentials, because gitignored secrets are
   invisible to every backup that follows the repository.
2. **The workspace must be portable.** Moving the workspace root to another
   user profile, machine, or container must preserve every secret and break
   no path.
3. **Nothing brand-specific or person-specific may be hardcoded.** Per
   foundation D12, identity is a variable; the same applies to the operator's
   personal data.
4. **Agents operate this estate.** Unattended agents read configuration and
   must never be able to read a credential they do not need, or leak one
   into a prompt, a log, or a commit.

## 2. Current state audit

Observed in the workspace on 2026-10-25. This is the baseline the
architecture must improve, recorded honestly so progress is measurable.

| Observation                                                                                                                                                                                                     | Assessment                                                                                                                                                                    |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A root-level `config/` directory already exists outside every project repository                                                                                                                                | Correct instinct and the right foundation. The centralization principle is already in practice                                                                                |
| `config/secrets/` is gitignored and organized by platform subdirectory                                                                                                                                          | Good shape: platform grouping scales better than per-repo duplication                                                                                                         |
| Secret material is stored unencrypted at rest: dotenv files, a private certificate, an OAuth client secret document, a database credential file, a git-crypt key, and recovery codes                            | **Finding.** Disk encryption is the only control. Any process, backup, sync client, or agent with filesystem read access reads everything                                     |
| `pii.json` carries full legal name, phone, email, location, and immigration status, and is **tracked** in a git repository                                                                                      | **Finding.** The repository currently has no remote, so exposure is latent rather than actual. One `git remote add` turns latent into permanent, because history preserves it |
| The parent meta-repo gitignores `config/` and also ignores `.env`, `*.env`, `*.pem`, `*.key`, and `secrets/` at any depth                                                                                       | Strong defense in depth; keep it                                                                                                                                              |
| Absolute paths appear in generated artifacts (for example the installed scheduler job in agent-research-kit)                                                                                                    | **Finding.** Blocks requirement 2: moving the workspace root breaks resolution                                                                                                |
| The RTS repository (`org-intelligence-revenue-system/shared/config`) already implements tracked `_template` and `_default` trees with gitignored real data, a documented precedence chain, and a management CLI | **This is the pattern to generalize.** It solves per-entity config correctly; the lab needs the same model one level up                                                       |

The RTS precedence chain, worth lifting verbatim as a convention:
explicit flag, then environment variable, then an active-context file, then
a single existing candidate.
