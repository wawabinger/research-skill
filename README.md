# research-skills

Claude Code skills for research work.

| Skill | Use |
|---|---|
| [`paper-reading`](paper-reading/) | Turn an academic paper into a structured bilingual reading note (from [pengsida/learning_research](https://github.com/pengsida/learning_research)) |
| [`brief`](brief/) | Fixed-format brief for review and approval: decisions, principle & conclusion, evidence, risks & next steps |
| [`exp-report`](exp-report/) | Fixed-format experiment report appended to `doc/experiment_log.md`: goal, setting, results, analysis, next experiments |
| [`cs-academic-writing`](cs-academic-writing/) | CS academic writing and polishing: papers, theses, proposals, reviewer responses (from [cs-academic-writing-claude-skill](https://github.com/wawabinger/cs-academic-writing-claude-skill)) |

## Installation

Copy the skill folders you want into your Claude Code skills directory, then restart the session:

```bash
git clone git@github.com:wawabinger/research-skills.git
cp -R research-skills/{paper-reading,brief,exp-report,cs-academic-writing} ~/.claude/skills/
```

Optional, for automatic triggering of `brief` / `exp-report`, add to `~/.claude/CLAUDE.md`:

```markdown
- 写简报/报告/方案待批/长任务总结/论文修改说明时，必须先加载 `brief` skill；写实验报告/实验记录时，必须先加载 `exp-report` skill。均按其固定模板输出。
```
